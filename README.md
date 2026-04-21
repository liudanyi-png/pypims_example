# pypims_example
pypims安装及模拟嘉峪关淹没参考代码
参考步骤：https://jishuzhan.net/article/1945785159780970497

我的计算机操作系统为Windows 11，系统类型是64 位操作系统。
具体步骤如下：
一、依次安装Miniconda、Git、Visual Studio、NVIDIA CUDA Toolkit。
二、克隆Pypims项目
进入欲安装的文件夹，在命令提示符工具中，输入以下命令：
git clone https://github.com/pypims/pypims.git
cd pypims
三、修改CmakeLists
当前 CUDA 版本或显卡驱动 不再支持 sm_35。因此需要在Pypims项目文件./pypims/pypims/CMakeLists.txt中，去掉对sm_35的支持，并替换为本机显卡支持的Compute Capability（sm_86）。
CUDA GPU Compute Capability查询网址：https://developer.nvidia.com/cuda-gpus

RTX A4000 → Compute Capability = 8.6 → sm_86

IF(WIN32)
    set(PLATFORM_CXX_FLAGS /Zi)
    set(CUDA_SEPARABLE_COMPILATION ON)
    set(CUDA_NVCC_FLAGS -arch=sm_86;--expt-extended-lambda)
ENDIF(WIN32)
四、修改cuda_data_bank.cu
在./pypims/pypims/lib/src/multi_threading/cuda_data_bank.cu代码中，使用了 HEMI_DEV_CALLABLE_INLINE_MEMBER 宏，它的作用是用来兼容 GPU 和 CPU 编译环境。而 HEMI 本身不再与新版本 CUDA（>= 11）和 Thrust 完美兼容。再加上我使用的是 CUDA 12.9，在编译时会触发错误，解决方案是手动定义 thrust::device_vector<GC::Vector3> 时不要使用 .resize(n)。
// 不推荐
thrust::device_vector<GC::Vector3> v;
v.resize(n);  // ❌ 这会默认构造 device 端 Vector3，如果 Thrust 不支持就会崩溃

// 推荐
std::vector<GC::Vector3> host_vec(n, GC::Vector3(0, 0, 0));
thrust::device_vector<GC::Vector3> v = host_vec;
因此对cuda_data_bank.cu文件的cuDataBankBranch函数修改为：
  cuDataBankBranch::cuDataBankBranch(unsigned int _size_lower2receive, unsigned int _size_lower2send, unsigned int _size_upper2receive, unsigned int _size_upper2send)
    :size_lower2receive(_size_lower2receive), size_lower2send(_size_lower2send), size_upper2receive(_size_upper2receive), size_upper2send(_size_upper2send){
    lower_status = 0;
    std::vector<GC::Vector3> host_vec1(size_lower2receive, GC::Vector3(0, 0, 0));
    data_lower = host_vec1;
    indices_lower2receive = host_vec1;
    std::vector<GC::Vector3> host_vec2(size_lower2send, GC::Vector3(0, 0, 0));
    indices_lower2send = host_vec2;
    upper_status = 0;
    std::vector<GC::Vector3> host_vec3(size_upper2receive, GC::Vector3(0, 0, 0));
    data_upper = host_vec3;
    indices_upper2receive = host_vec3;
    std::vector<GC::Vector3> host_vec4(size_upper2send, GC::Vector3(0, 0, 0));
    indices_upper2send = host_vec4;
  }
五、创建虚拟环境
conda create -n pypims python=3.7 -y
六、安装依赖
首先激活环境：
conda activate pypims
依次安装以下依赖，如安装出错，请直接单独下载对应版本安装包进行下载：
conda install cmake -y
conda install gdal -y
conda install rasterio -y
conda install fiona -y
conda install numpy -y
conda install scipy -y
conda install matplotlib -y
conda install imageio -y
conda install pandas -y
conda install pyshp -y
conda install "sphinx>=4.1" -y
conda install "sphinx-rtd-theme>=1.0.0" -y
conda install nbsphinx -y
conda install ipykernel -y
六、安装pypims
python setup.py install
或者：
conda install pypims
或者：
pip install pypims

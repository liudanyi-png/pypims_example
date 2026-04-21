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
四、修改cuda_data_bank.cu  
在./pypims/pypims/lib/src/multi_threading/cuda_data_bank.cu代码中，使用了 HEMI_DEV_CALLABLE_INLINE_MEMBER 宏，它的作用是用来兼容 GPU 和 CPU 编译环境。而 HEMI 本身不再与新版本 CUDA（>= 11）和 Thrust 完美兼容。再加上我使用的是 CUDA 12.9，在编译时会触发错误，解决方案是手动定义 thrust::device_vector<GC::Vector3> 时不要使用 .resize(n)。  

五、创建虚拟环境  
conda create -n pypims python=3.7 -y  
六、安装依赖  
首先激活环境：  
conda activate pypims  
依次安装以下依赖，如安装出错，请直接单独下载对应版本安装包进行下载：  
cmake、
gdal、
 rasterio 、
fiona、
numpy、
scipy、
matplotlib、
imageio 、
pandas 、
pyshp 、
"sphinx>=4.1"、
"sphinx-rtd-theme>=1.0.0"、
nbsphinx、
ipykernel 、  
七、安装pypims


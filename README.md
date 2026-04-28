# pypims_example

pypims安装及模拟嘉峪关淹没参考代码

具体步骤：https://jishuzhan.net/article/1945785159780970497   
代码及数据放在压缩包内，请修改文件路径运行。  
我的计算机操作系统为Windows 10，系统类型是64 位操作系统。

简要步骤如下：  

* **依次安装所需软件**
  Miniconda、Git、Visual Studio、NVIDIA CUDA Toolkit。

* **克隆Pypims项目**
  进入欲安装的文件夹，在命令提示符工具中，输入以下命令：
  ```bash
  git clone [https://github.com/pypims/pypims.git](https://github.com/pypims/pypims.git)
  cd pypims
  ```

* **修改CmakeLists**
  

* **修改cuda_data_bank.cu**
 

* **创建虚拟环境**
  ```bash
  conda create -n pypims python=3.7 -y
  ```

* **安装依赖**
  首先激活环境：
  ```bash
  conda activate pypims
  ```
  依次安装以下依赖，如安装出错，请直接单独下载对应版本安装包进行下载：  
  cmake、gdal、rasterio、fiona、numpy、scipy、matplotlib、imageio、pandas、pyshp、"sphinx>=4.1"、"sphinx-rtd-theme>=1.0.0"、nbsphinx、ipykernel

* **安装pypims**

# pypims_example

pypims安装及模拟嘉峪关淹没参考代码

具体步骤：https://jishuzhan.net/article/1945785159780970497   
代码及数据放在压缩包内，请修改文件路径运行。   
本地环境详细请见_local后缀文件，远程服务器详见_remote后缀服务器 


我的本地计算机操作系统为Windows 10，系统类型是64 位操作系统。  
### pypims 本地环境包版本总结清单

| 软件包名称 | 安装版本 | 安装渠道 |
| :--- | :--- | :--- |
| **cmake** | 3.31.2 | conda |
| **GDAL** | 3.4.2 | pip |
| **rasterio** | 1.2.8 | pip |
| **Fiona** | 1.8.21 | pip |
| **numpy** | 1.21.6 | pip |
| **scipy** | 1.7.3 | pip |
| **matplotlib** | 3.5.3 | pip |
| **imageio** | 2.36.0 | pip |
| **pandas** | 1.3.5 | pip |
| **pyshp** | 2.3.1 | pip |
| **Sphinx** | 5.3.0 | pip |
| **sphinx-rtd-theme** | 2.0.0 | pip |
| **nbsphinx** | 0.9.7 | pip |
| **ipykernel** | 6.16.2 | pip |  
  

### pypims 远程服务器环境包版本总结清单 (Linux/Conda)

| 软件包名称 | 安装版本 | 安装渠道 |
| :--- | :--- | :--- |
| **cmake** | 3.22.1 | conda |
| **GDAL** | 3.0.2 | pip |
| **rasterio** | 1.2.10 | pip |
| **Fiona** | 1.8.22 | pip |
| **numpy** | 1.21.5 | pip |
| **scipy** | 1.7.3 | pip |
| **matplotlib** | 3.5.3 | pip |
| **imageio** | 2.9.0 | pip |
| **pandas** | 1.3.5 | pip |
| **pyshp** | 2.1.3 | pip |
| **Sphinx** | 5.0.2 | pip |
| **nbsphinx** | 0.9.7 | pip |
| **ipykernel** | 6.16.2 | pip |

  
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

# Barcode
记录使用opencv+zxing进行条码识别并解码的方式
### 系统
Ubuntu16.0
### 详细说明
因为本人使用的是windows10系统，要用到linux，通过在VMware Workstation上安装虚拟机的方式使用Ubuntu16.0
### 步骤
1. 在VMware 上安装Ubuntu，指路一个比较好的博客http://blog.csdn.net/u013142781/article/details/50529030
2. 安装opencv
* 安装依赖
```bash
sudo apt-get install build-essential libgtk2.0-dev libjpeg-dev libtiff5-dev libjasper-dev libopenexr-dev cmake libeigen3-dev yasm libfaac-dev libtheora-dev libx264-dev libv4l-dev libavcodec-dev libavformat-dev libswscale-dev libv4l-dev ffmpeg
```
* 将opencv-3.2.0.zip解压到某个目录下，在命令行中进入该目录
* 新建编译目录并进入
```bash
mkdir release
cd release
```
* 编译
```bash
cmake -D MAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D WITH_OPENCL=OFF -D WITH_CUDA=OFF ..
make
```
* 安装
```bash
sudo make install
```
* 配置链接库
```bash
sudo /bin/bash -c 'echo "/usr/local/lib" > /etc/ld.so.conf.d/opencv.conf'
sudo ldconfig
```
* 完成后使用命令查看安装版本
```bash
pkg-config --modversion opencv
```
* 出现问题
  * 其中在编译过程中出现ippicv_linux_20151201.tgz校验和不符的问题，通过查询相关资料和指定目录下的文件，发现时因为在下载时被墙或者下载网站出现问题导致，所以在网上找到了ippicv_linux_20151201.tgz压缩包替换掉指定目录下的该文件并重新编译就可以了。
3. zxing库使用
* 使用方法在zxing_using库中给出
4. 在zxing中添加opencv的使用
* 将zxing中初始的读取图片解码改为使用opencv获取摄像头读取图片之后调用方法解码，最终给出zxing-cpp-master，使用时在命令行中进入
```bash
mkdir build
cd build
cmake ..
make
./zxing
```
* 在摄像头前放置条码图像就可以进行识别并解码

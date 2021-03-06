# smplify-x_in_docker

## 简介
smplify-x是德国马普所基于SMPLx开发的人体3d mesh预测网络，因为在复现时配环境非常费劲，所以写了这个配置docker的方法，配置完成之后即可直接在docker的容器中运行smplify。

使用docker主要时基于以下两点：
* smplify-x不能使用anaconda配置虚拟环境，经常会报错。
* 使用virtualenv可能不会出错，但是保险起见，还是使用容器更好。


## 运行
首先下载dockerfile以及所有需要的安装包并进入项目文件夹
```Shell
git clone https://github.com/wells-wei-wei/smplify-x_in_docker
cd smplify-x_in_docker
```
还要记得先从马普所的官网（https://smpl-x.is.tue.mpg.de/ ）下载smplx的模型，将解压后的models文件夹放到smplify-x_in_docker里（直接覆盖就行）
，然后在文件夹中建立镜像
```Shell
docker build -t smplx/smplify-x:v1 .
```
整个过程耗时很长，请耐心等待

完成之后在建立容器：
```Shell
docker run -it --runtime=nvidia -P smplx/smplify-x:v1
```
之后再进入容器，在/home中即可看到smplify-x的工程文件，进入后运行
```
python3 smplifyx/easy_run.py
```
即可完成demo

## 关于SSH
为了方便调试，dockerfile中加入了安装ssh并设置远程登陆的内容，适用于使用服务器的小伙伴，如果不需要可以删除

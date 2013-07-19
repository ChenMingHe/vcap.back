vcap
====


Cloud Foundry源码，因为官方已经开始放弃Chef的安装部署方式，但是BOSH一直觉得太难，尤其对于没有IaaS平台的大家而言，BOSH简直就是一个噩梦，
所以将所有官方的源码同步下来，便于自己开发。

首先，Chef有一个安装脚本，可以参考网址：https://github.com/ChenMingHe/vcap/blob/master/dev_setup/bin/vcap_dev_setup
建议将这个脚本复制下来用，执行命令

$ gedit ~/setup

然后将网页中的内容复制、黏贴、并保存，然后修改权限，让其可以运行

$ sudo chmod +x ~/setup

在运行安装脚本前，需要先解决一些依赖项，这样安装过程基本上就非常快了，否则就会有各种诡异问题，首先需要解决依赖的库问题，执行命令

$ sudo apt-get install libncurses5 libncurses5-dev unixodbc unixodbc-dev libalien-wxwidgets-perl  freeglut3-dev libwxgtk2.8-dev xsltproc fop gcc-4.4 libssl0.9.8 ruby ruby-dev libopenssl-ruby rdoc ri irb build-essential ssl-cert rubygems

+++++++++++++++++++++++++++++++++++++++++++++++++++

接下来的操作是为了能够更快的部署Chef而做准备。

首先，准备安装过程中需要的安装包，这些包我已经全部上传上来了，通过网址查看：https://github.com/ChenMingHe/package

如果本地已经有这些安装包，则将这些包直接拷贝到本地的： /var/cache/dev_setup  目录下即可。如果没有，也可以通过命令获取：

$ git clone https://github.com/ChenMingHe/package.git 


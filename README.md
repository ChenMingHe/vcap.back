vcap单节点部署方案
======


Cloud Foundry源码，因为官方已经开始放弃Chef的安装部署方式，但是BOSH一直觉得太难，尤其对于没有IaaS平台的大家而言，BOSH简直就是一个噩梦，
所以将所有官方的源码同步下来，便于自己开发。

首先，Chef有一个安装脚本，可以参考网址：https://github.com/ChenMingHe/vcap/blob/master/dev_setup/bin/vcap_dev_setup
建议将这个脚本复制下来用，执行命令

    $ gedit ~/setup

然后将网页中的内容复制、黏贴、并保存，然后修改权限，让其可以运行

    $ sudo chmod +x ~/setup

在运行安装脚本前，需要先解决一些依赖项，这样安装过程基本上就非常快了，否则就会有各种诡异问题，首先需要解决依赖的库问题，执行命令

    $ sudo apt-get install libncurses5 libncurses5-dev unixodbc unixodbc-dev libalien-wxwidgets-perl  freeglut3-dev libwxgtk2.8-dev xsltproc fop gcc-4.4 libssl0.9.8 ruby ruby-dev libopenssl-ruby rdoc ri irb build-essential ssl-cert rubygems

可选步骤
------

接下来的操作是为了能够更快的部署Chef而做准备。

第一步，准备安装过程中需要的安装包，这些包我已经全部上传上来了，通过网址查看：     https://github.com/ChenMingHe/package

如果本地已经有这些安装包，则将这些包直接拷贝到本地的： /var/cache/dev_setup  目录下即可。如果没有，也可以通过命令获取：

    $ git clone https://github.com/ChenMingHe/package.git 

获取以后，根据https://github.com/ChenMingHe/package 中给的建议，将这些包放在相应的目录下即可。

第二步、我们是准备maven的库，因为Cloud Foundry的时候需要从Maven的中央库上下载大量的依赖库，个人感觉这个速度是非常的慢的，
所以我也将这部分的库全部弄出来了，对应网址就是https://github.com/ChenMingHe/cfrepo 获取相应的包的时候，在目录 ： ~/.m2/repository
 中执行命令：

    $ cd  ~/.m2/repository
    $ git clone https://github.com/ChenMingHe/cfrepo

通过这种方式，在编译过程中就少了大量下载Maven代码的过程。

第三步、准备Cloud Foundry中需要源码，因为Cloud Foundry的源码一直在更新，我不知道会不会有一天，Chef会不再支持这些源码，所以我
还是将这些源码准备下来了。如果本地有这些源码，在部署其他主机的时候，不妨就从中去获取，速度肯定比网上要快很多很多。
尤其是service的源码，现在Cloud Foundry的源码已经放在一个很深的目录中了，不太好找到。

    vcap : https://github.com/ChenMingHe/vcap
    cloud_controller : https://github.com/ChenMingHe/cloud_controller
    uaa : https://github.com/ChenMingHe/uaa
    stager : https://github.com/ChenMingHe/stager
    dea : https://github.com/ChenMingHe/dea
    router : https://github.com/ChenMingHe/router
    acm : https://github.com/ChenMingHe/acm
    services : https://github.com/ChenMingHe/services

(注：其实我也不知道这个源码能否继续用下去，因为我总觉得一些重要的组件的源码我还没完全弄下来，如果有缺失，很可能某天就
不能再用了)

这些源码的话应该是这样的一个目录结构：

    ~/
     +- vcap 
     +- cloud_controller
     +- uaa
     +- stager  
     +- dea
     +- router
     +- acm
     +- services

第四步、更换一个好一点的gem源，因为国外的Gem源速度不行，下载起来会相当的慢，所以最好更换成国内的源。
建议使用国内的淘宝源，执行命令：

    $ gem sources --remove http://rubygems.org/
    $ gem sources --add http://ruby.taobao.org/
    $ gem sources --update

好了，如果能够做好这些步骤，那应该比官方的方式要快很多。

安装
-------

Chef的部署最简单，不像BOSH那样要一步步构建平台，所以只需要运行安装脚本就可以了

安装脚本默认在一个节点里面安装所有组件，我也建议这样做，以后如果想只开启某个组件，
只需要修改配置文件，将不需要的组件关闭即可。
执行命令：

    $ ~/setup

如果顺利的话，应该可以一次成功，中间可能会出现网络不行，结果安装过程报错的问题，如果是的话就重新执行安装脚本。
如果不是，可以上网查资料，我以前也做了一些笔记，大家可以参考：

    http://blog.csdn.net/wearenoth/article/details/8035968
    http://blog.csdn.net/wearenoth/article/details/8072799


我只能说，这东西部署起来，真心考验耐心，里面的问题一般都很诡异。如果需要查阅资料。最好上Google Group或者Github的Issue列表
中查，国内的基本上没什么用了。

最后，祝君顺利!!!!
----




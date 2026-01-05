+++
date = '2025-01-30T18:45:48+08:00'
draft = false
title = 'HEXO博客网站搭建'
+++

## 前言

在这学期期末做JAVA实训项目，去CSDN上查询相关资料的时候，我无意间看到了在文章资料底部，作者留下了自己的个人网站，当时打开之后就感觉好cool😎，就想着趁着寒假，也要做一个自己的博客网站。以下是我搭建网站时，通过观看不同的视频教程，文章教程总结而成的文章，希望帮助自己理解的同时也能帮助其他人搭建博客，如有问题欢迎在评论区指出:）

## 一.服务器与域名的购买与设置

### 服务器的设置

阿里云，腾讯云，百度云.......  [腾讯云 产业智变·云启未来 - 腾讯](https://cloud.tencent.com/)

![DB857267C6173C65DE9D52EBC26B063E](https://bu.dusays.com/2025/01/29/679a2f0bf1e15.png)

并记住登录系统的用户名与密码

![E30D31218F189B85744193155638B4E9](https://bu.dusays.com/2025/01/29/679a2f70db1d4.png)

### 域名的设置

首先需要对域名进行解析，进入控制台，点击域名注册

![A3563E054AE8DF1E1D69365F3FD28429](https://bu.dusays.com/2025/01/29/679a2f889041b.png)

在“我的域名”导航栏中，点击解析

![99C38D93E61D211E5131FFE18561BF1A](https://bu.dusays.com/2025/01/29/679a2f9626d65.png)

按照如下勾选进行解析，网站IP填写服务器的外网IP，到此解析成功 :)

![F0D27EAC04C950F6DA67FA2A022A2AF6](https://bu.dusays.com/2025/01/29/679a2fa164fe5.png)

### 域名SSL证书申请

在控制台中搜索SSL证书，申请免费证书

![3D7FCFE74018E91A77416D653D0C3BFB](https://bu.dusays.com/2025/01/29/679a2fb2bee5c.png)

申请完毕之后选择下载，并下载此项证书，后面会用到pem文件和key文件

![6498BB1A22D62697E44AFC42291EE8E1](https://bu.dusays.com/2025/01/29/679a2fbe8b715.png)

## 二、安装Xshell与Xftp

[家庭/学校免费 - NetSarang Website](https://www.xshell.com/zh/free-for-home-school/)   名称随便填，主机选择服务器外网ip,Xftp的连接方式类似

![0F45FF65BA98A78A2C60E83F926EBE06](https://bu.dusays.com/2025/01/29/679a2fca67a09.png)

## 三、宝塔面板的安装与配置

### 安装宝塔面板

在连接好的xshell中输入命令

![5EA38CE03E3514CC76F1ED2C69862584](https://bu.dusays.com/2025/01/29/679a2fd3b538f.png)

输入以下代码

```
wget -O install_panel.sh https://download.bt.cn/install/install_panel.sh && bash install_panel.sh ed8484bec
```

 将会得到以下信息

========================宝塔面板账户登录信息==========================

【云服务器】请在安全组放行 aaa 端口(具体端口看你自己的面板)
 外网面板地址: xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
 内网面板地址: xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
 username: xxx
 password: xxxxxxxxx

### 为宝塔面板放行aaa端口

进入服务器控制台，按照画线规则来添加一条规则,放行端口

![4757B917A79E090AE75CD20379D10887](https://bu.dusays.com/2025/01/29/679a2fded2fd1.png)

### 进入宝塔面板进行配置

在浏览器中输入外网面板网址进入宝塔面板,选择如下套件，等待安装

![0AB9E45D6D0C22A50725565025DAAEC6](https://bu.dusays.com/2025/01/29/679a2fe77fbee.png)

在宝塔面板中选择网站这一栏，并按照下图设置添加站点

![D63DC22363A265643716C96356369255](https://bu.dusays.com/2025/01/29/679a2ff413968.png)

点击SSL证书，此操作会用到之前在腾讯云申请的证书，用记事本打开下载好的key和pem文件，复制粘贴到其中

![9B0FC5159D3573252922755B9D93E60F](https://bu.dusays.com/2025/01/29/679a2fff1dc18.png)

## 四、将HEXO安装到服务器前的配置

在安装hexo之前，需要安装nodejs，git

![B0F4FFCDEA2876445C8FA5A0EC21ED1D](https://bu.dusays.com/2025/01/29/679a300cdcdbc.png)

### 安装nodsjs

[下载 | Node.js 中文网](https://nodejs.cn/download/)

![407C7AEA28F9751667A1F548046D1D75](https://bu.dusays.com/2025/01/29/679a30192e4ec.png)

打开之前下载的Xftp,按照xshell类似的方法进行服务器的连接,找到你的nodejs压缩包，双击它，进行传输，注意右边目录选择root

![00753718D73066026B255145CAFFC0BC](https://bu.dusays.com/2025/01/29/679a3023157d6.png)

传输完成之后打开xshell，连接服务器，在命令窗口中输入如下代码，进行解压操作

(注意这里的node-v22.13.0-linux-x64.tar.xz代表的是你自己下载的，可能与我的版本不同，可以自己更改)

```
tar -vxf node-v22.13.0-linux-x64.tar.xz   
```

接下来设置软链接，输入如下代码

```
ln -s ~/nodejs/bin/node /usr/local/bin/
```

```
ln -s ~/nodejs/bin/npm /usr/local/bin/
```

接下来验证是否安装成功,分别输入如下代码

```
node -v
```

```
npm -v
```

出现版本号代表安装成功

![A386602506A040DE0ACBCD21915C64CB](https://bu.dusays.com/2025/01/29/679a303118f92.png)

接下来更换npm源，官方的源下载速度很慢，可以用国内的源，输入如下代码

```
npm config set registry https://registry.npmmirror.com
```

### 安装git

安装前在xshell中输入git -v来检验是否有git，如果没有再进行以下步骤

首先更新一下软件包(适用于debian和unbantu)

```
apt-get update
```

安装git

```
apt-get install git
```

安装hexo脚手架，并设置软连接，依次输入以下代码

```
ln -s ~/nodejs/bin/hexo /usr/local/bin/
```

```
hexo -v
```

### 创建blog文件夹

之后打开xftp，连接上自己的服务器，在箭头指向的框中输入/，进入到root的上一级目录，并创建一个名为blog的文件夹

![59FBEAE4BF1F242E3F21CBCE867B0061](https://bu.dusays.com/2025/01/29/679a303edf453.png)

## 五、vscode的安装与使用

### 安装vscode与相应的插件

[Visual Studio Code - Code Editing. Redefined](https://code.visualstudio.com/)   在拓展中搜索SSH，安装Remote-SSH（为了远程连接我们的服务器，方便管理）

![8B7E79858BA2A093F91A1354CC085EC9](https://bu.dusays.com/2025/01/29/679a304b7d693.png)

### 获得ssh公钥和密钥

点击win+r键，输入cmd，打开命令行

![34EF7B0CD6ABBD7B17FD84F08E13A1EF](https://bu.dusays.com/2025/01/29/679a3053a39c3.png)

在命令行中输入如下代码，一路回车，获得本机的ssh公钥和密钥

```
ssh-keygen -t rsa
```

接着在电脑的这个目录下面就会生成两个文件（后面会用到id_rsa.pub文件）

![65399BE5C2F34962EE72F375989D9F6C](https://bu.dusays.com/2025/01/29/679a305c6c2d6.png)

接着打开xshell，连接服务器，同样输入上述代码，一路回车

之后打开xftp，在框中输入/root/.ssh点击回车，进入.ssh文件夹

![8A69F044FDEA5F1BD74BD945F5371EBD](https://bu.dusays.com/2025/01/29/679a30660cdf9.png)

把之前在电脑上生成的id_rsa_pub文件用记事本打开，复制里面的文本，之后右键authorized_keys文件，选择用记事本编辑，粘贴复制的文本

![6D3BB6AE4EE3DDD60A1979204D5730E4](https://bu.dusays.com/2025/01/29/679a306d3d2f8.png)

### 用vscode连接服务器

按照下图进行操作

![C27B71D3324A52CDE6BA9B12B4081124](https://bu.dusays.com/2025/01/29/679a30797a204.png)

![08CE15A2697F95F54F03A86C993E68C2](https://bu.dusays.com/2025/01/29/679a308233415.png)

![DA8825DE0CE40F79FC0870DBB7141456](https://bu.dusays.com/2025/01/29/679a30895d4a1.png)

在配置文件中加入一行 IdentityFile, 后面的路径选择之前在电脑上生成ssh密钥的路径，填写完毕之后按ctrl+s保存

![A6B1E3C95C5CA6AD009CB9059BED2EA0](https://bu.dusays.com/2025/01/29/679a3092e58f6.png)

接着连接服务器，并打开blog文件夹

![3463833467DD0FEDACC9FACE62D0FBB1](https://bu.dusays.com/2025/01/29/679a309b8a5ad.png)

接着在终端中输入hexo init到此结束，连接完毕！

![E65032962D33A6CB5BBE7D257A9A0953](https://bu.dusays.com/2025/01/29/679a30a737cc8.png)

在终端中输入

```
hexo cl
hexo g
hexo s
```

并打开给出的网址，即可查看是否安装成功

### 主题安装与使用(anzhiyu)

参考[安知鱼主题官方文档 | 一个简洁、美丽的静态hexo主题](https://docs.anheyu.com/)

## 六、修改网站目录和运行目录

打开宝塔面板

接着进入自己的网址，即可看到安装成功！![3E6A0C15C6AD92CA146091A5C6C59624](https://bu.dusays.com/2025/01/29/679a30b6dedd3.png)

![6D3B44B4D7EECADDF3DD62DA53906FEB](https://bu.dusays.com/2025/01/29/679a30c925c91.png)
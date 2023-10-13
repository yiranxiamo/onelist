# onelist
一个类似emby的专注于刮削alist聚合网盘形成影视媒体库的程序。

![](./docs/imgs/01.png)

### 主要解决以下痛点：

* alist挂载云盘后能在网页端看视频，却没有分类，没有海报墙

* 使用webdav挂载本地后，用jellyfin或者emby刮削会下载视频截取封面导致封号

* 用jellyfin或者emby之类，没有大带宽公网ip，在外难以访问

### 常见问题汇总：
* 比如你的alist是这样"[https://pan.alist.com/阿里云盘/电影](https://pan.alist.com/阿里云盘/电影)"，你在新建alist类型影库时候域名应该输入"https://pan.alist.com",不要有多余字符，在这个影库下挂载电影目录时候输入"/阿里云盘/电影"
* 刮削成功无法播放，先确认alist使用最新版，且需要alist后台关闭"签名所有功能"，还有要确认是否是浏览器不支持的编码，这种可以调用外部浏览器播放


### 多种安装方式，推荐docker安装：

---
[docker安装](./docs/docker_install.md) | [docker-compose方式安装](./docs/docker_conpose_install.md)

---

手动安装教程：https://www.bilibili.com/video/BV15M41177LN
## 1.程序下载
可以在github发布页下载已经编译好的二进制文件

使用前必看，程序采用themoviedb作为刮削的资源库，推荐使用国外主机，否则你需要修改hosts文件。
```
99.84.251.12 api.themoviedb.org
99.84.251.19 api.themoviedb.org
99.84.251.67 api.themoviedb.org
99.84.251.108 api.themoviedb.org
156.146.56.162 image.tmdb.org
108.138.246.49 image.tmdb.org
```
## 2.下载后先初始化配置文件

输入`./onelist -run config`命令,便会生成配置文件config.env
修改完config.env配置文件后,运行`onelist -run server`便可启动项目,运行`onelist -run admin`可查看管理员账户!

config.env
```
# 服务设置
# 注意要改为未被占用的端口
API_PORT=5245
FaviconicoUrl=https://wework.qpic.cn/wwpic/818353_fizV30xbQCGPQRP_1677394564/0
API_SECRET=fRVvjcNd11gYGI85StVaeCtPVSmJTRRE

# Env有两种模式，Debug及Release，主要用在数据库为mysql时候，需要注意修改Env环境和mysql密码对应
Env=Debug

# 管理员账户设置，用于初始化管理员账户
UserEmail=xxxx.@qq.com
UserPassword=xxxxx

# 数据库设置
DB_DRIVER=sqlite
DB_USER=root
DbName=onelist

# 如果上面DB_DRIVER类型为mysql，就需要正确填下以下参数
DB_PASSWORD_Debug=123456
DB_PASSWORD_Release=123456

# TheMovieDb Key
# 在https://www.themoviedb.org网站申请
KeyDb=22f10ca52f109158ac7fe064ebbcf697
```
## 3.运行程序

```
# 先运行，查看有无错误
./onelist -run server

注意：如果提示权限问题，可以先授权文件chmod 777 onelist

# 如果想后台一直保持运行，可用以下命令
nohup ./onelist -run server >/dev/null 2>&1 &
```
## 4.登录
访问你的`ip:端口`就可以进入管理后台了(记得防火墙放行该端口)
## 5.添加媒体库
![](./docs/imgs/02.png)

1.对应输入媒体库名字，比如电影，类型选择movie

2.封面图片可以暂时不填

3.填写alist相关信息，这个主要用于程序查询你alist中文件，根据文件名进行刮削

## 6.挂载资源，新建完毕后，添加挂载目录。
![](./docs/images/03.png)

挂载的目录中文件必须满足下面这种命名方式
```
电影就按电影名称

电视同一部美剧，所有季可以分开或者放在不同子目录，但是文件名一定得满足以下格式
权力的游戏S01E01.mp4
权力的游戏S01E02.mp4
权力的游戏S01E03.mp4
```
填写比如`/阿里2号/电影01组`即可，可以选择是否自动刮削，用于你网盘有新文件，程序自动给你添加进影库,

点击创建后反应比较慢，是因为程序去遍历你的alist文件了，稍微等下

> 注意：添加挂载目录只能选择你建立媒体库中采用的alist相关目录，要与alist域名一致
>
## 7.创建后点击刷新就可以看到刮削进度了，有需要的请在hosts内添加以下内容
13.224.161.90 api.themoviedb.org
104.16.61.155 image.themoviedb.org
13.35.67.86 api.themoviedb.org
54.192.151.79 www.themoviedb.org
13.225.89.239 api.thetvdb.com
13.249.175.212 api.thetvdb.com
13.35.161.120 api.thetvdb.com
13.226.238.76 api.themoviedb.org
13.35.7.102 api.themoviedb.org
13.225.103.26 api.themoviedb.org
13.226.191.85 api.themoviedb.org
13.225.103.110 api.themoviedb.org
52.85.79.89 api.themoviedb.org
13.225.41.40 api.themoviedb.org
13.226.251.88 api.themoviedb.org

可以进入错误文件中查看
### 交流群：
> 群名称：
onelist
> QQ群   号：
765592050


<span><small>感谢您的关注！开源不易，需要开发者们的不断努力和付出。如果您觉得我的项目对您有所帮助，希望能够支持我继续改进和维护这个项目，您可以考虑打赏我一杯咖啡的钱。
您的支持将是我继续前进的动力，让我能够更加专注地投入到开源社区中，让我的项目变得更加完善和有用。如果您决定打赏我，可以通过以下方式：</small></span>
<ul>
    <li>给该项目点赞 &nbsp;<a style="vertical-align: text-bottom;" href="https://github.com/msterzhang/onelist">
      <img src="https://img.shields.io/github/stars/msterzhang/onelist?style=social" alt="给该项目点赞" />
    </a></li>
    <li>关注我的 Github &nbsp;<a style="vertical-align: text-bottom;"  href="https://github.com/msterzhang/onelist">
      <img src="https://img.shields.io/github/followers/msterzhang?style=social" alt="关注我的 Github" />
    </a></li>
</ul>
<table>
    <thead><tr>
        <th>微信</th>
        <th>支付宝</th>
    </tr></thead>
    <tbody><tr>
        <td><img style="max-width: 150px" src="./docs/imgs/wx.png" alt="微信" /></td>
        <td><img style="max-width: 150px" src="./docs/imgs/zfb.jpg" alt="支付宝" /></td>
    </tr></tbody>
</table>

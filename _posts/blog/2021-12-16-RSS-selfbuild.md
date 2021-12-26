---
layout: post
title: 信息茧房脱出-自建RSS
date: 2021-12-15
author: Anduin9527
categorise: 折腾
tags : RSS 教程 
permalink: /blog/2021/RSS-selfbuild
---
RSS，也就是 Rich Summary Site 。这玩意儿有点时代的眼泪的感觉了。在推荐算法大行其道的当下，RSS本身是一种逆潮流的选择。加之国区对于RSS应用的监管力度之大致使很多优秀的RSS服务在国内被和谐。

我之前一直使用的是 feeder.co 无奈他的 IPAD 应用不仅要 Dollar，还锁了国区。所以选择折腾一手，自建RSS。

<!--more-->

<img src="https://imgbed-1304793179.cos.ap-nanjing.myqcloud.com/typora/20211216172339.jpeg" alt="img" style="zoom:67%;" />



## Miniflux

[Miniflux](https://miniflux.app/) 是一个免费开源的RSS聚合源，与另一个开源的 [TTRSS](https://tt-rss.org/) 相比，它的极简设计风格，深的我心（虽然默认UI都差不多丑）。

Miniflux 是基于 `GO` 编写的，数据库选择的是 `Postgresql`，不依赖其他的 ORM 以及框架。

### 部署

如果你没有 Docker 以及 Docker-compose，请立即安装并学习。

[Docker 从入门到实践](https://vuepress.mirror.docker-practice.com/)

1. 新建一个 miniflux 目录

```bash
mskdir ~/miniflux && cd ~/miniflux
```

2. 创建并修改 `docker-compose.yml`

```yaml
version: '3'
services:
  miniflux:
    image: miniflux/miniflux:latest
    ports:
      - "<端口>:8080"
    depends_on:
      - db
    environment:
      - DATABASE_URL=postgres://miniflux:<数据库密码>@db/miniflux?sslmode=disable
      - RUN_MIGRATIONS=1
      - CREATE_ADMIN=1
      - ADMIN_USERNAME=<Miniflux管理员用户名>
      - ADMIN_PASSWORD=<Miniflux管理员密码>
  db:
    image: postgres:latest
    environment:
      - POSTGRES_USER=miniflux
      - POSTGRES_PASSWORD=<数据库密码>
    volumes:
      - miniflux-db:/var/lib/postgresql/data
volumes:
  miniflux-db: 
```

+ 自行修改上述带有`<>`的选项

3. 启动 Miniflux

```bash
docker-compose up -d
```

访问 `localhost:<端口>` 进入 Miniflux 的管理页面说明大成功，然后就可以开启相应的防火墙，让外网也可以访问。

## RssHub

Miniflux 充当的角色是个**聚合的订阅源**，那么源本身从哪里来呢？别人整合的固然方便，但是自定义程度肯定不如自己来得爽。但是有些网站或者博客根本没有做 RSS 订阅（<del>比如我</del>）

>RSSHub 是一个开源、简单易用、易于扩展的 RSS 生成器，可以给任何奇奇怪怪的内容生成 RSS 订阅源。RSSHub 借助于开源社区的力量快速发展中，目前已适配数百家网站的上千项内容
>
>可以配合浏览器扩展 [RSSHub Radar (opens new window)](https://github.com/DIYgod/RSSHub-Radar)和 移动端辅助 App [RSSBud (opens new window)](https://github.com/Cay-Zhang/RSSBud)(iOS) 与 [RSSAid (opens new window)](https://github.com/LeetaoGoooo/RSSAid)(Android) 食用

### 使用

最常用的场景就是下载一个浏览器插件，他会自动嗅探当前网页，如果有符合的路由规则（来自于开源社区的支持），他会自动帮你生成一个 RSS 源，同时支持一键导入到你的聚合源（在设置界面中添加Miniflux的地址）。

<img src="https://imgbed-1304793179.cos.ap-nanjing.myqcloud.com/typora/20211216165507.png" alt="image-20211216165506944" style="zoom:67%;" />

### 部署

RSSHub默认可以使用官方提供的服务器服务，但出于反爬以及稳定性的考量，还是建议我们选择自建服务。

<del>如果你没有Docker以及Docker-compose，请立即安装并学习。</del>

运行下面的命令下载 RSSHub 镜像

```bash
$ docker pull diygod/rsshub
```

然后运行

```bash
$ docker run -d --name rsshub -p 1200:1200 diygod/rsshub
```

### 添加配置

配置运行在 docker 中的 RSSHub，最便利的方法是使用 docker 环境变量

以设置缓存时间为 1 小时举例，只需要在运行时增加参数：`-e CACHE_EXPIRE=3600`

```bash
$ docker run -d --name rsshub -p 1200:1200 -e CACHE_EXPIRE=3600 
```

更多配置项请看 [官方文档](https://docs.rsshub.app/install/#pei-zhi)

### 使用

同样的，在部署成功之后访问对应的地址。（记得打开防火墙）

然后就可以在 RSSHub Rader 等的设置页面，使用自定义 RSSHub域名

## 阅读器推荐

说了这么多，总得来点读的，考虑到我的使用场景，所以没有找IOS或者Android的阅读器。

### win10&win11

推荐国人大佬 云之幻 制作的[RSS追踪](https://www.microsoft.com/zh-cn/p/rss-%E8%BF%BD%E8%B8%AA/9n85pv1rjd6v)，界面充分体现了UWP应用一贯的极简且平滑的设计理念👍。

>集成多种主流RSS服务的原生UWP阅读器，通过在线服务，你可以实现多端同步。经过全新设计的UI与强化后的功能，是Windows端一个不错的RSS阅读选择

<img src="https://imgbed-1304793179.cos.ap-nanjing.myqcloud.com/typora/20211216170732.jpeg" alt="img" style="zoom:67%;" />

这里选择Fever模式

进入Miniflux的后台，在设置中打开Fever插件，设置用户名密码后。即可用 `http://IP:minifluxport/fever/` 的方式导入

<img src="https://imgbed-1304793179.cos.ap-nanjing.myqcloud.com/typora/20211216171232.png" alt="image-20211216171231808" style="zoom:67%;" />

总之就是清爽😎

### ipadOS

APPStore 个人觉得最好用的 Feeder 5 已经从国区下架了，国人团队做的 Ego Reader 体验也不错。可惜横屏适配问题一直没有解决。

<img src="https://imgbed-1304793179.cos.ap-nanjing.myqcloud.com/typora/20211216172758.jpg" alt="img" style="zoom:67%;" />



## 参考

[Miniflux](https://miniflux.app/)

[RSSHub](https://docs.rsshub.app/)

[利用 Miniflux 自建 RSS](https://hydrotho.github.io/Miniflux-Build-Guide/)








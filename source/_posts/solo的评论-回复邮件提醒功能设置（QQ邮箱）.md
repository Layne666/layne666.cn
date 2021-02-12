---
title: Solo的评论/回复邮件提醒功能设置（QQ邮箱）
copyright_author_href: https://layne666.cn
cover: https://bed.layne666.cn/images/2021/02/12/ed40945b4deeedf4f6ae6f4979fec45f.png
date: 2019-01-01 22:29:41
updated: 2019-02-08 17:19:25
categories: 
  - Solo
tags: 
  - Solo
---

话说我今天看到solo系统有**评论/回复邮件提醒**功能，然后我自己尝试回复一下我小号发的评论，评论是回复成功了，但是邮件没发出去！

然后我就去找solo的[用户指南](https://hacpai.com/article/1492881378588)，发现里面好像没有写怎么配置，所以自己琢磨弄了半天（没办法，我很菜），终于弄好了，所以记录在这里分享给大家。
首先，我先去github上把项目克隆到本地（需要JDK8或以上的版本，Tomcat版本至少是9），导入Eclipse中，并且把**mail.properties**进行如下的配置。

![e048d546a9e9a8048afa9c993ff5fad5.png](https://bed.layne666.cn/images/2021/02/12/e048d546a9e9a8048afa9c993ff5fad5.png)

user是QQ邮箱，密码我一开始以为就是QQ密码 😂
其实并不是，是授权码。

现在，需要登录QQ邮箱，在设置—>账号中开启smtp服务，然后生成授权码，把授权码填入到mail.properties的password。

![a2b320ec4ba935c5419ff6984b527c02.png](https://bed.layne666.cn/images/2021/02/12/a2b320ec4ba935c5419ff6984b527c02.png)

![dcf09f32612aa578030cfc3ab400d201.png](https://bed.layne666.cn/images/2021/02/12/dcf09f32612aa578030cfc3ab400d201.png) 

我把这些配置完之后就开始跑项目了，发现邮件还是没发出去，控制台出现报错信息。

![ce8b98a29c5ad0b0c08eda9b550eeb14.png](https://bed.layne666.cn/images/2021/02/12/ce8b98a29c5ad0b0c08eda9b550eeb14.png)

没办法，出现报错信息，只能调试看看了！别说，我还真发现点东西。

![e806e58d6964da7c23ad733fe934aeaf.png](https://bed.layne666.cn/images/2021/02/12/e806e58d6964da7c23ad733fe934aeaf.png) 

![72fe17f27edc4d7af8dfff7bf1429c5e.png](https://bed.layne666.cn/images/2021/02/12/72fe17f27edc4d7af8dfff7bf1429c5e.png) 

![46fa507fa62a8b25a7f3190cb31603b9.png](https://bed.layne666.cn/images/2021/02/12/46fa507fa62a8b25a7f3190cb31603b9.png)

好像是adminEmail和mail.properties里面的user邮箱设置的不一致，然后就会报这个错！
我的adminEmail里面的值是layne666@ solo.b3log.org，这应该是b3log给的默认邮箱，所以我寻思着能不能把这个改成我的QQ邮箱。

我查数据库发现，**表b3_solo_option**里面有这个值的设置，二话不说，改成我的QQ邮箱再说

![c083d8f08ef2ae26dd9cf9063fbe8e5e.png](https://bed.layne666.cn/images/2021/02/12/c083d8f08ef2ae26dd9cf9063fbe8e5e.png) 

![b544b3195cf0d535de92be89bd94b396.png](https://bed.layne666.cn/images/2021/02/12/b544b3195cf0d535de92be89bd94b396.png)


改完之后，重新跑一下项目。然后我回复评论，回复成功了，邮件也发出去了，小号成功收到邮件。

![ed40945b4deeedf4f6ae6f4979fec45f.png](https://bed.layne666.cn/images/2021/02/12/ed40945b4deeedf4f6ae6f4979fec45f.png)

到此算是暂告一段落了！

![4bead1db7b132f22f57b2ca752fae778.gif](https://bed.layne666.cn/images/2021/02/12/4bead1db7b132f22f57b2ca752fae778.gif)

讲道理，能看到[Solo](https://github.com/b3log/solo)的源码，真得很棒，很值得学习，感谢D大，感谢为Solo贡献的所有人！💖
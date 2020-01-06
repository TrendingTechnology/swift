+++
author = ""
date = 2020-01-05T16:00:00Z
description = "默认设置下netlify使用的是保守设置，不会使用最新版本的去和雨果来构建网站。可以增加两个环境变量来覆盖netlify的默认设置："
featuredimage = "https://res.cloudinary.com/diqqalzsx/image/upload/v1578297638/static/swift/Learning_Disabilities_wcees9.jpg"
tags = []
title = "在netlify使用最新版本的hugo和go建立网站"

+++
如果你使用[雨果](https://gohugo.io/)构建网站，那么一定知道雨果最近新发布了[v0.60版本](https://github.com/gohugoio/hugo/releases/tag/v0.60.0)  
雨果v0.60开始，更换了默认的降价渲染内核，使用更快的[戈德马克](https://github.com/yuin/goldmark/)。  
默认设置下netlify使用的是保守设置，不会使用最新版本的去和雨果来构建网站。  
可以增加两个环境变量来覆盖netlify的默认设置：

|  |  |
| --- | --- |
| HUGO_VERSION | 0.60.0 |
| GO_VERSION | 1.13.4 |

[![](https://lvv.me/posts/2019/11/29_newest_hugo_and_go_version_on_netlify/01.png)](https://lvv.me/posts/2019/11/29_newest_hugo_and_go_version_on_netlify/01.png)
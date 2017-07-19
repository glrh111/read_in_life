# Read In Life 项目

## 项目综述
本项目为一个博客系统. 用户可以发表文章并评论;可以通过私信交流. 

客户端支持: weapp端和普通浏览器端

后台API相关:API框架基于tornado开发, 前期业务逻辑使用python实现.

> 曾宴桃源深洞，一曲舞歌鸾凤。尝记别伊时，和泪出门相送。如梦如梦，残月落花烟重。--后唐李存勖

本项目包含服务如下:
* Postgres数据库服务
* Redis服务
* API服务
* 后台管理服务(待开发)
* nginx服务
* IM聊天服务(待开发, 希望使用Golang开发)
* elastic搜索服务(待开发)
* 队列服务(待开发)

全部服务使用docker管理.

## 项目内容
+ [API代码](https://github.com/glrh111/read_in_life_api) (已上线, 参见 [API实例](http://glrh11.com/ping/ping))
+ IM相关代码
+ [weapp小程序代码](https://github.com/glrh111/read_in_life_weapp) (v0.1已经提审,但一直没通过,现准备置之不理)
+ [前端代码](https://github.com/glrh111/read_in_life_web)(已上线, 参见 [风雨穿行](https://glrh11.com))
+ [服务部署相关](https://github.com/glrh111/read_in_life/tree/master/deployment)
+ 搜索服务elastic实现(正在开发)



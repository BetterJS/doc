##介绍

>BadJS 是 web 前端脚本错误监控及跟踪解决方案。此项目为鹅厂 [imweb](http://imweb.io/) 团队的开源项目。


**项目亮点**

1. 一站式体系化解决方案：业务只需要简单的配置，引入上报文件，即可实现脚本错误上报，每日统计邮件跟踪方便。
2. 可视化查询系统，快速定位错误信息：web应用程序脚本数量庞大，开发人员在如此之多的脚本中定位某个问题变得困难。BadJS能够巧妙定位错误脚本代码，进行反馈。通过各种查询条件，快速找到详细错误日志。
3. 跨域、Script Error等棘手问题不再是难题：tryjs帮你发现一切。
4. 真实用户体验监控与分析：通过浏览器端真实用户行为与体验数据监控，为您提供JavaScript、AJAX请求错误诊断和页面加载深度分析帮助开发人员深入定位每一个问题细节。即使没有用户投诉，依然能发现隐蔽bug，主动提升用户体验。
5. 用户行为分析：细粒度追踪真实的用户行为操作及流程，前端崩溃、加载缓慢及错误问题，可关联到后端进行深度诊断。
6. 产品质量的保障：浏览器百花齐放，用户环境复杂，巨大的差异导致开发人员难以重现用户遇到的问题。无法像后台一样上报所有用户操作日志。通过BadJS，上报用户端脚本错误，为产品质量保驾护航。

##系统架构


![qq 20150925214633](https://cloud.githubusercontent.com/assets/2292731/10102147/6720c4e4-63cf-11e5-8ae5-0aac7c89a91b.png)

**前端**

badjs-report - 前端错误监控工具
<br/>

**后端**


badjs 系统使用面向服务的体系架构，各个模块介绍如下

badjs-acceptor - 接入层，使用多进程处理

badjs-mq - 消息队列中心，用于分发给其他系统

badjs-storage - 存储服务，存入mongodb ，并提供查询日志和统计日志的服务
> 默认使用mongodb 进行存储

badjs-web - 管理系统，提供用户管理、日志查询和日志统计
> badjs-web/db/create.sql 初始化数据库

badjs-openapi - 方便整合现有的第三方系统，例如实时统计和告警系统
> 可以不安装

配置(project.json)说明
> 所有"project.debug.json"为本地调试配置,用于区分"开发环境"和"生产环境"，运行时候可以添加参数 --debug(debug 日志输出) --project(使用测试配置)



##安装要求
nodejs 12.0+

zmq 3.0+ 
> zmq 安装为  [#1 ](https://github.com/BetterJS/doc/issues/1)

mysql 5.0+

mongodb 3.0+

pyton 2.7+

## 如何部署

1. 安装前面提到的必要环境
2. 下载各个模块
  - git clone https://github.com/BetterJS/badjs-accepter.git
  - git clone https://github.com/BetterJS/badjs-mq.git
  - git clone https://github.com/BetterJS/badjs-storage.git
  - git clone https://github.com/BetterJS/badjs-web.git
  - git clone https://github.com/BetterJS/badjs-openapi.git
3. 进入各个模块npm install 
4. 进入 badjs-acceptor 目录， 运行命令 `` node app.js --debug --project `` ，运行成功看到下面的提示:
``` cmd
start badjs-acceptor success. 
```
5.接着进入 badjs-storage , 通过 project.debug.json 文件配置你的mongodb地址 接着运行  `` node app.js --debug --project ``，成功看到下面提示:
``` cmd
start badjs-storage success.
```
6. 接着进入badjs-web 目录, 通过 project.debug.json 文件配置你的mysql地址，然后删除oos 配置， 接着运行  `` node app.js --debug --project`` ,成功看到下面提示：
``` cmd 
start badjs-web , listen 8081
```
7. 最后进入其他剩下的模块，依次运行 `` node app.js --debug --project``
8. 访问 http://127.0.0.1:8081/index.html ，进入页面确定启动成功。
9. 线上环境配置，请访问各个模块的页面，查看配置说明。


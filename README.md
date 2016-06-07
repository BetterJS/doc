[![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/BetterJS?utm_source=share-link&utm_medium=link&utm_campaign=share-link)

##介绍
>BadJS 是 web 前端脚本错误监控及跟踪解决方案。此项目为鹅厂 [imweb](http://imweb.io/)（qq群:179045421） 团队的开源项目。




**项目亮点**

1. 一站式体系化解决方案：业务只需要简单的配置，引入上报文件，即可实现脚本错误上报，每日统计邮件跟踪方便。
2. 可视化查询系统，快速定位错误信息：web应用程序脚本数量庞大，开发人员在如此之多的脚本中定位某个问题变得困难。BadJS能够巧妙定位错误脚本代码，进行反馈。通过各种查询条件，快速找到详细错误日志。
3. 跨域、Script Error等棘手问题不再是难题：tryjs帮你发现一切。
4. 真实用户体验监控与分析：通过浏览器端真实用户行为与体验数据监控，为您提供JavaScript、AJAX请求错误诊断和页面加载深度分析帮助开发人员深入定位每一个问题细节。即使没有用户投诉，依然能发现隐蔽bug，主动提升用户体验。
5. 用户行为分析：细粒度追踪真实的用户行为操作及流程，前端崩溃、加载缓慢及错误问题，可关联到后端进行深度诊断。
6. 产品质量的保障：浏览器百花齐放，用户环境复杂，巨大的差异导致开发人员难以重现用户遇到的问题。无法像后台一样上报所有用户操作日志。通过BadJS，上报用户端脚本错误，为产品质量保驾护航。

##系统架构

![image](https://cloud.githubusercontent.com/assets/2292731/12427248/28530902-bf19-11e5-9884-551dc9442326.png)


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


**类库** 

badjs-openapi-client - 连接 badjs-mq 的客户端的类库
> 一般用于接收数据后并处理后，转发给第三方系统

配置(project.json)说明
> 所有"project.debug.json"为本地调试配置,用于区分"开发环境"和"生产环境"，运行时候可以添加参数 --debug(debug 日志输出) --project(使用测试配置)



##安装要求
nodejs 0.12+

mysql 5.0+

mongodb 3.0+

pyton 2.7.x

git 命令，用于拉取各个系统模块

## 部署
#### 单机环境部署
1. 安装前面提到的必要环境
2. git clone https://github.com/BetterJS/badjs-installer.git
3. 进入到badjs-installer的目录，运行 ```npm run clone``` ，拉取各个模块
4. 运行```npm run install``` ,安装依赖，**这个步骤很容易出现问题** ，对于新用户建议进入各个模块进行```npm install```
  - phantomjs 安装不成功，请查看  [#8 ](https://github.com/BetterJS/doc/issues/8) 
5. 进入badjs-web/db ，将里面的 create.sql 导入到 mysql中 
5. 运行 ```npm run start``` ，启动各个模块
6. 访问 http://127.0.0.1:8081/index.html ，进入页面确定启动成功。

#### 多机环境部署
1. 下载各个模块的稳定版本
  - https://codeload.github.com/BetterJS/badjs-acceptor/zip/v1.1.1
  - https://codeload.github.com/BetterJS/badjs-mq/zip/v1.1.1
  - https://codeload.github.com/BetterJS/badjs-web/zip/v1.3.0
  - https://codeload.github.com/BetterJS/badjs-storage/zip/v1.3.0
2. 线上环境配置，请访问各个模块的页面的配置说明：
  - https://github.com/BetterJS/badjs-acceptor/blob/master/Readme.md
  - https://github.com/BetterJS/badjs-web/blob/master/Readme.md
  - https://github.com/BetterJS/badjs-mq/blob/master/Readme.md
  - https://github.com/BetterJS/badjs-storage/blob/master/Readme.md
3. 用 forever 或 nohub 启动各个模块


##如何使用
1. 在 http://127.0.0.1:8081/index.html 上会有介绍。
2. 安装完成后，使用默认的超级帐号 admin/admin 进入
3. 登录成功后，点击右上角的“我的业务”进入管理界面，点击"申请业务"
4. 申请成功后，点击"管理" -> "申请列表" 对自己的业务进行审核通过。
5. 完成审核，系统会讲业务信息下发给badjs-accpeor , badjs-mq
  - 查看下发是否成功，可进入 badjs-acceptor 查看 project.db

**到这里，整个后台的部署已经成功了。接下来即可使用 badjs-report/example/index.html 进行测试验证上报。**


## 怎么上报
1. 关于上报的任何问题，可以点击下面的链接进行查看
  - [report 介绍](https://github.com/BetterJS/badjs-report)
  - [report 问题列表](https://github.com/BetterJS/badjs-report/issues)
  
  
## 百万PV 优化  
  - 参见 [#15 ](https://github.com/BetterJS/doc/issues/15) 

##谁在用

![ke.qq.com](https://cloud.githubusercontent.com/assets/2292731/10385573/5d4c5114-6e7d-11e5-9aed-21c36453c9ee.png)

![mail.qq.com](https://res.mail.qq.com/zh_CN/htmledition/images/webp/logo/qqmail/qqmail_logo_default_35h206ff1.png)

![image](https://cloud.githubusercontent.com/assets/2292731/10385585/87e76fda-6e7d-11e5-9e33-655d8849ae21.png)

![image](https://cloud.githubusercontent.com/assets/2292731/10385601/dc15d9ac-6e7d-11e5-82f5-10d984126df6.png)

![qun.qq.com](http://qplus3.idqqimg.com/qun/portal/img/logo2.png)

![image](https://cloud.githubusercontent.com/assets/2292731/10385625/2f0bc0ae-6e7e-11e5-871b-28d020e4e326.png)

![image](https://cloud.githubusercontent.com/assets/2292731/10385652/9277ced0-6e7e-11e5-8d05-c5fafbb095b9.png)

![image](https://cloud.githubusercontent.com/assets/2292731/12528051/eb5f622a-c1c5-11e5-9716-d3f75d93668b.png)


## 更新日志
##### v1.7
  - storage 模块采用实时统计
  - axon 替换 zmq 
  
#####  v1.6
  - oa 登录模块的抽取
  - UI 调整
  - bugfix
  
##### v1.5
  - oa 登录模块的抽取
  - UI 调整
  
##### v1.4
  - 千万PV级别优化
  - 增加 openapi 
  - bugfix
  
##### v1.3
  - mq 模块抽取
  - 限制上报规则
  - 增加实时日志
  - 上报模块的优化

##### v1.2
  - 统计功能优化
  - 增加图标展示
  - bugfix
  - 增加项目审批功能
  - 上报模块的优化
  
#####  v1.1
  - 增加邮件功能
  - 增加统计功能
  
#####  v1.0
  - 项目上线
  - 上报功能
  - 历史日志查看

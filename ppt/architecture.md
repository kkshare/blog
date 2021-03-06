title: 分布式系统架构经验总结
speaker: kk
url: https://kkshare.github.io
transition: slide3
theme: dark

[slide]

# 分布式系统架构经验总结
<small>2016-06-15 何通庆</small>

[主页](https://kkshare.github.io)

[slide]
# Facebook的五条管理技术团队的经验
- 招聘很紧急，而且要找牛人
- 流程由实践者确立
- 内部晋升，不找空降的管理人员
- 开发工具代替人力低效劳动
- 技术领导，不要外行指挥内行。

[note]
facebook：让亲身实践者执行工作流程
 * 个人制定并执行的工作流程，会针对真实工作的情况进行更多优化调整。
管理者设计的工作流程，最多能接近实际工作流程，它需要管理、优化或整理。
这是许多愚蠢、低效的工作流程的来源。
 * 在人们亲自制定工作流程时，会感到更大的自主权。
在今后，随着情况不可避免地变化，也就更有权视情况对其调整，而不是任其僵化。
外部强加的（自上而下的）工作流程更加难以打破，而且往往会被神化，从而产生非常大的组织惯性。
[/note]

[slide]
# 利用开源项目
- 资源: codeplex, google code, sourceforge,  
  github.com www.open-open.com
- 直接使用:tomcat,mysql,redis
- 间接使用:使用部分组件、代码或仅参考设计思路
- 改造使用:改配置，增加代理，改源码(如何改造？)
 * 使用工具是为了解决问题，带着问题不偏离方向
 * 带着问题能够激发好奇与兴趣，使责任与兴趣统一
 * 查看源码：源码之下藏不住真相
 * 分解问题：小问题容易完成，有成就感，持续动力
 * 优缺点同时关注，同类产品对比 ehcache/memcache/redis
 * 突破点：运行起来

[slide]
# 何时不用开源项目
- 反思为何使用开源
 * 为了赶时髦？为了技术而技术？
 * 为了技术还是解决问题？
- 优缺点同时关注，对比
 * 没有项目会否定自己
- 开源项目通常会考虑通用性
 * 增加性能损耗
 * 增加学习成本

[slide]
# 为何不用spring
- AOP(分层架构)
 * 为了降低耦合增加重用，可是重用反而会增加耦合。
 * 需要重新考虑分层架构真的能够降低耦合？
 * 解耦应该大于重用
- IoC(控制反转)
 * 通过配置文件实现，很多配置文件我们从来不改，改也很麻烦。
 * 配置文件使项目重构时不能统一修改(无法与IDE集成)
 * 增加性能损耗、学习成本与文档文本。
 * 生成一个对象的步骤变复杂(别扭和不直观)
 * 降低人们了解全部源代码能力 (限制了开发，麻烦了管理)
 * 我们需要这么灵活吗？
[slide]
# 为何不用spring
- 提倡小而紧，高聚合，低耦合系统
 * 分层是有必要的，未必需要用AOP/IoC实现
 * 分层通过用不同包(类)实现，尽量不增加额外配置文件
 * 对内支持灵活重构，对外保持不变、少变(RESTful API)
 * 黑盒测试，模拟场景+性能测试
 * 更适合XP开发，快速迭代
- 架构三原则：简单、简单、再简单
 * "互联网+"特点未必是大，但一定要快
 * 简单才能快
 * 重要的是数据结构而不是复杂的算法

[note]
UNIX哲学:简单简单简单
[/note]

[slide]
# 系统复杂可能原因(工作量评估参考)
- 前期：架构选型，数据定义，接口定义，开发测试环境准备
- 日志
- 线程并发
- 连接池
- 安全
- 缓存(用户，文件，会话)
- 异常处理:这个常常占用很多工作，常被忽略
- 单元测试调试
- 需求变更：数据关联增加复杂性
- 后期：部署，配置，脚本工具

[slide]
# 分布式系统开发总结
- 可靠性可扩展性最重要，其次才是性能
- 随时优雅重启，不是不停机
- IPC使用TCP，可用命令`netstat -tn`检查队列状态
- 考虑zookeeper实现自己的nameservice
 * DNS不适合快速failover(超时而不是轮询)
- 使用IDGenerater:减少生成ID时的IO等
- 避免阻塞IO+心跳检测
- 消息模型与协议格式尽早确定：thrift,PB,Avro,MessagePack - 利于系统升级
- 监控：内置http服务器+外部监控,REST-SOAP

[slide]
# 关门的能力: 知道不做什么也很重要
- 太多重点相当于没有重点，分心工作做不好任何一项工作
- 避免过度架构
 * maven一些插件用shell实现(比如打包、部署)
 * 单元测试用集成测试代替, 参考[mytest](https://kkshare.github.io/ppt/publish/mytest)
 * 自己写的代码文件少，依赖少，升级容易，包括本身的升级与依赖组件的升级

[slide]
# 其它经验
- Done is better than perfect --Facebook
- 始终关注性能，集中解决性能瓶颈(广度优先)
- 扩展性：预测一到两步（别太多）
- 热爱
- *边*工作*边*总结，不只是工作后总结，后者难度大
 * 记笔记(evernote随身携带)或blog
 * ppt:更能概括出精华，了解更深入，变成真正自己的知识
- 开发工具代替人力低效劳动

[slide]
# 工作体会
- 基础技能除了算法还有这些能力也很重要：
 * 专注能力
 * 学习能力
 * 使用工具或IDE的能力
 * 查找知识的能力，建立知识库索引的能力(blog,evernote)
- 创新很重要，那么什么是创新，如何才能创新，创造创新的条件：
 * 工具或IDE掌握熟练了，工作效率高了，业余时间多了
 * 同事关系融洽了

[slide]
# 技术管理总结
- 执行者制定流程，利于持续改进（唯变不变）
- 让流程随处可见，随时参考和改进
 * 项目中README，INSTALL
 * web方式发布，而不是mail/ftp doc/docx/ppt/pptx/...
- 优先开发工具
- 亲自参与开发才能真正了解和预计进度
- 项目计划细化，单个任务不要超过一周
- UNIX哲学：简单简单简单
 * 重要的是数据结构而不是算法
 * 设计的系统必须能让*一个人*理解

[slide]
# 适合自己(公司)的才是最好的

Thanks!

# 个人使用技术栈


<!--more-->

这篇文章，是受到这个博主的（https://www.bmpi.dev/dev/tech-stack-of-side-project/ ）的启发，记录一下自己这些年使用的并留下来的技术盏。

一方面，可以对自己有更清楚的认识；另一方面，如果有人看这个私人博客，可以快速了解博主的技术水平，如若得不到价值，可减少不必要的时间浪费。

## 编程语言

作为一个后端的程序开发设计人员，秉持着设计大于语言实现。但没有尝试更多的技术语言，无法在比较中有任何的发言权利，这点正在检讨中。

- JAVA：过去的很多年，一直在使用这一个模型。遇到项目的第一反应，使用gradle或maven去构建一个springboot的项目。这有效，但是似乎是个坏习惯，屏蔽了新技术的应用。
- GO：正在尝试使用GO，去替换业务中一个小型业务模块，促进对非语言依赖的RPC框架的使用。
- Python：使用Python给我女儿讲解一些可视化的编程课程。学习了一部分的Python语法。正在学习使用Python替代Excel作为特定场景计算应用。现在看大火的技术语言，在数据分析领域有高效，学习成本低等天然优势。

## 技术框架

- Dubbo：用了很多年的Dubbo2.x的RPC框架，为数不多的认真的读过传输模型的核心代码。这个框架，使用的Netty的NIO，足够简单专注，成本低，速度快，适合小型团队的快速应用。但也存在很多被诟病的问题，启动扫描成本高，在庞大冗杂的业务系统面前，面对几千甚至更多的服务列表，单纯的服务治理对项目管理来说显得无能为力。好消息是2021年，3.0版本被发布出来，还尝试支持gRPC的通信，期待这个框架能够再次活跃起来。

- SpringCloud：如果说Dubbo是个服务治理框架，实际上的SpringCloud的全家桶更多的是面对微服务概念产生的一个服务管理生态。包括负载均衡，流量治理，熔断等等，特别是支持第七层的Rest服务调用，考虑到近年飞速发展的容器技术，丛云原生到服务网格等等，与dubbo相比，这两者就是兼容和不兼容的本质区别。SpringCloud背后还有想Netflix，Alibaba等大厂支持，还是当下JAVA领域最成熟的解决框架。

- Service Mesh：严格的说，这不是一个技术框架，而是要配合容器技术这种行业发展趋势，接触如gRPC这种跨语音的RPC解决方案。这个模型还在学习使用中，等掌握之后再更新。

## 架构模型

作为后端架构师，习惯性的做领域模型设计，拆分服务模型，支持服务级别快速拆分，支持服务级别快速扩容。过去几年的项目中，经历了底层环境变化，插件式的功能拼装，做了非常多的服务间的拆拆合合。深刻的体会到服务化“规范”的价值。

- 微服务：所有公司级别项目，都遵循这个服务模型，dubbo/springcloud的框架下的springboot的应用管理。
  
- Serverless：最近尝试将个人项目Serverless应用化，成本评估是主要原因，也看好几年内的这个领域的快速发展。

## 数据存储

数据处理是我们所有产品/应用的最终目的。过去工作中的主要数据存储工具，是数据库层级的Mysql和对象层级的Ceph。个人存储会在网盘文件中。现在逐渐在使用一些新鲜的事务。

- Mysql：作为应用产品系统架构师，OLTP领域，还是首选Mysql，绝大多数的工作也是在这里，没什么说的。优缺点，网上很透彻了。

- Tidb：2020年引进到系统中。对比Mysql，它在亿级别单表上的操作上表现很好。在没使用Tidb前，为了避免做分库分表这个单向门操作，做了很多方案。包括影响业务的定期归档，冷热表分离，以及使用ElasticSearch做查询等。另一方面，Tidb还有一定的OLAP能力，具有小型的连表查询分析能力。对比Mysql来说，缺点是成本较高，一组高可用性最低模型需要八个节点。Mysql是三个。磁盘性能要求也比较高。他的分析能力也无法跟专门的分析性数据库对比。是一个主OLTP兼OLAP场景的不错的解决方案。

- Redis：Redis集群，主要以缓存的方式出现，提升系统的查询能力，常见的使用是加载Tidb等生成的数据，降低数据库压力。还有一个重要的作用是分布式应用的锁，比起依赖ZK的锁更常用一些。

- Memcache：在小型的独立项目中还是比较常用，降低数据库压力。在一些特定的高并发场景有不错的表现。但总得来说，我接触的Memcache场景已经不多了。

- MangoDB：在之前配合算法同学做的机器人项目中，“被动”接触了MangoDB，在非结构化数据模型的实时查询领域，有很好的的表现，其他的优点体验的不多，其他项目并没有应用。

- Hbase：公司项目中主要的数据仓库。主要作用是离线数据分析使用。ETL是个比较麻烦的事情，毕竟数据分析的同学并不擅长数据结构设定，合适的拆分关系型数据库模型，对架构师能力有很高的要求，同样的，从拆分的关系构建一张width-column数据模型的能力，也一样重要。

- Amazon DynamoDB：近期正在个人项目中接触的数据库存储，配合Serverless模型的应用，尝试将OLTP部分，移植到一个Nosql的项目中，看看会有什么问题。

- Amazon S3：同样是由于Serverless模型中，对象存储的存在。这部分还在学习状态，等待日后更新。

## 基础服务

- AWS：大量的托管类服务。行业顶级的Paas/Saas工具。很多我打算在Aliyun使用的功能，都会现在AWS上找对应工具进行体验。但是记得有些服务要及时删除，部分服务费用昂贵。

- AliYun：国内最好的云服务商。一些工作的项目，正在逐渐迁移到阿里云的EKS的云原生环境上。

- Namecheap：域名注册商。

## 部署

- Docker：容器化是现在，也是可以看到的时间里的未来。工作中的应用环境，全部在Docker容器上；个人项目中，受限一些部署迁移的工具，也仍然在使用虚拟机。

- Kubernetes：工作中，使用私有云环境K8s集群，正在迁移阿里云EKS集群中。学习成本比较高。两个小建议：1. 经验不足使用托管EKS。2. 虚拟机 or 容器集群？ 容器集群；容器集群的成本在初期会略微贵一点点，但规模化后，节点利用率高，边际成本低。

## 开发工具

- Github：无需多说，源码管理。我的Blog的内容也在Github上托管。

- InteliJ IDEA：最主要的JAVA项目开发调试工具，缺点就是太重了。
  
- VSCode：主要在写文章，写团队博客中使用。最近也尝试在阅读代码中使用VSCode替代InteliJ，最重要的原因是轻量级，不会引起风扇噪音。插件丰富，能满足绝大多数的工作需要。准备再使用一段时间，看看能否将开发工作也迁移过来。

## 设计

- OmniGraffle：个人使用比较习惯的绘图工具，用来画架构，流程图。他有很多模板（stencil）下载，方便拖拽选用。

- Axure：产品原型工具。日常项目中，有很多技术驱动的产品设计，需要画出来与产品研发同学沟通，这个工具搭建简易原型要更有效率。顺便多说一句，项目设计时，一图胜千言。


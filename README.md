# ServellessLLM学习笔记

论文仓库：[ServerlessLLM/ServerlessLLM: Cost-efficient and fast multi-LLM serving. (github.com)](https://github.com/ServerlessLLM/ServerlessLLM)

## Servelless简介

​	Serverless 是对用户强调 No Server，本质并不是不需要服务器，而是将服务器全权托管给了云厂商，用户不用去关心，不用去管理，只用把业务部署到平台上来，只需聚焦业务逻辑代码，能够根据实际请求进行弹性伸缩，不用再去关心资源够不够。

![](.\image\1.webp)

​	作为开发者，我们可以**直接把镜像或者代码包部署到 Serverless 计算平台上来**，省去了整个资源的购买和环境部署这个过程。部署上来之后呢，后端可以跟存储、数据库进行交互，构成完整的 Serverless 架构。之后通过像 LB 或者 HTT 的方式，直接去访问到业务代码，平台会根据用户的请求去做调度和弹性伸缩。Serverless 平台支持负载均衡，应对各种突发流量，用户不用去关心后台资源。

![2](.\image\2.webp)

### Servelless主要技术

​	FaaS（函数即服务） + BaaS（后台即服务） 可以称为一个完整的 Serverless 的实现。除此之外，还有 PaaS（平台即服务）的概念。而通常平台环境都通过容器技术实现，最终都为了达到 NoOps（无人运维），或者至少 DevOps（开发&运维）。

简单介绍一下这几个名词，防止大家被绕晕：

- **FaaS** - Function as a service

​	函数即服务，每一个函数都是一个服务，函数可以由任何语言编写，除此之外不需要关心任何运维细节，比如：计算资源、弹性扩容，而且可以按量计费，且支持事件驱动。业界大云厂商都支持 FaaS，各自都有一套工作台、或者可视化工作流来管理这些函数。

- **BaaS** - Backend as a service

​	后端及服务，就是集成了许多中间件技术，可以无视环境调用服务，比如数据即服务（数据库服务），缓存服务等。虽然下面还有很多 `XAAS`，但组成 Serverless 概念的只有 FaaS + BaaS。

- **PaaS** - Platform as a service

​	平台即服务，用户只要上传源代码就可以自动持续集成并享受高可用服务，如果速度足够快，可以认为是类似 Serverless。但随着以 Docker 为代表的容器技术兴起，以容器为粒度的 PaaS 部署逐渐成为主流，是最常用的应用部署方式。比如中间件、数据库、操作系统等。

- **DaaS** - Data as a service

​	数据即服务，将数据采集、治理、聚合、服务打包起来提供出去。DaaS 服务可以应用 Serverless 的架构。

- **IaaS** - Infrastructure as a Service

​	基础设施即服务，比如计算机存储、网络、服务器等基建设施以服务的方式提供。

- **SaaS** - Software as a Service

​	软件即服务，比如 ERP、CRM、邮箱服务等，以软件为粒度提供服务。

- **容器**

​	容器就是隔离了物理环境的虚拟程序执行环境，而且环境可被描述、迁移，比较热门的容器技术是 **Docker**。随着容器数量增多，就出现了管理容器集群的技术，比较有名的容器编排平台是 Kubernetes。容器技术是 Serverless 架构实现的一种选择，也是实现的基础。

- **NoOps**

​	就是无人运维，比较理想主义，也许要借助 AI 的能力才能实现完全无人运维。无人运维不代表 Serverless，Serverless 可能也需要人运维（至少现在），只是开发者不再需要关心环境。

- **DevOps**

笔者觉得可以理解为 “开发即运维”，毕竟出了事情，开发要被问责，而一个成熟的 DevOps 体系可以让更多的开发者承担 OP 的职责，或者与 OP 更密切的合作。



## 参考内容

1.[一文读懂 Serverless 的起源、发展和落地实践-阿里云开发者社区 (aliyun.com)](https://developer.aliyun.com/article/857454)


---
description: 预计阅读时间：10分钟
---

# Docker 概述

Docker是一个用于开发，发布和运行应用程序的开放平台。Docker使您能够将应用程序与基础环境分离，从而可以实现快速交付应用。您可以通过像管理应用程序那样来管理应用所需要的基础运行环境。通过利用Docker的方法来快速交付，测试和部署代码，您可以大大减少从编写代码到在生产环境中上线之间所需要的时间。

### Docker 平台

Docker提供了在轻量隔离环境（容器）中打包和运行应用程序的功能。隔离和安全的特性使您可以在给定主机上同时运行多个容器。docker容器是轻量的，因为它们不需要管理程序的额外负载，而是直接在主机的内核中运行。这意味着与使用虚拟机相比，在给定的硬件配置上可以运行更多的容器。您甚至可以在虚拟机（vm）中运行Docker容器！

Docker提供了工具和平台来管理容器的生命周期：

* 使用容器开发应用程序及其支持组件。
* 容器成为构建和测试程序的基本单元。
* 准备就绪后，可以将应用程序作为容器或协调服务部署到生产环境中。无论您的生产环境是本地数据中心，云提供商还是两者的混合，其工作原理都相同。

### Docker 引擎 <a id="docker-engine"></a>

Docker引擎是基于C/S架构的应用程序，主要包括以下组件：

* 一个常驻运行的服务端程序，我们称为守护进程（daemon/`dockerd` command）。
* REST API，它指定程序可以用来与守护进程进行通信并指示其操作的接口。
* 命令行界面（CLI）客户端（docker命令）。

![](.gitbook/assets/engine-components-flow.png)

CLI使用Docker REST API与Docker守护程序进行交互。许多其他Docker应用程序都使用基础API和CLI。

守护程序创建和管理Docker对象，例如镜像，容器，网络和卷。

{% hint style="info" %}
Docker已经基于Apache 2.0许可开放源代码。
{% endhint %}

有关更多详细信息，请参阅下面的Docker架构。

### 我可以用Docker做什么？

快速，一致地交付您的应用程序。

Docker通过允许开发人员使用本地容器来模拟标准化的线上环境，从而简化了开发生命周期。容器非常适合持续集成和持续交付（CI / CD）工作流程。

考虑以下示例场景：

* 您的开发人员在本地编写代码，并使用Docker容器与同事共享他们的工作。
* 他们使用Docker将其应用程序部署到测试环境中，并执行自动和手动测试。
* 当开发人员发现错误时，他们可以在开发环境中对其进行修复，然后将其重新部署到测试环境中以进行测试和验证。
* 测试完成后，将修补程序推送给生产环境就像将更新的镜像推送到生产环境一样简单。

响应式部署和扩展

基于Docker容器化的应用具有高度的可移植性。 Docker容器可以在开发人员的本地笔记本电脑上，数据中心内的物理或虚拟机上，云提供商上或混合环境中运行。

Docker的可移植性和轻量级的特性还使您可以轻松地动态管理工作负载，并根据业务需求实时扩展或停止不需要的应用程序和服务。

在同一硬件上运行更多工作负载

Docker轻量而且快速。它为基于虚拟机管理程序的虚拟机提供了可行且经济高效的替代方案，因此您可以利用更多的计算能力来实现业务目标。 Docker非常适合高密度环境以及中小型部署，而您可以用更少的资源做更多的事情。

### Docker 架构 <a id="docker-architecture"></a>

Docker使用C/S架构。 Docker客户端与Docker守护进程进行通信，该守护程序完成了构建，运行和分发Docker容器的繁重工作。Docker客户端和守护进程可以在同一系统上运行，或者您可以将Docker客户端连接到远程Docker守护进程。Docker客户端和守护进程通过UNIX套接字（本地UNIX sockets）或网络使用REST API进行通信。

![](.gitbook/assets/architecture.svg)

#### Docker 守护进程 <a id="the-docker-daemon"></a>

Docker守护进程（dockerd）监听Docker API请求并管理Docker对象，例如镜像，容器，网络和卷。守护进程还可以与其他守护程序通信以管理Docker服务。

#### Docker 客户端程序 <a id="the-docker-client"></a>

Docker客户端（docker）是许多Docker用户与Docker交互的主要方式。当您使用诸如docker run之类的命令时，客户端会将这些命令发送至dockerd，然后执行它们。 docker命令使用Docker API。 Docker客户端可以与多个守护进程通信。

#### Docker 镜像仓库 <a id="docker-registries"></a>

Docker镜像仓库存储Docker镜像。 Docker Hub是任何人都可以使用的公开镜像库，并且默认情况下，Docker配置为在Docker Hub上查找镜像。您可以指定私有镜像库。

执行`docker pull`或`docker run`命令时，所需的镜像将从配置的镜像库中提取。使用`docker push`命令时，会将镜像推送到配置的镜像库。

#### Docker 对象 <a id="docker-objects"></a>

使用Docker时，您就会创建和使用镜像，容器，网络，卷，插件和其他对象。本节是其中一些对象的简要概述。

**镜像**

**镜像**是一个只读模板，其中包含创建Docker容器的说明。


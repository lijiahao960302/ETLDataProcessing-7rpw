
> 注：当前项目为 Serverless Devs 应用，由于应用中会存在需要初始化才可运行的变量（例如应用部署地区、服务名、函数名等等），所以**不推荐**直接 Clone 本仓库到本地进行部署或直接复制 s.yaml 使用，**强烈推荐**通过 `s init ` 的方法或应用中心进行初始化，详情可参考[部署 & 体验](#部署--体验) 。

# ETLDataProcessing 帮助文档
<p align="center" class="flex justify-center">
    <a href="https://www.serverless-devs.com" class="ml-1">
    <img src="http://editor.devsapp.cn/icon?package=ETLDataProcessing&type=packageType">
  </a>
  <a href="http://www.devsapp.cn/details.html?name=ETLDataProcessing" class="ml-1">
    <img src="http://editor.devsapp.cn/icon?package=ETLDataProcessing&type=packageVersion">
  </a>
  <a href="http://www.devsapp.cn/details.html?name=ETLDataProcessing" class="ml-1">
    <img src="http://editor.devsapp.cn/icon?package=ETLDataProcessing&type=packageDownload">
  </a>
</p>

<description>

随着云计算、人工智能、物联网等新技术的应用普及，人类产生的数据呈现出了爆发式增长的态势，对数据处理的需求能力也提出了越来越高的要求。数据成了重要资产，收集、处理数据的能力成为了核心竞争力，比如：应用服务的运行监控，运营数据的分析，以及深度学习的数据过滤、预处理等，这些对已有数据的处理能力将直接影响服务的运营效率。我们可以使用现成的 ETL 系统完成上述目的，但是在很多情况下您可能希望自建服务。比如：

您的数据处理业务不定时运行，希望在无任务时，不消耗任何资源；
您的数据处理需求只有简单的几个步骤，"杀鸡焉用牛刀"？还是自建来的快点；
您的数据处理业务流程有较多的自定义步骤，但现成系统灵活性不足，自建才能满足业务需求；
您不希望消耗过多精力搭建和维护系统中使用的各类开源数据处理模块，但希望在大并发数据处理请求的场景下能够有较为良好的性能表现。
如果您有上述需求，或者希望实现一个 高度灵活、高度可靠、低成本、高性能 的离线数据处理系统，那么本文提供的 Serverless 技术方案将是您的最佳选择。

业务场景简介
场景：假设我们有一批待处理数据，数据的值为 data_1 或 data_2。我们数据处理的目的是统计各类数据的出现次数，并将统计结果存储到数据仓库中。当数据量级达到一定程度，亦或数据源异构的情况下，我们很难一次性的通过一个进程在短时间内快速处理完成，在这种场景下，函数工作流 + 函数计算的组合提供了高效的解决方案。

在介绍方案细节前，先来了解下主要会使用到的两款产品：

阿里云函数计算 是阿里云基于事件驱动的全托管计算服务，通过极强的弹性、多语言的支持、丰富的工具链帮助用户快速搭建 serverless 服务，应对瞬时波峰并免去运维烦恼，让您专注于业务逻辑。
阿里云函数工作流 是阿里云分布式任务协同的全托管云服务，支持函数计算、自建服务（如 ECS 自建）等作为底层计算资源来实现您的业务编排。
为方便展示数据处理方面的核心能力，在数据仓库的存储方面，我们使用阿里云对象存储（OSS）来代表各种类型的数据库等作为基础存储设施。

下述方案将展示如何使用函数工作流 + 函数计算实现一个低成本高弹性的数据处理系统。在这个系统中，函数计算将根据数据量大小动态提供底层计算资源用于数据的处理、统计等工作，函数工作流将协助实现复杂业务上下游的逻辑编排。

</description>

<codeUrl>



</codeUrl>
<preview>



</preview>


## 前期准备

使用该项目，您需要有开通以下服务：

<service>



| 服务 |  备注  |
| --- |  --- |
| 函数计算 FC |  消息分组，数据写入，数据压缩等函数部署在函数计算 |
| Serverless 工作流 |  数据转储工作流部署在 Serverless 工作流 |

</service>

推荐您拥有以下的产品权限 / 策略：
<auth>



| 服务/业务 |  权限 |  备注  |
| --- |  --- |   --- |
| 工作流 | AliyunFnFFullAccess |  创建或者更新音视频处理工作流 |
| 函数计算 | AliyunFCFullAccess |  创建或者更新消息分组，写入，压缩等函数 |

</auth>

<remark>



</remark>

<disclaimers>



</disclaimers>

## 部署 & 体验

<appcenter>
   
- :fire: 通过 [Serverless 应用中心](https://fcnext.console.aliyun.com/applications/create?template=ETLDataProcessing) ，
  [![Deploy with Severless Devs](https://img.alicdn.com/imgextra/i1/O1CN01w5RFbX1v45s8TIXPz_!!6000000006118-55-tps-95-28.svg)](https://fcnext.console.aliyun.com/applications/create?template=ETLDataProcessing) 该应用。
   
</appcenter>
<deploy>
    
- 通过 [Serverless Devs Cli](https://www.serverless-devs.com/serverless-devs/install) 进行部署：
  - [安装 Serverless Devs Cli 开发者工具](https://www.serverless-devs.com/serverless-devs/install) ，并进行[授权信息配置](https://docs.serverless-devs.com/fc/config) ；
  - 初始化项目：`s init ETLDataProcessing -d ETLDataProcessing `
  - 进入项目，并进行项目部署：`cd ETLDataProcessing && s deploy - y`
   
</deploy>

## 应用详情

<appdetail id="flushContent">

业务流程介绍:


</appdetail>

## 使用文档

<usedetail id="flushContent">
</usedetail>


<devgroup>


## 开发者社区

您如果有关于错误的反馈或者未来的期待，您可以在 [Serverless Devs repo Issues](https://github.com/serverless-devs/serverless-devs/issues) 中进行反馈和交流。如果您想要加入我们的讨论组或者了解 FC 组件的最新动态，您可以通过以下渠道进行：

<p align="center">  

| <img src="https://serverless-article-picture.oss-cn-hangzhou.aliyuncs.com/1635407298906_20211028074819117230.png" width="130px" > | <img src="https://serverless-article-picture.oss-cn-hangzhou.aliyuncs.com/1635407044136_20211028074404326599.png" width="130px" > | <img src="https://serverless-article-picture.oss-cn-hangzhou.aliyuncs.com/1635407252200_20211028074732517533.png" width="130px" > |
| --------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| <center>微信公众号：`serverless`</center>                                                                                         | <center>微信小助手：`xiaojiangwh`</center>                                                                                        | <center>钉钉交流群：`33947367`</center>                                                                                           |
</p>
</devgroup>

# 术语表

origin: <https://cloud.google.com/apis/design/glossary>


## 网络 APIs (Networked APIs)

应用程序编程接口（API），用于操作一组通过网络连接的计算机。他们使用网络协议（如：HTTP）通信。通常来说一个消费者会使用不同组织生产的 API。


## Google APIs

Google 提供的网络 api 。大部分 api 都在 googleapis.com 域名下面。其他类型的 api 比如客户端库或者 SDK 里面的 api 并不在此列。


## API 接口 (API Interface)

一个协议缓冲区服务定义。在大多数编程语言里面，它通常映射到一个接口。一个 API 接口可以由任意数量的 API 服务来实现。


## API 版本 (API Version)

一个或一组定义在一起 API 的版本号。API 版本号通常是一个 string 类型的字段，比如： v1 ，版本号一般在 API 请求里面或者 Protocol Buffers 的包名。


## API 方法 (API Method)

一个接口的单个操作。它通常在 rpc 定义的 Protocol Buffers 中。或者大多数编程语言的 API 接口中，它通常映射为一个函数。


## API 请求 (API Request)

一个 API 方法的单次调用。通常用于计费、日志记录、监视和限速。


## API 服务 (API Service)

部署在网络端点（一个或多个）中的 API 接口（一个或多个）。 API service 通过它的 service name 来标识，service name 符合 RFC 1035 DNS 。如：calendar.googleapis.com


## API 端点 (API Endpoint)

API service 用来服务实际 api 请求的网络地址，如：pubsub.googleapis.com 和 content-pubsub.googleapis.com


## API 产品 (API Product)

一个 API Service 加相关组件，如：服务条款、文档、客户端库和服务支持，共同作为一个产品呈现给客户。例如：Google Calendar API。注意：人们有时会用一个 API 产品仅仅只是因为一个 API 。


## API 服务定义 (API Service Definition)

定义一个API服务的接口文档（.proto 文件）和服务器配置文件（.yaml文件）。


## API 消费者 (API Consumer)

消费一个 API 服务的实体。比如：一个拥有客户端应用或者服务端资源并且使用 Google APIs 的 Google 项目。


## API 生产者 (API Producer)

生产 API 的实体。比如：一个提供 API 服务的 Google 项目。


## API 后端 (API Backend)

实现了一个 API 业务逻辑的服务器加相关基础设施的组合。


## API 前端 (API Frontend)

一个服务器加相关基础设施的组合，提供了 API 服务的常见功能，如：负载均衡和身份验证。备注： API 前端和 API 后端既可以运行在一起也能离的很远。在某些情况下，它们也可以被编译成一个二进制应用程序运行在一个进程里面。

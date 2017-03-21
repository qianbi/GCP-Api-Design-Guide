# API 设计指南

本 API 设计指南的更新时间：2017-02-21

origin: <https://cloud.google.com/apis/design/>


## 简介
这是一个通用的网络 api 设计指南。从2014年起就已经在 Google 内部使用。我们在设计云平台 api 以及其他 api 时就遵循了这个规范。我们分享这个设计指南给全世界人民，以便于我们更好的合作。

Google 云平台的 api 开发人员在设计 gRPC APIs 时会发现这个设计指南特别有用。并且我们强烈建议这些开发人员遵循该设计原则。但是我们对非 Google 开发人员并没有此要求，你可以在不遵循此规范的情况下正常使用 Google 云平台 api 或 gRPC APIs 。

本指南为 REST api 和 RPC api 而设计，尤其是 gRPC APIs 。 gRPC APIs 使用 Protocol Buffers 去定义 HTTP mapping 、日志、监控等表层 api 及相关的 api 服务器配置。Google APIs 及 gRPC APIs 都用到了 HTTP mapping 去做 JSON/HTTP 到 Protocol Buffers/RPC 的映射。

每当有新的风格或设计模式被批准并采纳时，本指南就会更新。也就是说本指南没有最终版本，它将是艺术和工程持续不断的结晶。


## 本文档约定
本文档中需求等级的关键词 "MUST"、"MUST NOT"、"REQUIRED"、"SHALL"、"SHALL NOT"、"SHOULD"、"SHOULD NOT"、"RECOMMENDED"、"MAY" 和 "OPTIONAL" 的含义遵循 RFC 2119。

在本文档中这些关键词会用加粗字体突出显示。

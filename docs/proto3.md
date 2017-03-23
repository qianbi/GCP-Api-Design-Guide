# Protocol Buffers v3

origin: <https://cloud.google.com/apis/design/proto3>

本章节将要描述如何在 api 设计中使用 [Protocol Buffers] 。为了优化开发人员的体验以及提高运行时效率， gRPC APIs 在 API 定义时**应该**(**should**)使用 Protocol Buffers version 3 (proto3)

[Protocol Buffers] 是一个简单的语言无关和平台无关的接口定义语言(Interface Definition Language, IDL)，它被用来定义数据结构描述和编程接口。它同时支持二进制和 text wire 格式，并与许多不同的 wire 协议工作在不同的平台上。

Proto3 是 [Protocol Buffers] 的最后一个版本，与 Proto2 相比它有以下变更：

- `hasField` 不再用于原始字段。一个未赋值的原始字段有一个语言相关的默认值。
  - 消息字段仍然是可用的，可以使用编译器生成的 `hasField` 方法测试，或者与 null 做比较来测试，或在具体实现中定义标记值来测试。
- 字段中用户定义的默认值不再可用
- Enum 定义**必须**(**must**)从 Enum 值0开始
- Required 字段不再可用
— Extensions 不再可用。使用 `google.protobuf.Any` 替代
  - 为了保证向后及运行时兼容，`google/protobuf/descriptor.proto` 被保留
- Group 语法被移除

删除这些特性的原因是为了让 API 设计更简单、更稳定、性能更好。例如：我们在记录日志之前常常需要过滤某些字段，如删除敏感信息。而如果该字段是 required ，过滤信息这个需求就无法实现。

更多信息参考：[Protocol Buffers]



[Protocol Buffers]: https://github.com/google/protobuf

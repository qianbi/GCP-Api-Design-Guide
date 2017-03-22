# 目录结构

origin: <https://cloud.google.com/apis/design/directory_structure>

通常来说 API 服务端会使用 `.proto` 类型的文件来定义 API 对外的信息，用 `.yaml` 文件保存配置信息。

API 服务的代码仓库中**必须**(**must**)有一个文件目录包含它的定义文件及构建脚本。

API 的目录**应该**(**should**)有如下标准布局：
- API 目录
- 配置文件
  - `{service}.yaml` - Main service config file, `google.api.Service` proto 消息的 YAML 表示.
  - `prod.yaml` - Prod delta service config file.
  - `staging.yaml` - Staging delta service config file.
  - `test.yaml` - Test delta service config file.
  - `local.yaml` - Local delta service config file.

```
* 接口定义
  - `v[0-9]*/*` - 以这种方式命名的目录包含了同一个主(major)版本的 API ，主要是 proto 文件和构建脚本。
  - `{subapi}/v[0-9]*/*` - `{subapi}` 目录包含了某个子api(sub-API)的接口定义。每个子api可以有自己的主(major)版本号。
  - `type/*` - proto 文件包含了在不同 API 之间共享的类型。这些不同的 API 可能是不同版本号的相同 API 或者 API 和 服务端
    的实现。类型一旦被发布就**不应该(should not)**有突然的变更。
```

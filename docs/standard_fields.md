# 标准字段

origin: <https://cloud.google.com/apis/design/standard_fields>

本节定义一组标准的消息字段，当类似的概念出现时应该使用它们。这样确保不同的api中相同的概念具有相同的名称和语义。

| Name            | Type                | Description |
|-----------------|---------------------|-------------|
| name            | string              | **name** 字段应该(should)包含[相对资源]名称 |
| parent          | string              | 在资源定义和 List/Create 请求中， parent 字段应该(should)包含父资源的[相对资源]名称 |
| create_time     | Timestamp           | 一个实体的创建时间戳 |
| update_time     | Timestamp           | 一个实体的最近修改时间戳。注：该字段会在 create/patch/delete 操作完成之后更新 |
| delete_time     | Timestamp           | 当一个实体支持保留记录时，用于记录实体被逻辑删除时的时间戳 |
| time_zone       | string              | 时区的名称。应该是一个[IANA TZ]名称，比如： America/Los_Angeles 。更多信息参看：<https://en.wikipedia.org/wiki/List_of_tz_database_time_zones> |
| region_code     | string              | Unicode 编码的国家/地区（CLDR），比如： US和419。更多信息参看：<http://www.unicode.org/reports/tr35/#unicode_region_subtag> |
| language_code   | string              | BCP-47 语言代码，如： en-US、sr-Latn 。更多信息参看：<http://www.unicode.org/reports/tr35/#Unicode_locale_identifier>. |
| display_name    | string              | 一个实体的显示名称 |
| title           | string              | 一个实体的正式名称，如公司名称。它应该（should）被视为 **display_name** 的正式版本 |
| description     | string              | 关于某个实体的文本描述，文本描述可以是一段也可以是多段 |
| filter          | string              | 列表方法中的标准过滤参数 |
| query           | string              | 如果在一个 search 方法中使用与 **filter** 等同(即：[search]) |
| page_token      | string              | 分页请求的 token |
| page_size       | int32               | 总页数 |
| total_size      | int32               | 记录的总条数，与当前第几页无关 |
| next_page_token | string              | 响应结果中下一页的 token。被用来作为下一页请求 **page_token** 的值。空值意味着没有更多的结果 |
| resume_token    | string              | 一个不公开的token用于恢复流请求 |
| labels          | map<string, string> | 表示云资源标签 |
| deleted         | bool                | 如果某个资源允许撤销删除操作，它必须有一个 **deleted** 字段来表明资源已被删除 |
| show_deleted    | bool                | 如果某个资源允许撤销删除操作，它必须有一个 **show_deleted** 字段以便于客户端可以区分被删除了的资源 |
| update_mask     | FieldMask           | 在 **Update** 消息中，用于对某一资源进行部分更新 |
| validate_only   | bool                | 如果设置为 true ，表示给定的请求只用来做验证不做执行 |



[相对资源]: https://github.com/qianbi/GCP-Api-Design-Guide/blob/master/docs/resource_names.md#relative-resource-name
[IANA TZ]: http://www.iana.org/time-zones
[search]:  https://github.com/qianbi/GCP-Api-Design-Guide/blob/master/docs/custom_methods#common-custom-methods

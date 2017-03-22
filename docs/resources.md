# 面向资源的设计

origin: <https://cloud.google.com/apis/design/resources>

本指南的目标是帮助开发者设计出**简单、一致、便于使用**的网络 api。与此同时，该指南还有助于 RPC APIs（基于 socket） 和 REST APIs（基于 HTTP） 这两者设计理念的融合。

一般来说，人们用 api 接口和方法的方式设计 RPC APIs，如 CORBA 和 Windows COM 。随着时间的流逝，会产生越来越多的接口和方法。最后的结果可能是大量互不相同的接口和方法。开发者为了正确的使用这些接口和方法不得不仔细的熟悉它们，这是一件既耗时又容易出错的事情。

[REST](http://en.wikipedia.org/wiki/Representational_state_transfer) 架构首次在2000年提出，它主要设计与 HTTP/1.1 协调工作。 REST 架构的核心原则是定义资源，这些资源拥有自己的命名及少量的可用来操作资源的方法。这些资源及方法就是 APIs 的名词和动词。就 HTTP 协议来说，资源的名词对应的就是 url，资源的方法对应的就是 HTTP 的方法 POST、GET、PUT、PATCH 和 DELETE。

最近 HTTP REST APIs 在互联网上获得了巨大的成功。2010年，公共网络 api 中 HTTP REST APIs有大约74%的占有率。

虽然 HTTP REST APIs 在互联网上很受欢迎，但是 REST APIs 的流量远小于传统的 RPC APIs 。例如，美国互联网流量高峰时期有一半是视频内容，由于性能的原因很少会有人考虑用 REST APIs 去分发这些视频内容。在数据中心内部，许多公司使用 基于 socket 的 RPC APIs 去做网络数据交互，这些 API 的数量可能比公开的 REST APIs 有更高的数量级。

In reality, both RPC APIs and HTTP REST APIs are needed for various reasons. Ideally, an API platform should provide best support for all APIs. This Design Guide helps you design and build APIs that conform to this principle. It does so by applying resource-oriented design principles to general API design, and defines many common design patterns to improve usability and reduce complexity.

NOTE: This Design Guide explains how to apply REST principles to API designs independent of programming language, operating system, or network protocol. It is NOT a guide solely to creating REST APIs.


## REST API 是什么?

A REST API is modeled as collections of individually-addressable resources (the nouns of the API). Resources are referenced with their resource names and manipulated via a small set of methods (also known as verbs or operations).

Standard methods for REST Google APIs (also known as REST methods) are List, Get, Create, Update, and Delete. Custom methods (also known as custom verbs or custom operations) are also available to API designers for functionality that doesn't easily map to one of the standard methods, such as database transactions.

NOTE: Custom verbs does not mean creating custom HTTP verbs to support custom methods. For HTTP-based APIs, they simply map to the most suitable HTTP verbs.


## Design flow

The Design Guide suggests taking the following steps when designing resource- oriented APIs (more details are covered in specific sections below):

- Determine what types of resources an API provides.
- Determine the relationships between resources.
- Decide the resource name schemes based on types and relationships.
- Decide the resource schemas.
- Attach minimum set of methods to resources.


## Resources

A resource-oriented API is generally modeled as a resource hierarchy, where each node is either a simple resource or a collection resource. For convenience, they are often called as a resource and a collection, respectively.

- A collection contains a list of resources of the same type. For example, a user has a collection of contacts.
- A resource has some state and zero or more sub-resources. Each sub-resource can be either a simple resource or a collection resource.

For example, Gmail API has a collection of users, each user has a collection of messages, a collection of threads, a collection of labels, a profile resource, and several setting resources.

While there is some conceptual alignment between storage systems and REST APIs, a service with a resource-oriented API is not necessarily a database, and has enormous flexibility in how it interprets resources and methods. For example, creating a calendar event (resource) may create additional events for attendees, send email invitations to attendees, reserve conference rooms, and update video conference schedules.


## Methods

The key characteristic of a resource-oriented API is that it emphasizes resources (data model) over the methods performed on the resources (functionality). A typical resource-oriented API exposes a large number of resources with a small number of methods. The methods can be either the standard methods or custom methods. For this guide, the standard methods are: List, Get, Create, Update, and Delete.

Where API functionality naturally maps to one of the standard methods, that method should be used in the API design. For functionality that does not naturally map to one of the standard methods, custom methods may be used. Custom methods offer the same design freedom as traditional RPC APIs, which can be used to implement common programming patterns, such as database transactions or data analysis.


## Examples

The following sections present some real world examples on how to apply resource-oriented API design to large scale services.


## Gmail API

The Gmail API service implements the Gmail API and exposes most of Gmail functionality. It has the following resource model:

- The Gmail API service: gmail.googleapis.com
- A collection of users: users/*. Each user has the following resources.
  - A collection of messages: users/*/messages/*.
  - A collection of threads: users/*/threads/*.
  - A collection of labels: users/*/labels/*.
  - A collection of change history: users/*/history/*.
  - A resource representing the user profile: users/*/profile.
  - A resource representing user settings: users/*/settings.


## Google Cloud Pub/Sub API

The `pubsub.googleapis.com` service implements the Google Cloud Pub/Sub API, which defines the following resource model:

- The API service: `pubsub.googleapis.com`
- A collection of topics: `projects/*/topics/*`.
- A collection of subscriptions: `projects/*/subscriptions/*`.

NOTE: Other implementations of the Pub/Sub API may choose different resource naming schemes.

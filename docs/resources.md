# 面向资源的设计

origin: <https://cloud.google.com/apis/design/resources>

The goal for this Design Guide is to help developers design simple, consistent and easy-to-use networked APIs. At the same time, it also helps converging designs of socket-based RPC APIs with HTTP-based REST APIs.

Traditionally, people design RPC APIs in terms of API interfaces and methods, such as CORBA and Windows COM. As time goes by, more and more interfaces and methods are introduced. The end result can be an overwhelming number of interfaces and methods, each of them different from the others. Developers have to learn each one carefully in order to use it correctly, which can be both time consuming and error prone.

The architectural style of REST was first introduced in 2000, primarily designed to work well with HTTP/1.1. Its core principle is to define named resources that can be manipulated using a small number of methods. The resources and methods are known as nouns and verbs of APIs. With the HTTP protocol, the resource names naturally map to URLs, and methods naturally map to HTTP methods POST, GET, PUT, PATCH, and DELETE.

On the Internet, HTTP REST APIs have been recently hugely successful. In 2010, about 74% of public network APIs were HTTP REST APIs.

While HTTP REST APIs are very popular on the Internet, the amount of traffic they carry is smaller than traditional RPC APIs. For example, about half of Internet traffic in America at peak time is video content, and few people would consider using REST APIs to deliver such content for performance reasons. Inside data centers, many companies use socket-based RPC APIs to carry most network traffic, which can be orders of magnitude higher than public REST APIs.

In reality, both RPC APIs and HTTP REST APIs are needed for various reasons. Ideally, an API platform should provide best support for all APIs. This Design Guide helps you design and build APIs that conform to this principle. It does so by applying resource-oriented design principles to general API design, and defines many common design patterns to improve usability and reduce complexity.

NOTE: This Design Guide explains how to apply REST principles to API designs independent of programming language, operating system, or network protocol. It is NOT a guide solely to creating REST APIs.


## What is a REST API?

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

The pubsub.googleapis.com service implements the Google Cloud Pub/Sub API, which defines the following resource model:

- The API service: pubsub.googleapis.com
- A collection of topics: projects/*/topics/*.
- A collection of subscriptions: projects/*/subscriptions/*.

NOTE: Other implementations of the Pub/Sub API may choose different resource naming schemes.
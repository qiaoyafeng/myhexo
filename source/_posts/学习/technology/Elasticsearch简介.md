---
title: Elasticsearch简介
date: 2021-08-011 09:49:04
author: 乔亚峰
top: true
toc: true
mathjax: false
summary: Elasticsearch 是一个分布式、RESTful 风格的搜索和数据分析引擎，能够解决不断涌现出的各种用例。
categories: Elasticsearch
tags:
  - Elasticsearch
  - 博客
---


Elasticsearch 是一个分布式、RESTful 风格的搜索和数据分析引擎，能够解决不断涌现出的各种用例。

Elasticsearch 是一个实时的分布式搜索分析引擎，它能让你以前所未有的速度和规模，去探索你的数据。 它被用作全文检索、结构化搜索、分析以及这三个功能的组合。

Elasticsearch是一个实时分布式和开源的全文搜索和分析引擎。 它可以从RESTful Web服务接口访问，并使用模式少JSON(JavaScript对象符号)文档来存储数据。它是基于Java编程语言，这使Elasticsearch能够在不同的平台上运行。使用户能够以非常快的速度来搜索非常大的数据量。

## Elasticsearch的特性

  - Elasticsearch可扩展高达PB级的结构化和非结构化数据。
  - Elasticsearch可以用来替代MongoDB和RavenDB等做文档存储。
  - Elasticsearch使用非标准化来提高搜索性能。
  - Elasticsearch是受欢迎的企业搜索引擎之一，目前被许多大型组织使用，如Wikipedia，The Guardian，StackOverflow，GitHub等。
  - Elasticsearch是开放源代码，可在Apache许可证版本2.0下提供。


## Elasticsearch的优点

  - Elasticsearch是基于Java开发的，这使得它在几乎每个平台上都兼容。
  - Elasticsearch是实时的，换句话说，一秒钟后，添加的文档可以在这个引擎中搜索得到。
  - Elasticsearch是分布式的，这使得它易于在任何大型组织中扩展和集成。
  - 通过使用Elasticsearch中的网关概念，创建完整备份很容易。
  - 与Apache Solr相比，在Elasticsearch中处理多租户非常容易。
  - Elasticsearch使用JSON对象作为响应，这使得可以使用不同的编程语言调用Elasticsearch服务器。
  - Elasticsearch支持几乎大部分文档类型，但不支持文本呈现的文档类型。



## 使用Python编程语言与 Elasticsearch 进行交互

```
from elasticsearch import Elasticsearch

esclient = Elasticsearch(['localhost:9200'])
response = esclient.search(
  index='social-*',
  body={
    "query": {
      "match": {
        "message": "myProduct"
      }
    },
    "aggs": {
      "top_10_states": {
        "terms": {
          "field": "state",
          "size": 10
        }
      }
    }
  }
)

```
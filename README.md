# OpenDoc

[![Build Status](https://travis-ci.org/michalyao/opendoc.svg?branch=master)](https://travis-ci.org/michalyao/opendoc)

Generate your API documentation using Swagger gracefully and automatically.

## 概述

OpenDoc 项目基于 [swagger-codegen](https://github.com/swagger-api/swagger-codegen) 的 Maven 插件开发，能够将符合 Swagger2.0 规范的 yaml 文件转换为可阅读性高，信息更丰富的html文档。通过结合Jenkins等工具可以方便的实现项目文档的自动构建，
大大提高了项目文档的可维护性。

## 适用
如果你正在使用 Java 开发项目，并且了解 Swagger ，那么OpenDoc可能很适合你。
如果你不熟悉 Java 也没关系，OpenDoc 非常容易学习和使用。


## 说明
OpenDoc 主要使用 Swagger-Codegen 生成代码，在原代码的基础上改进了模板:
- 汉化标签
- 修正参数不支持下划线形式的bug
- 修正汉化标签无法作为锚点的bug
- 主页项优化，包括一些默认项等
- 页面侧栏字母不强制大小写
Swagger-Codegen 使用 Mustache 模板引擎，因此你也可以直接修改 doctemplate 目录下的模板文件，来更改文档的样式或参数等。

Swagger 文档须符合 Swagger2.0 规范, 支持 json 和 yaml 两种文件格式, 字段与生成的文档对应关系详见
[todo.yml](todo.yml)
[index.html](http://blog.yoryor.me/opendoc)

## 环境要求
- git
- JDK 1.7+
- Maven 3.3.x
如果不熟悉Java开发，可以在网上找一些教程来安装JDK和Maven.

## 使用方法

1. git clone https://github.com/michalyao/opendoc.git
2. cd opendoc/ 
3. 修改 pom 文件35行，指定 yaml 文件的路径
4. mvn clean package
5. 打开 html 目录下的 index.html 文件查看生成的文档

## FAQ 
1. API 如何分组？
使用 tag 字段，请仔细对照示例 html 和 yaml 文件.
2. 如何显示方法的中文描述？
使用 summary 字段，请仔细对照示例 html 和 yaml 文件.
3. tag支持中文字段吗？
不支持，锚点中使用中文会到导致导航失效(欢迎PR)
4. Windows 环境下构建的文档为什么中文都乱码了？怎么解决？
Windows 默认编码 GBK，生成的 html 编码格式为 UTF-8，因此会乱码。使用 Linux 或者用 IDE 强制项目使用 utf8 编码构建即可。
如果仍然要使用 Windows 环境构建，需要修改环境变量，指定 JVM 使用 utf8 编码。添加环境变量 JAVA_TOOL_OPTIONS=-Dfile.encoding=UTF8。
修改成功后再次运行 mvn package 会看到控制台会额外打印一行信息: Picked up JAVA_TOOL_OPTIONS: -Dfile.encoding=UTF8
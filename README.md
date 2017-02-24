# OpenDoc
[![Build Status](https://travis-ci.org/michalyao/opendoc.svg?branch=master)](https://travis-ci.org/michalyao/opendoc)
Generate your API documentation using Swagger gracefully and automatically.

## 概述

OpenDoc 基于swagger-codegen的maven插件实现API文档的自动构建，能够将符合swagger2.0规范的yaml文件转换为可阅读性高，信息更丰富的html文档。结合Jenkins等工具可以方便的实现项目文档的自动构建。
如果你使用Java开发，或者是已经使用swagger来维护项目的文档，那么OpenDoc可能很适合你。即使你平时不采用Java开发，OpenDoc也非常易用。


## 说明
OpenDoc 主要使用swagger-codegen生成代码，在原代码的基础上改进了模板:
- 汉化标签
- 修正参数不支持下划线形式的bug
- 修正汉化标签无法作为锚点的bug
- 主页项优化，包括一些默认项等
- 页面侧栏字母不强制大小写
swagger-codegen 使用 mustache 模板引擎，因此你也可以直接修改doctemplate目录下的模板文件，来更改文档的样式或参数等。

swagger文档须符合 swagger2.0 规范, 支持json和yaml两种文件格式, 字段与生成的文档对应关系详见
[todo.yml](todo.yml)
[index.html](http://opendoc.yoryor.me)

## 环境要求
- git
- JDK 1.8+（低版本未验证）
- Maven 3.3.x
如果不熟悉Java开发，可以在网上找一些教程来安装JDK和Maven.

## 使用方法

1. git clone https://github.com/michalyao/opendoc.git
2. cd opendoc/ 
3. 修改pom文件35行，指定yaml文件的路径
4. mvn clean package
5. 打开html目录下的index.html文件查看生成的文档

## FAQ 
1. API 如何分组？
使用 tag 字段，请仔细对照示例html和yaml文件
2. 如何显示方法的中文描述？
使用 summary 字段，请仔细对照示例html和yaml文件
3. tag支持中文字段吗？
不支持，锚点中使用中文会到导致导航失效(欢迎PR)
4. windows环境下构建的文档为什么中文都乱码了？怎么解决？
Windows默认编码GBK，生成的html编码格式为UTF-8，因此会乱码。使用linux或者用IDE强制项目使用utf8编码构建即可。
如果仍然要使用windows环境构建，需要修改环境变量，指定JVM使用utf8编码。添加环境变量 JAVA_TOOL_OPTIONS=-Dfile.encoding=UTF8。
修改成功后再次运行mvn package会看到控制台会额外打印一行信息: Picked up JAVA_TOOL_OPTIONS: -Dfile.encoding=UTF8
# dubbo-compiler

为了解决在 build.gradle.kts 中直接使用 org.apache.dubbo:dubbo-compiler:0.0.1 报的错误:

``` log
Caused by: org.gradle.api.GradleException: protoc: stdout: . stderr: Error: Could not find or load main class org.apache.dubbo.gen.grpc.DubboGrpcGenerator
--dubbo-grpc_out: protoc-gen-dubbo-grpc: Plugin failed with status code 1.
```

原因为 dubbo-compiler 原本是为 maven 所使用, 当项目配置为 gradle 时, 无法从 META-INF 中安装依赖, 所以重新打包时给 pom.xml 中增加打包为单体的配置, 从而解决问题.

可以参照 [nnt.log.jvm](https://github.com/wybosys/nnt.logic.jvm/blob/v1.0/dubbo.prj/build.gradle.kts) 的gradle配置, 配置 dubbo-grpc 的使用.

ps: 原本 dubbo-grpc 可以通过 protoc-gen-dubbo-java 插件来编译 proto 接口, 但是这东西只有 linux 版本, mac 和 windows 无法进行开发工作
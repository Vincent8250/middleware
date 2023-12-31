# Maven

### 依赖

[仓库地址](https://mvnrepository.com/)

#### 示例

```xml
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>easyexcel</artifactId>
    <version>3.1.1</version>
</dependency>
```



#### 依赖配置

- groupId(必须): 定义了当前 Maven 项目隶属的组织或公司。
  groupId 一般分为多段，通常情况下，第一段为域，第二段为公司名称。
  域又分为 org、com、cn 等，其中 org 为非营利组织，com 为商业组织，cn 表示中国。
  以 apache 开源社区的 tomcat 项目为例，这个项目的 groupId 是 org.apache，它的域是 org（因为 tomcat 是非营利项目），公司名称是 apache，artifactId 是 tomcat。
- artifactId(必须)：定义了当前 Maven 项目的名称，项目的唯一的标识符，对应项目根目录的名称。
- version(必须)：定义了 Maven 项目当前所处版本。
- packaging（可选）：定义了 Maven 项目的打包方式（比如 jar，war...），默认使用 jar。
- classifier(可选)：常用于区分从同一 POM 构建的具有不同内容的构件，可以是任意的字符串，附加在版本号之后。
- dependencies：一个 pom.xml 文件中只能存在一个这样的标签，是用来管理依赖的总标签。
- dependency：包含在 dependencies 标签中，可以有多个，每一个表示项目的一个依赖。
- type(可选)：依赖的类型，对应于项目坐标定义的 packaging。大部分情况下，该元素不必声明，其默认值是 jar。
- scope(可选)：依赖的范围，默认值是 compile。
- optional(可选)：标记依赖是否可选
- exclusions(可选)：用来排除传递性依赖,例如 jar 包冲突



#### 依赖冲突



##### 直接依赖冲突

同一个项目下同一个项目只能被引用一个版本 版本冲突的情况下 会引入后声明的



##### 间接依赖冲突

间接依赖冲突的话遵从两个原则

第一个：最短路径原则
下面这种情况就会依赖X 2.0

```
依赖链路一：A -> B -> C -> X(1.0)
依赖链路二：A -> D -> X(2.0)
```

第二个：声明顺序优先原则
下面这种情况就会依赖X1.0 （因为B在D之前先声明的）

```
依赖链路一：A -> B -> X(1.0)
依赖链路二：A -> D -> X(2.0)
```



#### 依赖排除

解决依赖冲突的办法 还有手动排除依赖

~~~xml
<dependency>
    ......
    <exclusions>
      <exclusion>
        <artifactId>x</artifactId>
        <groupId>org.apache.x</groupId>
      </exclusion>
    </exclusions>
</dependency>
~~~







### 仓库

Maven 仓库分为：

- **本地仓库**：运行 Maven 的计算机上的一个目录，它缓存远程下载的构件并包含尚未发布的临时构件。`settings.xml` 文件中可以看到 Maven 的本地仓库路径配置，默认本地仓库路径是在 `${user.home}/.m2/repository`。
- **远程仓库**：官方或者其他组织维护的 Maven 仓库。



Maven 远程仓库可以分为：

- **中央仓库**：这个仓库是由 Maven 社区来维护的，里面存放了绝大多数开源软件的包，并且是作为 Maven 的默认配置，不需要开发者额外配置。另外为了方便查询，还提供了一个[查询地址](https://search.maven.org/)，开发者可以通过这个地址更快的搜索需要构件的坐标。
- **私服**：私服是一种特殊的远程 Maven 仓库，它是架设在局域网内的仓库服务，私服一般被配置为互联网远程仓库的镜像，供局域网内的 Maven 用户使用。
- **其他的公共仓库**：有一些公共仓库是为了加速访问（比如阿里云 Maven 镜像仓库）或者部分构件不存在于中央仓库中。



Maven 依赖包寻找顺序：

1. 先去本地仓库找寻，有的话，直接使用。
2. 本地仓库没有找到的话，会去远程仓库找寻，下载包到本地仓库。
3. 远程仓库没有找到的话，会报错。





### 生命周期



| 阶段          | 处理     | 描述                                                     |
| :------------ | :------- | :------------------------------------------------------- |
| 验证 validate | 验证项目 | 验证项目是否正确且所有必须信息是可用的                   |
| 编译 compile  | 执行编译 | 源代码编译在此阶段完成                                   |
| 测试 Test     | 测试     | 使用适当的单元测试框架（例如JUnit）运行测试。            |
| 包装 package  | 打包     | 创建JAR/WAR包如在 pom.xml 中定义提及的包                 |
| 检查 verify   | 检查     | 对集成测试的结果进行检查，以保证质量达标                 |
| 安装 install  | 安装     | 安装打包的项目到本地仓库，以供其他项目使用               |
| 部署 deploy   | 部署     | 拷贝最终的工程包到远程仓库中，以共享给其他开发人员和工程 |

Maven 有以下三个标准的生命周期：

- default(或 build)：项目部署的处理
- clean：项目清理的处理
- site：项目站点文档创建的处理





#### Default 生命周期

这是 Maven 的主要生命周期，被用于构建应用，包括下面的 23 个阶段：

| 生命周期阶段                                | 描述                                                         |
| :------------------------------------------ | :----------------------------------------------------------- |
| validate（校验）                            | 校验项目是否正确并且所有必要的信息可以完成项目的构建过程。   |
| initialize（初始化）                        | 初始化构建状态，比如设置属性值。                             |
| generate-sources（生成源代码）              | 生成包含在编译阶段中的任何源代码。                           |
| process-sources（处理源代码）               | 处理源代码，比如说，过滤任意值。                             |
| generate-resources（生成资源文件）          | 生成将会包含在项目包中的资源文件。                           |
| process-resources （处理资源文件）          | 复制和处理资源到目标目录，为打包阶段最好准备。               |
| compile（编译）                             | 编译项目的源代码。                                           |
| process-classes（处理类文件）               | 处理编译生成的文件，比如说对Java class文件做字节码改善优化。 |
| generate-test-sources（生成测试源代码）     | 生成包含在编译阶段中的任何测试源代码。                       |
| process-test-sources（处理测试源代码）      | 处理测试源代码，比如说，过滤任意值。                         |
| generate-test-resources（生成测试资源文件） | 为测试创建资源文件。                                         |
| process-test-resources（处理测试资源文件）  | 复制和处理测试资源到目标目录。                               |
| test-compile（编译测试源码）                | 编译测试源代码到测试目标目录.                                |
| process-test-classes（处理测试类文件）      | 处理测试源码编译生成的文件。                                 |
| test（测试）                                | 使用合适的单元测试框架运行测试（Juint是其中之一）。          |
| prepare-package（准备打包）                 | 在实际打包之前，执行任何的必要的操作为打包做准备。           |
| package（打包）                             | 将编译后的代码打包成可分发格式的文件，比如JAR、WAR或者EAR文件。 |
| pre-integration-test（集成测试前）          | 在执行集成测试前进行必要的动作。比如说，搭建需要的环境。     |
| integration-test（集成测试）                | 处理和部署项目到可以运行集成测试环境中。                     |
| post-integration-test（集成测试后）         | 在执行集成测试完成后进行必要的动作。比如说，清理集成测试环境。 |
| verify （验证）                             | 运行任意的检查来验证项目包有效且达到质量标准。               |
| install（安装）                             | 安装项目包到本地仓库，这样项目包可以用作其他本地项目的依赖。 |
| deploy（部署）                              | 将最终的项目包复制到远程仓库中与其他开发者和项目共享。       |





#### Clean 生命周期

当我们执行 mvn post-clean 命令时，Maven 调用 clean 生命周期，它包含以下阶段：

- pre-clean：执行一些需要在clean之前完成的工作
- clean：移除所有上一次构建生成的文件
- post-clean：执行一些需要在clean之后立刻完成的工作





#### Site 生命周期

Maven Site 插件一般用来创建新的报告文档、部署站点等。

- pre-site：执行一些需要在生成站点文档之前完成的工作
- site：生成项目的站点文档
- post-site： 执行一些需要在生成站点文档之后完成的工作，并且为部署做准备
- site-deploy：将生成的站点文档部署到特定的服务器上










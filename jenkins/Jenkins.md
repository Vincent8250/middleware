# Jenkins

## 安装

**版本**

最新版需要JDK11、17的支持
我不想再装JDK所以使用的是历史版本 - [2.346.1 下载链接](https://get.jenkins.io/war-stable/2.346.1/)    [历史版本 列表](https://get.jenkins.io/war-stable/)

启动命令

~~~bash
java -jar jenkins.war
~~~

默认密码 C:\Users\sun\.jenkins\secrets\initialAdminPassword

![image-20230704140627272](../img/image-20230704140627272.png)



**提示**

Jenkins安装成功后 会让你选择安装插件
两个选项 一个是自定义安装 一个是推荐安装 
可以先不安装 这个插件进去了也是可以装的

#### 安装插件

1. <img src="../img/image-20230705134832956.png" alt="image-20230705134832956" style="zoom:50%;" />
2. ![image-20230705134912113](../img/image-20230705134912113.png)
3. ![image-20230705134931847](../img/image-20230705134931847.png)
4. 最少需要安装
   中文插件、Git、Maven.. 具体看项目要求
   ![image-20230705135033302](../img/image-20230705135033302.png)
   ![image-20230705135100163](../img/image-20230705135100163.png)
   ![image-20230705135118021](../img/image-20230705135118021.png)



#### 全局配置

1. <img src="../img/image-20230705135228856.png" alt="image-20230705135228856" style="zoom:50%;" />
2. ![image-20230705135316552](../img/image-20230705135316552.png)
3. Maven配置
   ![image-20230705135334953](../img/image-20230705135334953.png)
   ![image-20230705135440071](../img/image-20230705135440071.png)
4. JDK配置
   ![image-20230705135354004](../img/image-20230705135354004.png)
5. Git配置
   ![image-20230705135428444](../img/image-20230705135428444.png)





#### Git凭据

![image-20230705135638012](../img/image-20230705135638012.png)

![image-20230705135552833](../img/image-20230705135552833.png)



#### 添加任务

1. ![image-20230705135715633](../img/image-20230705135715633.png)
2. ![image-20230705135819572](../img/image-20230705135819572.png)
3. ![image-20230705140102172](../img/image-20230705140102172.png)


















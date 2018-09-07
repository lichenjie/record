## ngrinder安装手册
+ 功能说明：ngrinder安装，并且在tomcat上运行。
+ 描述：
nGrinder是基于Grinder开源项目，由NHN公司的开发团队进行了重新设计和完善。nGrinder是一款非常易用，有简洁友好的用户界面和controller-agent分布式结构的强大的压力测试工具。
nGrinder测试基于python测试脚本(groovy也可)，用户按照一定规范编写测试脚本，controller会将脚本一集需要的资源分发到agent，用jython执行。并且在执行的过程中收集运行情况、相应时间、测试目标服务器的运行情况等。并且保存这些数据生成测试报告，以供查看。
这款框架的一大特点就是非常的简单易用，安装也很容易，可以说是开箱即用。
nGrinderr直接部署成web服务，支持多用户使用，可扩展性好，可自定义plugin
+ 网上资源:
    +下载地址：https://sourceforge.net/projects/ngrinder/files/ngrinder-3.2.3/

    +安装指南：http://my.oschina.net/u/939534/blog/102878

    +问题解答：http://ngrinder.642.n7.nabble.com/ngrinder-user-cn-f114.html

### 安装步骤

#### 1.下载程序
 NGrinder 由两个模块组成，其运行环境为 Oracle JDK 1.6
+ nGrinder controller  web 应用程序，部署在Tomcat 6.x 或更高的版本
+ nGrinder Agent     Java 应用程序


#### 2.安装Controller
首先将nGrinder-controler.war 放在Tomcat 的webapps 目录下。
在Tomcat的启动文件start.sh/start.bat 中设置如下参数可以使Controller更稳定快速运行！

```
    JAVA_OPTS="-Xms600m -Xmx1024m -XX:MaxPermSize=200m"    # for catalina.sh

    set JAVA_OPTS=-Xms600m -Xmx1024m -XX:MaxPermSize=200m  # for catalina.bat
```
现在就可以启动nGrinder-controller。如果你不想在浏览器里 输入 http://hostname:8080/ngrinder-controller，

登录账号admin/admin ,可以将nGrinder-controler.war 改为 ROOT.war


#### 3.安装Agent
Agent作为一个Java应用程序，它可以做如下工作
+ 1.作为性能测试的一个监控服务器
+ 2.作为执行测试脚本对目标站点进行测试的服务器

运行Agent很简单！
```
    Windows:  ngrinder-core-{VersionNumber}-agent-package.zip  --> run_agent.bat

    Linux:  ngrinder-core-{VersionNumber}-agent-package.tar.gz --> run_agent.sh
```
当Agent正常启动后，它会在用户目录下创建
```
    ${user.home}/.ngrinder_agent
    例如本机 D:\Users\Administrator\.ngrinder_agent
```
然后，请在agent.conf 配置如下

```
    #start.mode=monitor
    #monitor.listen.port=13243
    # If you want to monitor bind to the different local ip not automatically selected ip. Specify below field.
    #monitor.host=hostname_or_ip

    start.mode=agent
    agent.console.ip=127.0.0.1
    #agent.console.port=16001
    #agent.region=
    #agent.hostid=
    #agent.servermode=true

    # provide more agent java execution option if necessary.
    #agent.javaopt=
    # set following false if you want to use more than 1G Xmx memory per a agent process.
    #agent.useXmxLimit=true
    #agent.same.console.host=true
    # please uncomment the following option if you want to send all logs to the controller.
    #agent.send.all.logs=true
```









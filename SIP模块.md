# SIP模块

## 基本概念
### Sofia-SIP
FreeSWITCH的SIP功能是在`mod_sofia`模块中实现的。FreeSWITCH并没有自己开发新的SIP协议栈，而是使用了比较成熟的开源SIP协议栈`Sofia-SIP`，以避免“重复发明轮子” 。

### Endpoint
在FreeSWITCH中，实现一些互联协议接口的模块称为`Endpoint`。Free-SWITH支持很多类型的Endpoint，如`SIP`、`H232`等。这些不同的Endpoint主要是使用不同的控制协议跟其他的Endpoint通话。所以说，Endpoint一般是跟通话相关的。

### mod_sofia
`mod_sofia`实现了SIP中的`注册服务器`、`重定向服务器`、`媒体服务器`、`呈现服务器`、`SBC`等各种功能。它的定位是一个`B2BUA`，它不能实现SIP代理服务器的功能。

### SIP Profile
在mod_sofia中，有一个概念是`SIPProfile`，它相当于一个`SIPUA`，通过各种不同的配置参数可以配置一个`UA`的行为。 一个系统中可以有多个`SIP Profile`，每个`SIP Profile`都可以监听不同的`IP地址`和`端口对`。

### Gateway
一个SIP Profile中有多个`Gateway`，`Gateway`可以直译为`网关`，它主要用于定义一个远端的SIP服务器，使FreeSWITCH可以与其他服务器通信。FreeSWITCH可以作为一个SIP客户端（UAC）向远端的网关进行注册；当然也可以不注册，而是使用与远端服务器对等的方式（俗称`SIPTrunk`，即`SIP中继`）相互通信。

### 本地SIP用户
FreeSWITCH可以作为注册服务器，这时候，其他的SIP客户端就可以向它注册。FreeSWITCH将通过用户目录 （`Directory`）中的配置信息对注册用户进行鉴权。这些SIP客户端所代表的用户就称为本地SIP用户，简称`本地用户`。

### 来话和去话
牢记FreeSWITCH是一个`B2BUA`。如果Alice通过FreeSWITCH给Bob打电话，Alice首先向FreeSWITCH发起呼叫，对FreeSWITCH而言，这路通话就称为`来话`（`InboundCall`）；然后 FreeSWITCH再去呼叫B，这路通话称为`去话`（`OubtoundCall`）。如果 来、去话都是本地的，又称为本地来话和本地去话。

### 中继来话或中继去话
如果来、去话不是本地的，双方通话需要以`中继`方式进行，就称为`中继来话`或`中继去话`。但是，中继的叫法只是沿用传统的PSTN网络中的概念，在SIP术语中，本来是没有中继的概念的。


## Sofia配置文件
Sofia的配置文件是`conf/autoload_configs/sofia.conf.xml`，不过一般不需要直接修改它，因为该文件仅有少数的配置参数，大部分的配置
参数实际上是直接在上述配置文件中使用下面的预处理指令装入 `conf/sip_profiles/`目录中的XML文件中的配置
```xml
<X-PRE-PROCESS cmd="include" data="../sip_profiles/*.xml"/>
```
Sofia的配置文件的总体结构应该是这样的：
```xml
<configuration name="sofia.conf" description="sofia Endpoint">    
    <global_settings>        
    <!-- 全局参数设置 -->    
    </global_settings>    
    <profiles>        
    <profile name="profile1">        
    </profile>        
    <profile name="profile2">        
    </profile>    
    </profiles> 
</configuration>
```
`global_settings`中存放了一些全局配置参数。下面的`profiles`标签中又包含多个`profile`标签。每个`profile`标签的详细信息都是在`conf/sip_profiles/`下的配置文件中配置的。

`Sofia`支持多个`Profile`，而每个`Profile`相当于一个`SIP UA`，在启动后它会监听一个`“IP地址:端口”对`。在讲`B2BUA`的概念时，实际上只用到了一个`Profile`，也就是一个`UA`，还是说FreeSWITCH启动了两个`UA`（一对背靠背的`UA`）来为Alice和Bob服务。从物理来讲，它确实只是一个`UA`，但由于它同时支持多个`Session`，在逻辑上就是相当于两个`UA`，FreeSWITCH中UA的含义了——简单来讲，一个`“IP地址:端口”对`唯一标志一个`UA`。

FreeSWITCH默认的配置带了三个Profile（也就是三个UA），仅讨论`internal`和`external`两个（它们分别是在`internal.xml`和`external.xml`中定义的）。不要被它们的名字所迷惑，其实`internal`和`external`最大的区别就是一个运行在`5060`端口上， 另一个运行在`5080`端口上。

### Profile配置文件

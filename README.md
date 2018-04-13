# freeSWITCH

- [install](install.md)
- [start](install.md)


## 什么是 `FreeSWITCH` ？
FreeSWITCH 是一个开源的电话交换平台，它具有很强的可伸缩性--从一个简单的软电话客户端到运营商级的软交换设备几乎无所不能。能原生地运行于Windows、 Max OS X、Linux、BSD 及 solaris 等诸多32/64位平台。可以用作一个简单的交换引擎、一个PBX，一个媒体网关或媒体支持IVR的服务器等。它支持SIP、H323、Skype、Google Talk等协议，并能很容易地与各种开源的PBX系统如sipXecs、Call Weaver、Bayonne、YATE及Asterisk等通信。 FreeSWITCH 遵循RFC并支持很多高级的SIP特性，如 presence、BLF、SLA以及TCP、TLS和sRTP等。它也可以用作一个SBC进行透明的SIP代理（proxy）以支持其它媒体如T.38 等。FreeSWITCH 支持宽带及窄带语音编码，电话会议桥可同时支持8、12、16、24、32及48kHZ的语音. 而在传统的电话网络中，要做到三方通话或多方通话需要通过专门的芯片来处理，其它像预付费，彩铃等业务在PSTN网络中都需要依靠智能网(IN)才能实现，而且配置起来相当不灵活。

## 快速体验
FreeSWITCH 的功能确实非常丰富和强大，在进一步学习之前我们先来做一个完整的体验。FreeSWITCH 默认的配置是一个SOHO PBX(家用电话小交换机)，那么我们本章的目标就是从0安装，实现分机互拨电话，测试各种功能，并通过添加一个SIP-PSTN网关拨打PSTN电话。这样，即使你没有任何使用经验，你也应该能顺利走完本章，从而建立一个直接的认识。在体验过程中，你会遇到一点稍微复杂的配置，如果不能完全理解，也不用担心，我们在后面会详细的介绍。当然，如果你是一个很有经验的 FreeSWITCH 用户，那么大可跳过本章。

> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.51cto.com](https://blog.51cto.com/victorly/2337272)

> tacacs 协议, TACACS + 协议，TACACS+(TerminalAccessControllerAccessControlSystem) 终端访问控制器访问控制系统。

© 著作权归作者所有：来自 51CTO 博客作者 msft 的原创作品，如需转载，请注明出处，否则将追究法律责任  
[TACACS + 协议](https://blog.51cto.com/victorly/2337272)  
[https://blog.51cto.com/victorly/2337272](https://blog.51cto.com/victorly/2337272)

TACACS+(Terminal Access Controller Access Control System) 终端访问控制器访问控制系统。与我们 IDsentrie 的 Radius 协议相近。不过 TACACS + 用的是 TCP 协议，Radius 用的是 UDP。它们的重要作用就是 3A。 所谓 3A, 即 Authentication 认证，Authorization 授权， Accounting 计费。

TACACS + 协议报文类型  
TACACS + 共有 7 种类型的消息：  
认证：  
1、Authentication_START  
2、Authentication_CONTIUNE  
3、Authentication_REPLY  
授权：  
4、Authorization_REQUEST  
5、Authorization_RESPONSE  
计费：  
6、Accounting_REQUEST  
7、Accounting_REPLY
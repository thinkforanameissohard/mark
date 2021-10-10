> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [www.cnblogs.com](https://www.cnblogs.com/wangliangblog/p/5198535.html)

1 、TACACS + 概述
==============

1.1   什么是 TACACS+
-----------------

TACACS+（Terminal Access Controller Access Control System，终端访问控制器控制系统协议）是在 TACACS 协议的基础上进行了功能增强的安全协议。该协议与 RADIUS 协议的功能类似，采用客户端 / 服务器模式实现 NAS 与 TACACS + 服务器之间的通信。

1.2  TACACS + 的用途
-----------------

TACACS + 协议主要用于 PPP 和 VPDN（Virtual Private Dial-up Network，虚拟私有拨号网络）接入用户及终端用户的 AAA。AAA 是 Authentication、Authorization、Accounting（认证、授权、计费）的简称，是网络安全的一种管理机制，提供了认证、授权、计费三种安全功能。

认证：确认访问网络的远程用户的身份，判断访问者是否为合法的网络用户。

授权：对不同用户赋予不同的权限，限制用户可以使用的服务。例如用户成功登录服务器后，管理员可以授权用户对服务器中的文件进行访问和打印操作。

计费：记录用户使用网络服务中的所有操作，包括使用的服务类型、起始时间、数据流量等，它不仅是一种计费手段，也对网络安全起到了监视作用。

2、 TACACS + 协议介绍
================

2.1 TACACS + 基本消息交互流程
---------------------

下图是 TACACS + 协议的基本信息交互流程：

 ![](https://images2015.cnblogs.com/blog/317564/201602/317564-20160218174952050-1769127725.jpg)

以 Telnet 用户认证过程为例，基本消息交互流程如下：

(1) Telnet 用户请求登录设备。

(2) TACACS + 客户端收到请求之后，向 TACACS + 服务器发送认证开始报文。

(3) TACACS + 服务器发送认证回应报文，请求用户名。

(4) TACACS + 客户端收到回应报文后，向用户询问用户名。

(5) 用户输入用户名。

(6) TACACS + 客户端收到用户名后，向 TACACS + 服务器发送认证持续报文，其中包括了用户名。

(7) TACACS + 服务器发送认证回应报文，请求登录密码。

(8) TACACS + 客户端收到回应报文，向用户询问登录密码。

(9) 用户输入密码。

(10) TACACS + 客户端收到登录密码后，向 TACACS + 服务器发送认证持续报文，其中包括了登录密码。

(11) TACACS + 服务器发送认证回应报文，指示用户通过认证。

(12) TACACS + 客户端向 TACACS + 服务器发送授权请求报文。

(13) TACACS + 服务器发送授权回应报文，指示用户通过授权。

(14) TACACS + 客户端收到授权回应成功报文，向用户输出设备的配置界面。

(15) TACACS + 客户端向 TACACS + 服务器发送计费开始报文。

(16) TACACS + 服务器发送计费回应报文，指示计费开始报文已经收到。

(17) 用户请求断开连接。

(18) TACACS + 客户端向 TACACS + 服务器发送计费结束报文。

(19) TACACS + 服务器发送计费结束报文，指示计费结束报文已经收到。

2.2 TACACS + 消息类型
-----------------

由 2.1 可知 TACACS + 共有 7 种类型的消息：

1、Authentication_START

2、Authentication_CONTIUNE

3、Authentication_REPLY

4、Authorization_REQUEST

5、Authorization_RESPONSE

6、Accounting_REQUEST

7、Accounting_REPLY

由于我们只关心认证流程所以只涉及到以上的 1、2、3 类型报文及 TACACS + 报文头，共计四中类型的报文，以下分别对其报文结构加以说明。

2.3  TACACS + 报文结构
------------------

### 2.3.1  TACACS + 报文头

所有的 TACACS + 数据包都使用 12 字节长的包头，结构如下：

 ![](https://images2015.cnblogs.com/blog/317564/201602/317564-20160218175042675-212200999.jpg)

下面对各个字段分别进行说明：

1)  Major：TACACS + 主版本号，取值为 0x0C

2)  Minor：TACACS + 次版本号，用于向后兼容扩展，一般为 0。

3)  Packet Type: 定义包的类型，取值：

#define TAC_PLUS_AUTHEN         1     // authentication 表示认证

#define TAC_PLUS_AUTHOR         2     // authorization 表示授权

#define TAC_PLUS_ACCT           3     // accounting 表示计费

4)  Sequence No: 当前会话中的数据包序列号。会话中的第一个 TACACS + 数据包序列号必须为 1，其后的每个数据包序列号逐次加 1。因此客户机只发送奇序列号数据包，而 TACACS+ Daemon 只发送偶序列号数据包。当序列号达到 255 时， 会话会重启并置回序列号为 1。

5)  Flags：用来示一些特殊条件，比如不加密（0x01），支持单连接多会话（0x04）等

6)  Session_id：为 TACACS + 会话的 ID，是个随机数。

7) Length：为 TACACS + 报文除头部之外的长度

### 2.3.2  Authentication 消息

TACACS + 认证有三种类型数据包：开始 (START)、继续(CONTINUE) 和回复 (REPLY)。客户端(client) 发送 START 和 CONTINUE 数据包，服务端 (daemon) 发送 REPLY 数据包。

    认证开始时，客户端发送一个 START 消息到服务端，该消息描述了要执行的身份验证类型，可能还包括用户名和一些认证数据。起始数据包仅作为 TACACS + 舍话开始或者会话重置后紧接着的第一个消息（会话重置可能是由服务端的回复包发起的）。起始数据包的序列号总是等于 1。服务端发送一个 REPLY 包以响应 START 包。回复包表明认证是否结束或者继续。如果认证继续，则回复包将指明所需要的新的认证信息。客户端取出相关信息并以 CONTINUE 包的形式进行返回。服务端以 REPLY 包来回复 START 包或者 CONTINUE 包，直到客户端在 CONTINUE 包指示要中止，此时会话将立即中止。

#### 2.3.2.1 认证 START 报文格式：

 ![](https://images2015.cnblogs.com/blog/317564/201602/317564-20160218175108503-647975956.jpg)

1) Action: 认证操作，合法值为：

TAC_PLUS_AUTHEN_LOGIN  =  Ox01 (甏录)

TAC PLUS ALTTHEN CHPASS=Ox02（修改密码）

TAC PLUS AUTHEN SENDPASS=Ox03（发送密码，已作废）

TAC PLUS AUTHEN SENDAUTH=Ox04（发送认证）

2) Priv lVl：认证权限级别，值域为 0-15，可以在 NAS 客户端中设置，预设值为：

TAC PLUS PRIV LVL MAX=OxOf（最高级别）

TAC_PLUS_PRIV_LVL_ROOT=OxOf (ROOT 用户级别)

TAC PLUS PRIV LVL USER=Ox01（普通用户级别）

TAC PLUS PRIV LVL MIN=Ox00（最低级别）

3) Authen_type: 认证类型，合法值为：

TAC_PLUS_AUTHEN_TYPE_ASCII  =  Ox01 (ASCII 值)

TAC_PLUS_AUTHEN_TYPE_PAP  =  Ox02 (PAP 伤 iX)

TAC_PLUS_AUTHEN_TYPE_CHAP  =  Ox03 (CHAP 协 iX)

TAC_PLUS_AUTHEN_TYPE_ARAP  =   Ox04 (ARAP 协议)

TAC PLUS AUTHEN TYPE MSCHAP=Ox05（微软 CHAP 协议）

4) Service: 认证服务，合法值为：

TAC_PLUS_AUTHEN_SVC_NONE  =  Ox00 c 无服务 )

TAC_PLUS_AUTHEN_SVC_LOGIN  =  Ox01(登录)

TAC_PLUS_AUTHEN_SVC_ENABLE = Ox02 (enable 服务)

TAC_PLUS_AUTHEN_SVC_PPP  =  Ox03 (PPP 协议)

TAC_PLUS_AUTHEN_SVC_ARAP  =  Ox04 (ARAP 协 iX)

TAC PLUS AUTHEN SVC PT=Ox05（负载类型）

TAC PLUS AUTHEN SVC RCMD=Ox06（远程命令）

TAC_PLUS_AUTHEN_SVC_X25 = Ox07 (x. 25 协 iX)

TAC_PLUS_AUTHEN_SVC_NASI  =  Ox08 (NASI 服务)

TAC_PLUS_AUTHEN _SVC_FWPROXY=Ox09（防火墙代理）

其中 ENABLE 服务是指获得管理特权，类似于 Linux 系统中的 “su” 命令。NONE 服务是在没有任何其它服务的情况下填写的。

5) User: 用户名，可选值。

6) Port：客户端认证所使用的端口，由客户端指定。

7) Rem addr: 远程地址，可选值，由客户端指定。

8) Data: 负载数据。

#### 2.3.2.2 认证 REPLY 报文格式：

 ![](https://images2015.cnblogs.com/blog/317564/201602/317564-20160218175127269-612572513.jpg)

1) Status: 认证当前状态，合法值为：

TAC_PLUS_AUTHEN_STATUS_PASS  =  Ox01(通过)

TAC_PLUS_AUTHEN_STATUS_FAIL  =  Ox02 (失败)

TAC PLUS AUTHEN STATUS GETDATA=Ox03（获取数据）

TAC PLUS AUTHEN STATUS GETUSER=Ox04（获取用户名）

TAC PLUS AUTHEN STATUS GETPASS=Ox05（获取密码）

TAC PLUS AUTHEN STATUS RESTART=Ox06（重启会话）

TAC_PLUS_AUTHEN_STATUS_ERROR = Ox07(错误)

TAC_PLUS_AUTHEN_STATUS_FOLLOW   =   Ox21 (使用备用  deamon)

2) Flags: 该字段包括各种位图格式的标志，定义值：

TAC PLUS REPLY FLAG NOECHO = Ox01 应)

3) Server_msg: 服务器返回给用户的提示信息，可选的。

4) Data: 负载数据。

#### 2.3.2.3 认证 CONTINUE 报文格式

 ![](https://images2015.cnblogs.com/blog/317564/201602/317564-20160218175138050-1654735589.jpg)

1) Flags: 该字段包括各种位图格式的标志，定义值：

TAC PLUS CONTINUE FLAG ABORT = Ox01c 中止)

2) User_msg: 用户输入信息，用于答复 Server_msg。

3) Data: 负载数据。

2.4 各类认证类型详解
------------

    Tacacs + 认证协议支持 ASCII 值、PAP、CHAP、 ARAP 协议、MS-CHAP 等五种认证类型，现分别对其进行分析。

### 2.4.1 ASII 值认证类型

         ASII 认证类型在认证流程中共包含 START 报文、REPLY 报文和 CONTINUE 报文，其中 START 报文中可以携带用户名信息也可以不携带（在 continue 中携带），具体流程如下：

![](https://images2015.cnblogs.com/blog/317564/201602/317564-20160218175247909-158228954.gif) 

图 2-4-1-1 start 报文不含用户信息认证流程

![](https://images2015.cnblogs.com/blog/317564/201602/317564-20160218175305581-1110928657.gif) 

图 2-4-1-2 start 报文包含用户信息认证流程

### 2.4.2 PAP 协议认证类型

    PAP 认证类型只包含一个 START 报文和一个 REPLY 报文，START 报文必须包含用户名信息和密码信息，其中用户名信息存储在 START 报文的 user 字段，密码存储在 START 报文的 data 字段，数据信息不需加密，认证流程如下：

 ![](https://images2015.cnblogs.com/blog/317564/201602/317564-20160218175330128-356434572.gif)

图 2-4-2-1 PAP 协议类型认证流程

### 2.4.3 CHAP 协议认证类型

CHAP 认证类型只包含一个 START 报文和一个 REPLY 报文，START 报文必须包含用户名信息和数据信息，其中用户名信息存储在 START 报文的 user 字段，数据存储在 START 报文的 data 字段，数据信息必须包含 session_id、challenge 和 authentication。

    session_id 必须占用 1 个字节，authentication 必须用 16 个字节，challenge 长度等与 data 总长度减去 session_id 长度和认证信息长度，authentication 是由 session_id、用户密码和 challenge 通过 MD5 加密生成。具体认证流程如下：

![](https://images2015.cnblogs.com/blog/317564/201602/317564-20160218175344191-839699945.gif) 

图 2-4-3-1 CHAP 协议类型认证流程

<table border="0" cellspacing="0" cellpadding="0"><tbody><tr><td width="87"><p align="left">session_id</p></td><td width="80"><p align="left">challenge</p></td><td width="365"><p align="left">authentication</p></td></tr><tr><td width="87"><p align="left">1 byte</p></td><td width="80">&nbsp;</td><td width="365"><p align="left">16 bytes,auth=MD5(se_id,usr_pwd,challenge)</p></td></tr></tbody></table>

图 2-4-3-2 START 报文 data 字段数据结构

### 2.4.4 MS-CHAP 协议认证类型

MS-CHAP 认证类型只包含一个 START 报文和一个 REPLY 报文，START 报文必须包含用户名信息和数据信息，其中用户名信息存储在 START 报文的 user 字段，数据存储在 START 报文的 data 字段，数据信息必须包含 session_id、MS-challenge 和 MS-authentication。

    session_id 必须占用 1 个字节，authentication 必须用 49 个字节，challenge 长度等与 data 总长度减去 session_id 长度和 authentication 长度，认证信息是由用户密码、challenge 等通过 MD4 和 DES 加密生成。具体认证流程如下：

 ![](https://images2015.cnblogs.com/blog/317564/201602/317564-20160218175509597-694646977.gif)

图 2-4-4-1 MS-CHAP 协议类型认证流程

<table border="0" cellspacing="0" cellpadding="0"><tbody><tr><td width="87"><p align="center">session_id</p></td><td width="95"><p align="center">challenge</p></td><td width="365"><p align="center">authentication</p></td></tr><tr><td width="87"><p align="center">1 byte</p></td><td width="95">&nbsp;</td><td width="365"><p align="center">49bytes</p></td></tr></tbody></table>

图 2-4-4-2 START 报文 data 字段数据结构

<table border="0" cellspacing="0" cellpadding="0"><tbody><tr><td width="547"><p align="center">MS-CHAPv1 协议 authentication 组成</p></td></tr><tr><td width="547"><p align="center">NTHASH=MD4(user_pwd)</p></td></tr><tr><td width="547"><p align="center">ChallengeResponse=DES(NTHASH[0-7]、challenge)||DES(NTHASH[7-14]、challenge)||DES(NTHASH[14-21]、challenge)；challenge 一般为 8 字节</p></td></tr><tr><td width="547"><p align="center">ChallengeResponse 封装在 authentication 的 [24-47] 字节中, 并且 authentication 最后一个字节（49 字节）值为 1</p></td></tr></tbody></table>

图 2-4-4-3 MS-CHAPv1authentication 组成

<table border="0" cellspacing="0" cellpadding="0"><tbody><tr><td width="547"><p align="center">MS-CHAPv2 协议 authentication 组成</p></td></tr><tr><td width="547"><p align="center">NTHASH=DES(toupper(user_pwd),MS-KEY(KGS!@#$%))</p></td></tr><tr><td width="547"><p align="center">ChallengeResponse=DES(NTHASH[0-7]、challenge)||DES(NTHASH[7-14]、challenge)||DES(NTHASH[14-21]、challenge)；challenge 一般为 16 字节</p></td></tr><tr><td width="547"><p align="center">ChallengeResponse 封装在 authentication 的 [0-23] 字节中, 并且 authentication 最后一个字节（49 字节）值为 0</p></td></tr></tbody></table>

图 2-4-4-4 MS-CHAPv2 authentication 组成

### 2.4.5  ARAP 协议认证类型

ARAP 认证类型只包含一个 START 报文和一个 REPLY 报文，START 报文必须包含用户名信息和数据信息，其中用户名信息存储在 START 报文的 user 字段，数据存储在 START 报文的 data 字段，数据信息必须包含 ServerChallenge、ClientChallenge 和 authentication。

    ServerChallenge、ClientChallenge 和 authentication 都只占用 8 个字节，authentication 是由用户密码作为 DES_KEY 对 ServerChallenge 和 ClientChallenge 进行 DES 加密生成。具体认证流程如下：

图 2-4-5-1 ARAP 协议认证流程

<table border="0" cellspacing="0" cellpadding="0"><tbody><tr><td width="114"><p align="center">ServerChallenge</p></td><td width="115"><p align="center">ClientChallenge</p></td><td width="174"><p align="center">authentication</p></td></tr><tr><td width="114"><p align="center">8byte</p></td><td width="115"><p align="center">8 字节</p></td><td width="174"><p align="center">8bytes</p></td></tr></tbody></table>

图 2-4-5-2 START 报文 data 字段数据结构

<table border="0" cellspacing="0" cellpadding="0"><tbody><tr><td width="547"><p align="center">ARAP 协议 authentication 组成</p></td></tr><tr><td width="547"><p align="center">KEY=pwd 各个字节分别左移一位</p></td></tr><tr><td width="547"><p align="center">ChallengeResponse=DES(ServerChallenge，KEY)；challenge 一般为 8 字节</p></td></tr></tbody></table>

图 2-4-5-3 ARAP authentication 组成

2.5  TACACS + 数据包的加密
--------------------

TACACS + 支持除包头之外所有信息的加密，加密方法如下：

1) 将 session_id、secret key, 版本号和 sequence number 一起进行 MD5 运算（其中 secret key 为 TACACS 客户端和服务器之间的共享秘密），计算结果为 MD5_1。

2) 后续的 MD5 运算将上次 MD5 运算的结果也纳入运算范围，如下：

MD5_1 = MD5{session_id, key, version, seq_no}

MD5_2 = MD5{session_id, key, version, seq_no, MD5_1}

....

MD5_n = MD5{session_id, key, version, seq_no, MD5_n-1}

3) 将所有的运算结果连接起来，直到总长度大于需要加密的数据的长度，然后截断到实际数据的长度，得到 pseudo_pad：

pseudo_pad = {MD5_1 [,MD5_2 [ ... ,MD5_n]]} truncated to len(data)

4) 随后将需要加密的数据和上面的 pseudo_pad 进行 XOR 运算，得到密文：

ENCRYPTED {data} == data ^ pseudo_pad

由于 TACACS + 对整个数据包进行加密，私密性要好于 RADIUS，窃听者无法根据报文的内容来猜测网络的配置和用户的身份。

3、TACACS + 服务器环境配置
==================

1.  硬软件要求
---------

硬件：Pentium IV 处理器， 1.8 GHz 或者更高   
操作系统：Windows 2000 Server 、Windows Server 2003， Enterprise Edition or Standard   
Edition (Service Pack 1)   
内存：最小 1GB   
虚拟内存：最小 1GB   
硬盘空间：最小 1GB 可用空间，实际大小根据日志文件的增长，复制和备份的需求而定。 

2. 软件要求
-------

浏览器：Microsoft Internet Explorer 6 或者更高版本  
 JAVA 运行环境：Sun JRE 1.4.2_04 或更高版本  
TACACS + 服务器：安装 cisco ACS
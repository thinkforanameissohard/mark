> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.csdn.net](https://blog.csdn.net/qq_43561370/article/details/111814842)

> IPSec文章目录`IPSec`简介`IPsec`的应用`IPsec`优势安全架构`IPsec`在`IP`层提供的服务`IPsec`的两种模式`IPsec`中的安全组合(SA)安全关联一个安全关联由三个参数唯一确定`IPsec`通信协议AH(Authentication Header)ESP协议AH和ESP的对比`IPsec`建立过程`IKE`协商`IKE`第一阶段`IKE`第二阶段`IKE`和`AH/ESP`之前的联系数据传输阶段概述VPN隧道黑洞参考博客参考博客简介Internet Protoc

`IPSec`
-------

### 文章目录

*   *   [`IPSec`](#IPSec_0)
    *   *   [简介](#_3)
        *   [`IPsec` 的应用](#IPsec_9)
        *   [`IPsec` 优势](#IPsec_16)
        *   [安全架构](#_22)
        *   [`IPsec` 在 `IP` 层提供的服务](#IPsecIP_30)
        *   [`IPsec` 的两种模式](#IPsec_38)
        *   [`IPsec` 中的安全组合 (SA)](#IPsecSA_57)
        *   *   [安全关联](#_62)
            *   [一个安全关联由三个参数唯一确定](#_68)
        *   [`IPsec` 通信协议](#IPsec_77)
        *   *   [AH(Authentication Header)](#AHAuthentication_Header_79)
            *   [ESP 协议](#ESP_90)
            *   [AH 和 ESP 的对比](#AHESP_109)
        *   [`IPsec` 建立过程](#IPsec_120)
        *   *   [`IKE` 协商](#IKE_122)
            *   [`IKE` 第一阶段](#IKE_133)
            *   [`IKE` 第二阶段](#IKE_146)
            *   [`IKE` 和 `AH/ESP` 之前的联系](#IKEAHESP_165)
            *   [数据传输阶段](#_172)
            *   *   [概述](#_174)
                *   [VPN 隧道黑洞](#VPN_179)
        *   [参考博客](#_197)

### 简介

> **Internet Protocol Security** (**IPsec**) 是一个安全网络协议套件，它可以完成认证加密数据包，从而为 IP 层网络设备提供安全加密通信。IPSec 还被用到了 VPN 中。
> 
> IPsec 包括了用于在客户端之间开始会话前建立相互认证和会话所用秘钥分发的协议簇。IPsec 可以保护数据流在端到端，网络到网络，端到网络之间。IPsec 使用密码安全服务来保护 IP 网络中的通信。它支持网络层对等身份认证，数据源认证，数据加密和重放保护。

### `IPsec`的应用

*   加密应用层数据
*   在公共互联网上为路由器发送数据提供安全保障
*   在不加密的情况下进行身份认证，比如验证来自一个已知发送者的数据报
*   通过使用 `IPsec` 隧道设置电路来保护网络数据，在这些电路中，所有数据在两个端点之间发送时都被加密，就像使用虚拟专用网络 (VPN) 连接一样

### `IPsec`优势

*   在路由器和防火墙中使用`IPsec`，对通过其边界的所有通信流提供强安全性，内部通信无安全开销
*   位于传输层之下，对所有应用透明
*   可以对终端用户透明，不需要对用户进行安全机制培训

### 安全架构

​ `IPsec`是一个开放的组件，是 IPv4 套件的一部分。`IPsec`使用了下面的这些协议实现各种各样的功能。

*   [Authentication Headers (AH)](https://en.wikipedia.org/wiki/IPsec#Authentication_Header) 提供无连接数据完整性及为 IP 数据报提供数据源认证，同时为重放攻击提供保护（这里防止重放是用序列号，其他情况下可能使用时间戳的形式）。
*   [Encapsulating Security Payloads (ESP)](https://en.wikipedia.org/wiki/IPsec#Encapsulating_Security_Payload) (封装安全有效负载) 提供加密，无连接数据完整性，数据源认证，抗重放共计，和有限的流量保密性。
*   [Security Associations (SA)](https://en.wikipedia.org/wiki/IPsec#Security_association) 提供算法和数据包，这些算法和数据包提供 AH 和 ESP 所需的参数。互联网安全协会和秘钥管理协议`(ISAKMP)`提供了用于身份验证和秘钥交换的框架，带有通过手动配置的预共享密钥，Internet 密钥交换（IKE 和 IKEv2），Kerberized Internet 密钥协商（KINK）或 IPSECKEY DNS 记录提供的实际经过身份验证的密钥材料。

### `IPsec`在`IP`层提供的服务

*   访问控制
*   无连接的完整新
*   数据来源验证
*   防重放攻击
*   加密和数据流分类加密

### `IPsec`的两种模式

*   传送模式
    *   当协议在一台主机上实现时使用，`IPsec`头部被插在`IP`头后面。主要为上层协议提供保护，加密和可选择的认证，用于在两个主机之间进行端到端通信。

![](https://img-blog.csdnimg.cn/20201227160324611.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNTYxMzcw,size_16,color_FFFFFF,t_70#pic_center)

*   隧道模式
    *   整个包被封装加密，形成新的`IP`头部。沿途路由器不检查内部的`IP`报头。
    *   适用于隧道结束在某个非目的地 (安全网关，防火墙) 该目的地结束`IPsec`隧道，还原成原来数据包在本地网（局域网）传输（局域网不用理解`IPsec`）
    *   隧道模式的另一个好处是可以将聚集`TCP`连接当成一个流加密。可以抵抗 traffic analysis
    *   加密发生在外部主机与安全网关之间或者发生在两个安全网关之间。

![](https://img-blog.csdnimg.cn/20201227160314582.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNTYxMzcw,size_16,color_FFFFFF,t_70#pic_center)

### `IPsec`中的安全组合 (SA)

*   本质上位一个安全通信信道提供的一套安全参数，是单向的，需要双向则两个关联
*   SA 是通过密钥管理协议在通信双方之间进行协商，协商完毕之后，双方都在它们的安全关联数据库中存储该 SA 参数

#### 安全关联

> 通信双方对某些要素之间的协定，包括：
> 
> 加密算法和模式 加密秘钥 加密参数（如初始化向量），鉴别协议和秘钥，关联的生命期（长时间会话时，尽可能频繁的选择新的加密密钥），关联对应端地址，受保护数据敏感级别。

#### 一个安全关联由三个参数唯一确定

*   安全参数索引
    *   指向一张安全关联表指针，由 AH 和 ESP 报头携带，使得接受系统选择合适的 SA
*   IP 目的地址
    *   目前仅允许单播地址，是 SA 的目的端点地址
*   安全协议标识
    *   表明是 AH 还是 ESP

### `IPsec`通信协议

#### AH(Authentication Header)

*   无连接数据完整性：通过哈希函数产生的校验来保证
*   数据源认证：通过在计算验证码时加入一个共享秘钥来实现
*   抗重放服务：AH 头部中的序列号可以防止重放攻击

AH 的协议号是 51，AH 头比 ESP 头简单很多，因为它不提供机密性，不会加密所保护的数据报。不论是在传输模式还是在隧道模式下，AH 提供对数据报的保护时，它保护的是整个 IP 数据包（易变的字段除外，如 IP 头中的 TTL 和 TOS 字段）

![](https://img-blog.csdnimg.cn/20201227160259890.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNTYxMzcw,size_16,color_FFFFFF,t_70#pic_center)

#### ESP 协议

*   无连接数据完整性
*   数据源认证
*   抗重放攻击
*   数据保密：密码算法加密 IP 数据包
*   有限的数据流保护：由隧道模式下的保密服务提供

ESP 通常使用 DES、3DES、AES 等加密算法实现数据加密，使用 MD5 或 SHA1 来实现数据完整性认证。

ESP 同样被当做一种 IP 协议对待，紧贴在 ESP 头前的 IP 头，协议号为 50.

![](https://img-blog.csdnimg.cn/20201227160250376.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNTYxMzcw,size_16,color_FFFFFF,t_70#pic_center)

*   在隧道模式中，ESP 保护整个 IP 包，整个 IP 包将会以 ESP 载荷的方式加入新建的数据包，同时，系统根据隧道起点和终点等参数，建立一个隧道 IP 头，作为这个数据包的新 IP 头，ESP 头夹在隧道 IP 头和原始 IP 头之间，并点缀 ESP 尾。
*   ESP 提供加密服务，所以原始 IP 包和 ESP 尾以密文的形式出现。
*   ESP 在验证过程中，只对 ESP 头部、原始数据包 IP 包头、原始数据包数据进行验证；只对原始的整个数据包进行加密，而不验证数据。

#### AH 和 ESP 的对比

*   ESP 在隧道模式不验证外部 IP 头，因此 ESP 在隧道模式下可以在 NAT 环境中运行
*   ESP 在传输模式下会验证外部 IP 头部，将导致校验失败
*   AH 因为提供数据来源确认（源 IP 地址一旦改变，AH 校验失败），所以无法穿越 NAT

![](https://img-blog.csdnimg.cn/20201227160240108.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNTYxMzcw,size_16,color_FFFFFF,t_70#pic_center)  
ESP 认证数据：是变长字段，只有选择了验证服务时才需要有该字段。

很多情况下，AH 的功能已经能满足安全的需要，ESP 由于需要使用高强度的加密算法，需要消耗更多的计算机运算资源，使用上受到一定限制。

### `IPsec`建立过程

#### `IKE`协商

*   `IPsec`的密钥管理：密钥的确定和分发
    *   典型的两个应用之间的通信需要 4 个密钥：用于完整性和机密性的发送对和接受对。
*   `IPsec`支持两种方式的`SA`建立和秘钥管理
    *   手工方式
    *   自动方式（IKE 协商）
        *   SA 可以通过协商方式产生
        *   SA 过期以后重新协商，提高了安全性
        *   适用于较为复杂的拓扑和较高安全性的网络

#### `IKE`第一阶段

![](https://img-blog.csdnimg.cn/20201227160112611.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNTYxMzcw,size_16,color_FFFFFF,t_70#pic_center)

*   用途
    *   协商创建一个通信信道 (IKE SA)
    *   对该信道进行认证
    *   为双方进一步的 IKE 通信提供机密性、数据完整性以及数据源认证服务
*   步骤
    *   策略协商
    *   DH 交换
    *   认证

#### `IKE`第二阶段

![](https://img-blog.csdnimg.cn/20201227160102617.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNTYxMzcw,size_16,color_FFFFFF,t_70#pic_center)

*   用途
    *   协商建立`IPsec SA`，为数据交换提供`IPsec`服务
*   步骤
    *   策略协商
    *   会话秘钥 “材料’刷新或交换产生 Ipsec 的认证和加密密钥
    *   SA 和密钥连同 SPI，递交给 IPSEC 驱动程序

> 1. 安全联盟 SA(Security Association)：是两个 IPSec 通信实体之间经协商建立起来的一种共同协定，它规定了通信双方使用哪种 IPSec 协议保护数据安全、应用的算法标识、加密和验证的密钥取值以及密钥的生存周期等等安全属性值。通过使用安全关联 (SA) ， IPSec 能够区分对不同的数据流提供的安全服务。  
> 2.IPSec 是在两个端点之间提供安全通信，端点被称为 **IPSec 对等体**。IPSec 能够允许系统、网络的用户或管理员控制对等体间安全服务的**粒度**。通过 SA（Security Association），IPSec 能够对不同的数据流提供不同级别的安全保护。  
> 3. **安全联盟**是 IPSec 的基础，也是 IPSec 的本质。SA 是通信对等体间对某些要素的约定，例如，使用哪种安全协议、协议的操作模式（传输模式和隧道模式）、加密算法（DES 和 3DES）、特定流中保护数据的共享密钥以及密钥的生存周期等。  
> 4. 安全联盟是**单向**的，在两个对等体之间的**双向通信**，**最少需要两个安全联盟**来分别对两个方向的数据流进行安全保护。入站数据流和出站数据流分别由入站 SA 和出站 SA 进行处理。同时，如果希望同时使用 AH 和 ESP 来保护对等体间的数据流，则分别需要两个 SA，一个用于 AH，另一个用于 ESP。  
> 5. 安全联盟由一个**三元组**来唯一标识，这个三元组包括**安全参数索引**（SPI, Security Parameter Index）、**目的 IP 地址**、**安全协议号（AH 或 ESP）**。SPI 是为唯一标识 SA 而生成的一个 32 比特的数值，它在 IPSec 头中传输。  
> 6.IPSec 设备会把 SA 的相关参数放入 **SPD（Security Policy Database）** 里面，SPD 里面存放着 “什么数据应该进行怎样的处理” 这样的消息，在 IPSec 数据包出站和入站的时候会首先从 SPD 数据库中查找相关信息并做下一步处理。

#### `IKE`和`AH/ESP`之前的联系

`IKE`是`UDP`之上的一个应用层协议，是 IPsec 的信令协议。`IKE`为`IPsec`协商产生秘钥，供`AH/ESP`加解密和验证使用。`AH`协议和`ESP`协议有自己的协议号，分别为 51 和 50。

![](https://img-blog.csdnimg.cn/20201227160033369.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNTYxMzcw,size_16,color_FFFFFF,t_70#pic_center)

#### 数据传输阶段

##### 概述

数据传输阶段是通过 **AH** 或者 **ESP 通信协议**进行数据的传输。  
数据传输建立在**网络层**。

##### VPN 隧道黑洞

> **可能情况：**  
> 对端的 VPN 连接已经断开而我方还处在 SA 的有效生存期时间内，从而形成了 VPN 隧道的黑洞。  
> 另外一端如果之前 SA 没有释放，异常重启的对端又来连接，是不会接受新的连接协商的。
> 
> **DPD 解决 VPN 隧道黑洞：**  
> DPD：**死亡对等体检测（Dead Peer Detection）**，检查对端的 ISAKMP SA 是否存在。当 VPN 隧道异常的时候，能检测到并重新发起协商，来维持 VPN 隧道。  
> DPD **只对第一阶段生效**，如果第一阶段本身已经超时断开，则不会再发 DPD 包。  
> **DPD 包**并不是连续发送，而是采用**空闲计时器机制**。每接收到一个 IPSec 加密的包后就重置这个包对应 IKE SA 的空闲定时器；  
> 如果空闲定时器计时开始到计时结束过程都没有接收到该 SA 对应的加密包，那么下一次有 IP 包要被这个 SA 加密发送或接收到加密包之前就需要使用 DPD 来检测对方是否存活。  
> **DPD 检测**主要靠**超时计时器**，超时计时器用于判断是否再次发起请求，默认是发出 5 次请求（请求 -> 超时 -> 请求 -> 超时 -> 请求 -> 超时）都没有收到任何 DPD 应答就会删除 SA。
> 
> **检查对端的 ISAKMP SA 是否存在两种工作模式：**  
> 1. **周期模式**：每隔一段时间，向对端发送 DPD 包探测对等体是否仍存在，如果收到回复则证明正常。如果收不到回复，则会每隔 2 秒发送一次 DPD，如果发送七次仍收不到回复，则自动清除本地对应的 ISAKMP SA 和 IPSEC SA。  
> 2. **按需模式**：这是默认模式，当通过 IPSEC VPN 发送出流量而又收不到回程的数据时，则发出 DPD 探测包，每隔 2 秒发送一次，七次都收不到回应则清除本地对应的 ISAKMP SA 和 IPSEC SA。注意，如果 IPSEC 通道上如果跑的只有单向的 UDP 流量，则慎用这个模式，尽管这种情况极少。  
> DPD 很实用，应该开启。至于选择哪个模式，则根据实际需要，周期模式可以相对快地找出问题 peer，但较消耗带宽；按需模式，较节约带宽，但只有当发出加密包后收不到解密包才会去探测。

### 参考博客

[IPSec 介绍](https://blog.csdn.net/NEUChords/article/details/92968314)

鉴于本人能力有限，如有错误请不吝指正，万分感谢！  
可以参考下面这篇博客，看 ipsec 和 nat 冲突的解决方案

[NAT-T：IPsec 穿越 NAT 之道](https://blog.csdn.net/u014023993/article/details/86634339)
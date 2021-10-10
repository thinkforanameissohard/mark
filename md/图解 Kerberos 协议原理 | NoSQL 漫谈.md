> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [www.nosqlnotes.com](http://www.nosqlnotes.com/technotes/kerberos-protocol/)

> Kerberos 是一个常用的认证与授权协议，在初次接触该协议的时候，往往觉得该协议充满复杂的交互逻辑，但在充分理解了之后，又会觉得这过程中其实充满了数学与逻辑的美学。

[Skip to content](#content)

Kerberos 是一个常用的认证与授权协议，在初次接触该协议的时候，往往觉得该协议充满复杂的交互逻辑，但在充分理解了之后，又会觉得这过程中其实充满了数学与逻辑的美学。本文主要结合 Wiki 中关于 Kerberos Protocol 的定义，增加了一些图解信息，希望能够让读者更直观的理解该协议的内容。  

整体流程
----

![](http://www.nosqlnotes.com/wp-content/uploads/2017/12/%E8%AE%A4%E8%AF%81%E4%B8%8E%E9%89%B4%E6%9D%83%E6%95%B4%E4%BD%93%E6%B5%81%E7%A8%8B.png)

参与的关键角色
-------

![](http://www.nosqlnotes.com/wp-content/uploads/2017/12/%E8%AE%A4%E8%AF%81%E4%B8%8E%E9%89%B4%E6%9D%83%E5%85%B3%E9%94%AE%E8%A7%92%E8%89%B2.png)  
整体流程的介绍中，关于用户身份认证与服务授权都用 “系统” 这个抽象角色描述的。但实际上，用户身份认证与服务授权都是不同的服务角色提供的。参与的各方角色包括：

*   **Client**: Application Client 应用客户端
*   **AS**: Authentication Server 用来认证用户身份
*   **TGS**: Ticket-Granting Service 用来授权服务访问
*   **SS**: Service Server 用户所请求的服务

1. 用户登录
-------

![](http://www.nosqlnotes.com/wp-content/uploads/2017/12/1%E7%94%A8%E6%88%B7%E7%99%BB%E5%BD%95-1.png)

*   用户登录阶段，通常由用户输入 **[用户名]** 和 **[密码]** 信息。
*   在客户端侧，用户输入的 **[密码]** 信息被通过一个**单向 Hash 函数**生成一个 **[Client 密钥]**。

2. 请求身份认证
---------

### 2.1 客户端向 AS 发送认证请求

![](http://www.nosqlnotes.com/wp-content/uploads/2017/12/2.1%E5%AE%A2%E6%88%B7%E7%AB%AF%E8%AF%B7%E6%B1%82%E7%94%A8%E6%88%B7%E8%AE%A4%E8%AF%81.png)

*   客户端为执行登录操作的用户向 **AS** 发送**认证请求**
*   请求中带有 **[用户名]** 信息，用户名以明文形式发送到客户端。

> **Note**  
> Client 往 AS 发送认证请求时并未发送 [密码] 或[密钥]信息

### 2.2 AS 确认 Client 端登录者用户身份

![](http://www.nosqlnotes.com/wp-content/uploads/2017/12/2.2AS%E7%A1%AE%E8%AE%A4%E5%AE%A2%E6%88%B7%E7%AB%AF%E7%94%A8%E6%88%B7%E8%BA%AB%E4%BB%BD-1.png)

1.  AS 收到用户认证请求之后，根据请求中的 **[用户名]** 信息，从数据库中查找该用户名是否存在。
2.  如果 **[用户名]** 存在，则对应的 **[密码]** 也可以从数据库中获取到。AS 利用相同的单向 Hash 函数为 [密码] 生成一个秘钥，如果第 1 步中用户提供的 [密码] 信息正确，该秘钥与用户登录章节中的 **[Client 密钥]** 相同。
3.  AS 为 Client 响应如下消息：
    *   **Msg A**  使用 **[Client 密钥]** 加密的 **[Client/TGS SessionKey]**
    *   **Msg B**  使用 **[TGS 密钥]** 加密的 **TGT(Ticket-Granting-Ticket)**，因此该消息 Client 不可解析。  
        TGT 中包含如下信息：
        *   [Client/TGS SessionKey]
        *   Client ID
        *   Ticket 有效时间
        *   Client 网络地址

4.  Client 收到 AS 的响应消息以后，利用自身的 **[Client 密钥]** 可以对 Msg A 进行解密，这样可以获取到 **[Client/TGS SessionKey]**。但由于 Msg B 是使用 **[TGS 密钥]** 加密的，Client 无法对其解密。

> **Note**
> 
> 1.  AS 响应的消息中有一条是属于 Client 的，但另外一条却属于 TGS。
> 2.  Client/TGS SessionKey 出现了两个 Copy，一个给 Client 端，一个给 TGS 端。
> 3.  本文中提及的**加密**，如无特殊说明，均采用的是**对称加密算法**。

3. 请求服务授权
---------

### 3.1 客户端向 TGS 发送请求服务授权请求

![](http://www.nosqlnotes.com/wp-content/uploads/2017/12/3.1%E5%AE%A2%E6%88%B7%E7%AB%AF%E8%AF%B7%E6%B1%82%E6%8E%88%E6%9D%83%E6%9C%8D%E5%8A%A1%E8%AE%BF%E9%97%AE.png)  
客户端发送的请求中包含如下两个消息：

*   **Msg C**
    *   要请求的服务 ID, 即 **[Service ID]**
    *   上一步 2.2 中由 AS 为 Client 提供的 **TGT**。
*   **Msg D**
    *   使用 **[Client/TGS SessionKey]** 加密的 Authenticator 1 {Client ID, Timestamp}。

### 3.2 TGS 为 Client 响应服务授权票据

![](http://www.nosqlnotes.com/wp-content/uploads/2017/12/3.2TGS%E6%8E%88%E6%9D%83%E5%AE%A2%E6%88%B7%E7%AB%AF%E7%94%A8%E6%88%B7%E8%AE%BF%E9%97%AE%E6%9C%8D%E5%8A%A1-1.png)  
TGS 为 Client 响应的消息包括：

*   **Msg E**   使用 **[Service 密钥]** 加密的 Client-To-Server Ticket, 该 Ticket 中包含了如下信息:
    *   **[Client/Server SessionKey]**
    *   Client 网络地址
    *   Ticket 有效时间
    *   Client ID
*   **Msg F**   使用 **[Client/TGS SessionKey]** 加密的 **[Client/Server SessionKey]**。

Msg F 使用了 **[Client/TGS SessionKey]** 加密，因此，该消息对 Client 可见。Client 对其解密以后可获取到 **[Client/Server SessionKey]**。  
而 Msg E 使用了 **[Service 密钥]** 加密，该消息可视作是 TGS 给 Service Server 的消息，只不过由 Client 一起携带。

4. 发送服务请求
---------

### 4.1 Client 向 SS(Service Server) 发送服务请求

![](http://www.nosqlnotes.com/wp-content/uploads/2017/12/4.1%E5%AE%A2%E6%88%B7%E7%AB%AF%E5%90%91%E7%94%B3%E8%AF%B7%E7%9A%84%E6%9C%8D%E5%8A%A1%E5%8F%91%E9%80%81%E8%AF%B7%E6%B1%82-2.png)  
发送的消息中包括：

*   **Msg E**   上一步 3.2 中，TGS 为 Client 响应的消息 Msg E。该消息可以理解为由 Client 为 SS 携带的消息。
*   **Msg G**   由 **[Client/Server SessionKey]** 加密的 **Authenticator 2**，包含 {Client ID, Timestamp} 信息。  
    这里的 Authenticator 2 区别于前面 3.1 步骤中的 Authenticator 1。

> **Note**
> 
> 1.  **[Client/Server SessionKey]** 并未直接透明传输，而是被包含在使用 **[Service 密钥]** 加密的 Msg E 中。
> 2.  既然 **[Client/Server SessionKey]** 并不直接透明传输， Client 需要向 SS 证明自己拥有正确的 **[Client/Server SessionKey]**，所以，Authenticator 2 使用了 **[Client/Server SessionKey]** 加密。

### 4.2 SS 响应 Client

![](http://www.nosqlnotes.com/wp-content/uploads/2017/12/4.2%E8%A2%AB%E8%AF%B7%E6%B1%82%E7%9A%84%E6%9C%8D%E5%8A%A1%E7%BB%99%E5%AE%A2%E6%88%B7%E7%AB%AF%E5%93%8D%E5%BA%94.png)  
SS 收到客户端的服务请求之后，先利用自身的 **[Service 密钥]** 对 Msg E 进行解密，提取出 Client-To-Server Ticket, 在 3.2 步骤中，提到了该 Ticket 中包含了 **[Client/Server SessionKey]** 以及 Client ID 信息。  
SS 使用 **[Client/Server SessionKey]** 解密 Msg G，提取 Client ID 信息，而后将该 Client ID 与 Client-To-Server Ticket 中的 Client ID 进行比对，如果匹配则说明 Client 拥有正确的 **[Client/Server SessionKey]**。  
而后，SS 向 Client 响应 Msg H(包含使用 **[Client/Server SessionKey]** 加密的 Timestamp 信息)。  
Client 收到 SS 的响应消息 Msg H 之后，再使用 **[Client/Server SessionKey]** 对其解密，提取 Timestamp 信息，然后确认该信息与 Client 发送的 Authenticator 2 中的 Timestamp 信息一致。  
如上信息可以看出来，该交互过程起到了 Client 与 SS 之间的 **“双向认证”** 作用。

_References_

1.  [Kerberos Protocol](https://en.wikipedia.org/wiki/Kerberos_(protocol))

本文源自：[NoSQL 漫谈 (nosqlnotes.com)](http://www.nosqlnotes.com/)  
除非特别注明，本站文章均为原创，转载请注明出处和链接。
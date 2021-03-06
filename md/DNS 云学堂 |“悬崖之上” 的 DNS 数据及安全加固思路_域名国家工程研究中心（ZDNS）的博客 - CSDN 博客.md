> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.csdn.net](https://blog.csdn.net/weixin_38354951/article/details/116654299)

> 5G、物联网等新技术的发展，推动亿万终端接入互联网，网间传输着大量的用户数据。然而作为互联网应用访问的枢纽，DNS在其设计之初对数据的完整性、可靠性缺乏考虑，导致用户的资产信息、应用访问信息、访问行为等隐私数据对外暴露，存在安全隐患。本期云学堂将为大家阐述加固DNS数据安全的重要性。enjoy：近来，IETF（互联网工程任务组）提出一项新的DNS安全技术草案——Oblivious DNS Over HTTPS。该技术提供公共秘钥加密、代理服务器两种手段，实现DNS数据安全的提升。传统DNS请求过程

5G、物联网等新技术的发展，推动亿万终端接入互联网，网间传输着大量的用户数据。然而作为互联网应用访问的枢纽，DNS 在其设计之初对数据的完整性、可靠性缺乏考虑，导致用户的资产信息、应用访问信息、访问行为等隐私数据对外暴露，存在安全隐患。本期云学堂将为大家阐述加固 DNS 数据安全的重要性。enjoy：

近来，IETF（互联网工程任务组）提出一项新的 DNS 安全技术草案——Oblivious DNS Over HTTPS。该技术提供公共秘钥加密、代理服务器两种手段，实现 DNS 数据安全的提升。  
![](https://img-blog.csdnimg.cn/20210511143730945.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zODM1NDk1MQ==,size_16,color_FFFFFF,t_70#pic_center)  

传统 DNS 请求过程

![](https://img-blog.csdnimg.cn/20210511144914603.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zODM1NDk1MQ==,size_16,color_FFFFFF,t_70#pic_center)  

ODNS 请求过程

由上图可以看出，传统 DNS 的请求和响应数据都是明文传输，用户请求的源 IP 地址、请求域名、请求类型、TTL、应答结果等信息都可被获取，攻击者可以对用户的访问数据、访问行为进行分析，实施下一步攻击；ODNS 的请求和响应数据都使用秘钥加固，在 DNS 递归和权威解析的任何一个环节，只能获取用户的片段化信息，极大的提升了 DNS 查询过程中的数据安全性。但由于 ODNS 流程中增加了数据加密、代理转发、迭代查询过程，为整个 DNS 解析引入了额外的成本。

**我们不禁要问：通过复杂性机制来提升 DNS 数据安全性，是否值得？**

在《IDC 2020 全球 DNS 威胁报告》中指出：

*   过去一年，全球 79% 的公司遭遇过 DNS  
    攻击，大部分企业承担着 DNS 攻击带来的经济损失，平均每次攻击造成的损失在 924,000 美元左右。
*   DNS 网络钓鱼成为流行攻击方式，有 39％的公司遭遇网络钓鱼，这意味着企业用户的隐私数据（如个人账户的用户名 / 密码、手机号、住址、银行账户密码等）可能被恶意攻击者窃取。
*   17% 的公司遭受到 DNS 隧道攻击，攻击者可以利用 DNS 隧道窃取用户的数据，或是将木马、蠕虫、恶意软件等植入用户的终端设备，致使设备中毒。
*   另外，16% 的受访者在遭遇 DNS 攻击的同时，隐私数据也被盗取，同比 2019 年为 13%。企业用户的隐私数据在 DNS 攻击过程中的丢失的几率在不断增加。

在这种趋势下，DNS 数据安全应该成为企业网络安全重点关注的问题。

整体上我们认为，企业用户面临的 DNS 隐私数据风险一般分为三层，任何一层没有得到防护，都可能导致用户的业务直接受损：  
![](https://img-blog.csdnimg.cn/20210511144205988.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zODM1NDk1MQ==,size_16,color_FFFFFF,t_70#pic_center)

*   **第一层（内部风险）**：攻击者将恶意软件植入到客户终端，使终端中毒，通过 DNS 请求外泄用户的隐私数据。  
    **应对思考**：针对此类风险，除了保证终端设备的安全外，我们也可以通过限制 DNS 数据的携带特征、流量特征以及 DNS 要查询的域名，检测请求传输过程中可疑的数据，从而保证 DNS 查询和响应过程中数据内容的安全可靠，避免用户数据外泄。
*   **第二层（DNS 自身风险）**：由于 DNS 自身系统存在漏洞或安全合规机制不完善，导致在其上的业务配置、运维数据被窃取或篡改，用户数据的完整性和可靠性无法保证。  
    **应对思考**：针对此类风险，我们应该从整体系统安全的角度进行防护。
    *   操作系统安全：我们可以对操作系统进行安全加固，定期执行安全扫描，避免因系统的漏洞引发 DNS 攻击。
    *   DNS 业务安全：我们可以通过合规控制、权限划分、审计工作流、记录日志等手段保障业务数据的完整性和准确性。
*   **第三层（外部风险）**：由于 DNS 与互联网的交互数据透明传输，攻击者可以通过网络监听手段，收集用户的访问痕迹（如查询时间、访问内容、用户 IP 地址等）信息，并分析用户的行为习惯，进而实施下一步攻击，如缓存投毒。  
    **应对思考**：针对此类风险，我们可以通过 DNSSEC、ODNS、DoH、DoT 等技术，加密请求和应答数据，使攻击者无法对用户的 DNS 数据下手。

总结
--

完善的 DNS 安全应该是服务 + 数据的双重保险，**在确保 DNS 服务坚固的同时，加固隐私数据的传输通道，进而保障用户的网络安全。**
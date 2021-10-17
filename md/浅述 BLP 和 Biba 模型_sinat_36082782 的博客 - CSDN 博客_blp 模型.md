> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.csdn.net](https://blog.csdn.net/sinat_36082782/article/details/104506721)

BLP 和 Biba 模型都属于强制访问控制（MAC）模型。其中，BLP 用于保护数据机密性，而 Biba 则针对完整性。

1.BLP 模型
--------

Bell-LaPadula 模型 (BLP) 是一种状态机模型，用于在政府和军事应用中实施访问控制。BLP 当初设计出来用于规范美国国防部的多级安全 (MLS) 策略。采用 BLP 模型的系统之所以被称为多级安全系统，是因为使用这个系统的用户具有不同的许可，而且系统处理的数据也具有不同的分类。

BLP 数据和用户安全等级被划分为以下安全等级  
　公开（Unclassified）  
　受限（Restricted）  
　秘密（Confidential）  
　机密（Secret）  
　高密（Top Secret）

BLP 模型侧重于数据的**保密性**和对机密信息的受控访问，如果主体对对象的所有访问模式符合安全策略，则该系统的状态被定义为 “**安全**”。为了确定是否允许特定的访问模式，系统需要将主体 (subject) 的许可权与对象 (object) 的等级（更确切地说，数据等级和数据分隔的组合所构成的安全级别 ）进行比较。  
BLP 具有三种安全属性：

1.  简单安全属性 (Simple Security Property) ：规定给定安全级别的主体无法读取更高安全级别的对象。
2.  * 属性 (star Property) ：规定给定安全级别的主体无法写入任何更低安全级别的对象。
3.  自主安全属性 (Discretionary Security Property) ：使用访问矩阵来规定自主访问控制。

在存在受信任主体的情况下，BLP 模型可能会产生从高机密文档到低机密文档的信息流动。**受信任主体不受 * 属性的限制**，但必须证明其在安全策略方面是值得信任的。该安全模型针对访问控制，并被描述为：“下读，上写”。 **信息自下而上流入**

在 BLP 模型中，用户只能在其自己的安全级别或更高的安全级别上创建内容（如，秘密研究人员可以创建秘密或绝密文件，但不能创建公共文件；不能下写）。相反，用户只能查看在其自己的安全级别或更低的安全级别的内容（如，秘密研究人员可以查看公共或秘密文件，但不能查看绝密文件；不能上读）。  
![](https://img-blog.csdnimg.cn/20200225221853735.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NpbmF0XzM2MDgyNzgy,size_16,color_FFFFFF,t_70)

2.Biba 模型
---------

Biba 模型是 K.J.Biba 在 1977 年提出的完整性访问控制模型，也是一种强制访问控制模型。  
Biba 模型解决了系统内数据的**完整性**问题。它不关心安全级别和机密性。Biba 模型用完整性级别来防止数据从任何完整性级别流到较高的完整性级别中。**信息在系统中只能自上而下流动。**  
Biba 通过 3 条主要规则来提供这种保护：

1.  简单完整性公理：主体不能从较低完整性级别读取数据（被称为 “不能向下读”）。
2.  * 完整性公理：主体不能向位于较高完整性级别的客体写数据（被称为 “不能向上写”）。
3.  调用属性：主体不能请求（调用）完整性级别更高的主体的服务。

![](https://img-blog.csdnimg.cn/20200225222424509.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NpbmF0XzM2MDgyNzgy,size_16,color_FFFFFF,t_70)

参考资料：
-----

> https://zhuanlan.zhihu.com/p/34722589  
> https://zh.wikipedia.org/wiki/Bell%E2%80%93LaPadula%E6%A8%A1%E5%9E%8B#cite_note-1  
> https://blog.csdn.net/ajian005/article/details/8490082
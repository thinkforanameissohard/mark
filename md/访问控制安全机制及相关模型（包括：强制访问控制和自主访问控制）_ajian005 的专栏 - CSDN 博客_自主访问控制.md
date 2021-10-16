> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.csdn.net](https://blog.csdn.net/ajian005/article/details/8490082)

> 第一章 访问控制的概念　访问控制分类　网络访问控制 　主机/操作系统访问控制 　应用程序访问控制　加密方式在访问控制系统中的应用第二章 强制访问控制与自主访问控制 　强制访问控制（MAC） 　自主访问控制（DAC）第三章 访问控制模型　BELL-LAPADULA保密性模型 　LATTICE安全模型　BIBA完整性模型　CLARK WILSON完整

**第一章 访问控制的概念**

　访问控制分类

　网络访问控制

　主机 / 操作系统访问控制

　应用程序访问控制

　加密方式在访问控制系统中的应用

**第二章 强制访问控制与自主访问控制**

　强制访问控制（MAC）

　自主访问控制（DAC）

**第三章 访问控制模型**

　BELL-LAPADULA 保密性模型

　LATTICE 安全模型

　BIBA 完整性模型

　CLARK WILSON 完整性模型

　CHINESE WALL 模型

第一讲 访问控制概念  

-------------

**绪论**

　　访问控制，作为提供信息安全保障的主要手段，及最为突出的安全机制, 被广泛地应用于防火墙、文件访问、**VPN** 及物理安全等多个方面。 所有这些技术可归诸于几类访问控制模型，本文将一一介绍并以实例说明，以帮助设计者在多变的环境中解决相关安全问题。

### **第一章 访问控制的概念**

　　访问控制是信息安全保障机制的核心内容，它是实现数据保密性和完整性机制的主要手段。访问控制是为了限制访问主体（或称为发起者，是一个主动的实体；如用户、进程、服务等），对访问客体（需要保护的资源）的访问权限，从而使计算机系统在合法范围内使用；访问控制机制决定用户及代表一定用户利益的程序能做什么，及做到什么程度。

访问控制的两个重要过程：  
1、通过 " 鉴别（**authentication**）" 来检验主体的合法身份  
2、通过 " 授权（**authorization**）" 来限制用户对资源的访问级别

访问包括读取数据，更改数据，运行程序，发起连接等。

**访问控制分类**  
  
因实现的基本理念不同，访问控制可分为以下两种：

*   强制访问控制（Mandatory access control）  
    
*   自主访问控制（Discretionary access control）  
    （关于强制访问控制与自主访问控制，本文将在第二章作详细介绍。）

　　例如，当一个用户通过身份认证机制登陆到某一 **WINDOWS** 系统时，**WINDOWS** 文件访问控制机制将检查系统中哪些文件该用户可以访问。

　　访问控制所要控制的行为有以下几类：读取数据、运行可执行文件、发起网络连接等等。

**访问控制应用类型**

根据应用环境的不同，访问控制主要有以下三种：  

*   网络访问控制  
    
*   主机、操作系统访问控制  
    
*   应用程序访问控制

**网络访问控制**

![](https://img-my.csdn.net/uploads/201301/10/1357802757_7966.JPG)  

图 1-1　　　　　　　　　　　　　　　　　　　

　　访问控制机制应用在网络安全环境中，主要是限制用户可以建立什么样的连接以及通过网络传输什么样的数据，这就是传统的网络防火墙。防火墙作为网络边界阻塞点来过滤网络会话和数据传输。根据防火墙的性能和功能，这种控制可以达到不同的级别。

 **防火墙可实现以下几类访问控制：**

　　1) 连接控制，控制哪些应用程序终结点之间可建立连接。例如，防火墙可控制内部的某些用户可以发起对外部 WEB 站点间的的连接。

　　2) 协议控制，控制用户通过一个应用程序可以进行什么操作，例如，防火墙可以允许用户浏览一个页面，同时拒绝用户在非信任的服务器上发布数据。

　　3) 数据控制，防火墙可以控制应用数据流的通过。如防火墙可以阻塞邮件附件中的病毒。

防火墙实现访问控制的尺度依赖于它所能实现的技术。

**主机 / 操作系统访问控制**

![](https://img-my.csdn.net/uploads/201301/10/1357803070_5547.JPG)  

图 1-2

　　目前主流的操作系统均提供不同级别的访问控制功能。通常，操作系统借助访问控制机制来限制对文件及系统设备的访问。

　　例如**：Windows NT/2000** 操作系统应用访问控制列表来对本地文件进行保护，访问控制列表指定某个用户可以读、写或执行某个文件。文件的所有者可以改变该文件访问控制列表的属性。

**应用程序访问控制**

![](https://img-my.csdn.net/uploads/201301/10/1357803195_3610.JPG)  

　　　访问控制往往嵌入应用程序（或中间件）中以提供更细粒度的数据访问控制。当访问控制需要基于数据记录或更小的数据单元实现时，应用程序将提供其内置的访问控制模型。

　例如，大多数数据库（如 **Oracle**）都提供独立于操作系统的访问控制机制，**Oracle** 使用其内部用户数据库，且数据库中的每个表都有自己的访问控制策略来支配对其记录的访问。

　　另外比较典型的例子是电子商务应用程序，该程序认证用户的身份并将其置于特定的组中，这些组对应用程序中的某一部分数据拥有访问权限。

**加密方式在访问控制系统中的应用**

　　加密方法也经常被用来提供实现访问控制。或者独立实施访问控制，或者作为其它访问控制机制的加强手段。例如，采用加密可以限定只有拥有解密密钥的用户才有权限访问特定资源。

　　**IPsec VPN** 采用强加密机制来提供访问控制以非可信网络中的用户访问经由 **VPN** 传输的数据。此外，加密和密钥管理也可实现访问控制机制，只有拥有相应的密钥（**IPsec** 安全关联协商成功），才可以解密及访问数据。

　　存储于本地硬盘的数据也可以被加密，所以同一系统中的用户若无相应解密密钥也不可读取相关数据。如此就可以代替传统的文件权限控制方式。个别数据库产品可以加密位于本地磁盘上的数据库文件，这样就可弥补操作系统访问控制机制的不足。

### **第二章 强制访问控制与自主访问控制**

**强制访问控制（MAC）**

　　用来保护系统确定的对象，对此对象用户不能进行更改。也就是说，系统独立于用户行为强制执行访问控制，用户不能改变他们的安全级别或对象的安全属性。这样的访问控制规则通常对数据和用户按照安全等级划分标签，访问控制机制通过比较安全标签来确定的授予还是拒绝用户对资源的访问。强制访问控制进行了很强的等级划分，所以经常用于军事用途。

![](https://img-my.csdn.net/uploads/201301/10/1357804236_1243.JPG)  

　　　　　　　　　　　　　　图 2-1

　　在强制访问控制系统中，所有主体（用户，进程）和客体（文件，数据）都被分配了安全标签，安全标签标识一个安全等级。

*   　主体 (用户, 进程) 被分配一个安全等级  
    
*   　客体 (文件, 数据) 也被分配一个安全等级  
    
*   　访问控制执行时对主体和客体的安全级别进行比较

　　用一个例子来说明强制访问控制规则的应用，如 **WEB** 服务以 "秘密" 的安全级别运行。假如 **WEB** 服务器被攻击，攻击者在目标系统中以 "秘密" 的安全级别进行操作，他将不能访问系统中安全级为 "机密" 及 "高密" 的数据。

**自主访问控制（DAC）**

　　自主访问控制机制允许对象的属主来制定针对该对象的保护策略。通常 **DAC** 通过授权列表（或访问控制列表）来限定哪些主体针对哪些客体可以执行什么操作。如此将可以非常灵活地对策略进行调整。由于其易用性与可扩展性，自主访问控制机制经常被用于商业系统。

自主访问控制中，用户可以针对被保护对象制定自己的保护策略。

*   　每个主体拥有一个用户名并属于一个组或具有一个角色  
    
*   　每个客体都拥有一个限定主体对其访问权限的访问控制列表（**ACL**）  
    
*   　每次访问发生时都会基于访问控制列表检查用户标志以实现对其访问权限的控制

　　在商业环境中，你会经常遇到自主访问控制机制，由于它易于扩展和理解。大多数系统仅基于自主访问控制机制来实现访问控制，如主流操作系统 (**Windows NT Server, UNIX** 系统)，防火墙（**ACLs**）等。

　　强制访问控制和自主访问控制有时会结合使用。例如，系统可能首先执行强制访问控制来检查用户是否有权限访问一个文件组（这种保护是强制的，也就是说：这些策略不能被用户更改），然后再针对该组中的各个文件制定相关的访问控制列表（自主访问控制策略）。

### **第三章 访问控制模型 之 **强制访问控制（MAC）****

**Bell-LaPadula** 保密性模型是第一个能够提供分级别数据机密性保障的安全策略模型（多级安全）。

**1973 年，David Bell** 和 **Len LaPadula** 提出了第一个正式的安全模型，该模型基于强制访问控制系统，以敏感度来划分资源的安全级别。将数据划分为多安全级别与敏感度的系统称之为多级安全系统

**Bell-LaPadula (BLP)** 安全模型对主体和客体按照强制访问控制系统的哲学进行分类，这种分类方法一般应用于军事用途。

数据和用户被划分为以下安全等级

*   　公开（**Unclassified**）  
    
*   　受限（**Restricted**）  
    
*   　秘密（**Confidential**）  
    
*   　机密（**Secret**）  
    
*   　高密（**Top Secret**）  
    

**BLP** 保密模型基于两种规则来保障数据的机秘度与敏感度：

*   　上读 (**NRU**) , 主体不可读安全级别高于它的数据  
    
*   　下写 (**NWD**) , 主体不可写安全级别低于它的数据

　　直接来讲，要考虑数据的保秘性. 例如. 假如一个用户，他的安全级别为 "高密"，想要访问安全级别为 "秘密" 的文档，他将能够成功读取该文件，但不能写入；而安全级别为 "秘密" 的用户访问安全级别为 "高密" 的文档，则会读取失败，但他能够写入。这样，文档的保秘性就得到了保障。

　　另外，目前不能在原有操作系统中直接进行安全分级。也就是说，在解决其易用性与功能单一性之前，**BLP** 模型不能直接用于商业系统。

![](https://img-my.csdn.net/uploads/201301/10/1357804629_4734.JPG)  

图 3-1 **图 3-1** 为一个用户和资源安全分级的例子。 **BLP** 模型允许用户读取安全级别比他低的资源；相反地，写入对象的安全级别只能高于用户级别。简言之，信息系统是一个由低到高的层次化结构。  
 

![](https://img-my.csdn.net/uploads/201301/10/1357804793_1699.JPG)　　　　　　　　　　　　　　　　　　　　　　图 3-2

**图 3-2** 示例在通讯过程中如何体现 BLP 模型思想，尽管这种应用在 **BLP** 模型的实际应用中并不多见。当企业的两个分支网络要跨越非可信网络进行互联时，我们可以为两个网络及其间传输的数据设定虚拟的安全标签，可以假设两个分支机构的安全级别均为 "机秘"，而 **Internet**，作为 **VPN** 的传输媒介，它的安全级别为 "公开"，因此依照 BLP 模型，**Internet** 上的用户仅可以看到 "公开" 的数据。而两个分支网络间的数据安全级别为 "机秘"，因此，访问控制机制导致 **Internet** 用户不能访问 "机秘" 数据，而这是由于 VPN 使用了加密技术以实现访问控制机制。

　　另外的一个例子是防火墙所实现的单向访问机制，它不允许敏感数据从内部网络（例如，其安全级别为 "机秘"）流向 **Internet**（安全级别为 "公开"），所有内部数据被标志为 "机密" 或 "高密"。防火墙提供 "上读" 功能来阻止 **Internet** 对内部网络的访问，提供 "下写" 功能来限制进入内部的数据流只能经由由内向外发起的连接流入（例如，允许 **HTTP** 的 "**GET**"操作而拒绝"**POST**" 操作，或阻止任何外发的邮件）。  
  

**Lattice 安全模型**

![](https://img-my.csdn.net/uploads/201301/10/1357805106_1550.JPG)  

  
**Lattice** 模型通过划分安全边界对 **BLP** 模型进行了扩充，它将用户和资源进行分类，并允许它们之间交换信息，这是多边安全体系的基础。

　　多边安全的焦点是在不同的安全集束（部门，组织等）间控制信息的流动，而不仅是垂直检验其敏感级别。

　　建立多边安全的基础是为分属不同安全集束的主体划分安全等级，同样在不同安全集束中的客体也必须进行安全等级划分，一个主体可同时从属于多个安全集束，而一个客体仅能位于一个安全集束。

　　在执行访问控制功能时，**lattice** 模型本质上同 **BLP** 模型是相同的，而 **lattice** 模型更注重形成 "安全集束"。**BLP** 模型中的 "上读下写" 原则在此仍然适用，但前提条件必须是各对象位于相同的安全集束中。主体和客体位于不同的安全集束时不具有可比性，因此在它们中没有信息可以流通。

　　例如，某用户有安全级别为 "高密" 并从属于安全集束 "**ALPHA**"，另一个安全级别为" 机密 "的集束"**BETA**"中的用户试图访问从属于多个安全集束中的文件，若他需要访问集束"**ALPHA**"中安全级别为" 机密 "的文件，访问将被允许；而他访问集束"**BETA**"中的" 机密 "文件的试图将被拒绝。试图访问集束"**GAMMA**"中的任何对象都将被拒绝，因为其在集束"**GAMMA**" 中不具有任何安全等级

**Biba 完整性模型**

![](https://img-my.csdn.net/uploads/201301/10/1357805415_2062.JPG)  

　　七十年代，**Ken Biba** 提出了 **Biba** 访问控制模型，该模型对数据提供了分级别的完整性保证，类似于 **BLP** 保密性模型，**BIBA** 模型也使用强制访问控制系统。  
  
 **Biba** 完整性模型对主体和客体按照强制访问控制系统的哲学进行分类，这种分类方法一般应用于**军事用途**。

　数据和用户被划分为以下安全等级  

*   　公开（**Unclassified**）  
    
*   　受限（**Restricted**）  
    
*   　秘密（**Confidential**）  
    
*   　机密（**Secret**）  
    
*   　高密（**Top Secret**）

**BIBA** 模型基于两种规则来保障数据的完整性的保密性。

*   　下读 (**NRU**) 属性, 主体不能读取安全级别低于它的数据  
    
*   　上写 (**NWD**) 属性, 主体不能写入安全级别高于它的数据

　　从这两个属性来看，我们发现 **Biba** 与 **BLP** 模型的两个属性是相反的，BLP 模型提供保密性，而 **BIBA** 模型对于数据的完整性提供保障。

　 **BIBA** 模型并没有被用来设计安全操作系统，但大多数完整性保障机制都基于 **Biba** 模型的两个基本属性构建。

　　如图 3-4，一个安全级别为 "机密" 的用户要访问级别为 "秘密" 的文档，他将被允许写入该文档，而不能读取。如果他试图访问 "高密" 级的文档，那么，读取操作将被允许，而写入操作将被拒绝。这样，就使资源的完整性得到了保障。

　　因此，只有用户的安全级别高于资源的安全级别时可对资源进行写操作，相反地，只有用户的安全级别低于资源的安全经别时可读取该资源。简而言之，信息在系统中只能自上而下进行流动。

**应用举例：**

![](https://img-my.csdn.net/uploads/201301/10/1357805499_3231.JPG)  

**Biba** 模型在应用中的一个例子是对 **WEB** 服务器的访问过程。如图形 - 5，定义 **Web** 服务器上发布的资源安全级别为 "秘密"，**Internet** 上用户的安全级别为 "公开"，依照 **Biba** 模型，Web 服务器上数据的完整性将得到保障，**Internet** 上的用户只能读取服务器上的数据而不能更改它，因此，任何 "**POST**" 操作将被拒绝。

　　另一个例子是对系统状态信息的收集，网络设备作为对象，被分配的安全等级为 "机密"，网管工作站的安全级别为 "秘密"，那么网管工作站将只能使用 **SNMP** 的 "**get**"命令来收集网络设备的状态信息，而不能使用"**set**" 命令来更改该设备的设置。这样，网络设备的配置完整性就得到了保障。

**Clark Wilson 完整性模型**

 **Clark-Wilson** 数据完整性安全模型是在 1987 年被提出的，通常被用在银行系统中来保证数据的完整性，该模型略显复杂，是为现代数据存储技术量身定制的。

 **Clark Wilson** 完整性模型经常应用在银行应用中以保证数据完整性，它的实现基于成形的事务处理机制。

*   　系统接受 " 自由数据条目 (**UDI**)"并将其转换为" 受限数据条目 (**CDI**)"  
    
*   　" 受限数据条目 (**CDI**)"仅能被" 转换程序（**TP**）" 所改变  
    
*   　" 转换程序 (**TP**)"保证" 受限数据条目  
    **CDI**" 的完整性  
    
*   　每个受限数据条目 (**CDI**) 拥有一个完整性检查程序 (**IVP**)  
    
*   　访问控制机制由三个元素组成 (主体, **TP**, **CDI**)

应用举例：  
 ![](https://img-my.csdn.net/uploads/201301/10/1357805574_8322.JPG)  

**图 3-6** 所示为 **Clark Wilson** 完整性模型在电子商务程序中的应用，用户接到自主数据条目（**UDI**）并由转换程序（**TP**）将其转换为受限数据条目（**CDI**）**CDI1**，**CDI1** 用来更新 **CDI2**（例如客户的订单）和 **CDI3**（如客户的帐单），完整性检查程序（**IVP**）总是要检查是否 **CDI2**（订单）和 **CDI3（**帐单）是否出入平衡，因此可确保整个交易的完整性。

**Chinese Wall 模型**

**Chinese Wall** 模型是应用在多边安全系统中的安全模型（也就是多个组织间的访问控制系统），应用在可能存在利益冲突的组织中。最初是为投资银行设计的，但也可应用在其它相似的场合。

**Chinese Wall** 安全策略的基础是客户访问的信息不会与目前他们可支配的信息产生冲突。在投资银行中，一个银行会同时拥有多个互为竞争者的客户，一个银行家可能为一个客户工作，但他可以访问所有客户的信息。因此，应当制止该银行家访问其它客户的数据。

**Chinese Wall** 安全模型的两个主要属性：

*   　用户必须选择一个他可以访问的区域  
    
*   　用户必须自动拒绝来自其它与用户所选区域的利益冲突区域的访问

　　这种模型同时包括了 **DAC** 和 **MAC** 的属性：银行家可以选择为谁工作（**DAC**），但是一旦选定，他就被只能为该客户工作（**MAC**）。

应用示例：

![](https://img-my.csdn.net/uploads/201301/10/1357805663_5364.JPG)  

图 3-7

 **Chinese Wall** 安全模型在网络安全体系中应用的一个典型的例子是位于防火墙内部的一台服务器，连接着内部与外部网络。假如策略禁止经由此服务器转发数据，该服务器将曝露于外部网络（也就是说，该服务器仅能与外部网络通讯，而不能与内部网络通讯）

![](https://img-my.csdn.net/uploads/201301/10/1357805725_3313.JPG)  

图 3-8

　　另外用远程访问 **VPN** 来举例说明，位于 **Internet** 上的用户与内部网络建立 **VPN** 会话之后。依照中国墙安全模型所建议，在任何时候，用户或与 **Internet** 通讯，或与公司网络进行通讯，二者只可选其一（也就是说：隧道不可分割）

　　单向会话只发生在有限的时间内，本安全模型的核心在于 -- 用户选择与其中一方进行通讯，则放弃了与另一方会话的权利。

[第二讲 传统的访问控制](http://www.cnblogs.com/adylee/archive/2007/11/21/967552.html)
---------------------------------------------------------------------------

### **一、基本概念**

访问控制的基本任务是：防止非法用户进入系统及合法用户对系统资源的非法使用，它保证主体对客体的所有直接访问都是经过授权的。

**1****．客体：**

是一种能够从其它主体或客体接收信息的实体（文件、目录、数据块、记录、程序、存储器段、网络节点等），即包含有信息，又可以被访问的实体。

**2****．主体**

是一种可以使信息在客体之间流动的实体（进程、作业或任务（代表用户），用户也称为是主体）或能访问或使用客体的活动实体。

通常，我们把主体也看作是一个客体。因为当一个程序存放在内存或硬盘上时，那么它就与其它数据一样被当作客体，可供其它主体访问，但当这个程序运行时，它就成为了主体，可以去访问别的客体。

**3．访问模式（访问权限）  
**      是指主体对客体可进行的特定访问操作如：读（r）、写（w 可读可写或修改）、添加（a）、删除（d）、运行 (e) 等。

二种特殊的访问权限是控制权（c）、拥有权（o）。

       c 是指某个主体具有改变其它主体对某客体的访问权限的能力。

       o 若主体 S 创建客体 O，则 S 对 O 具有拥有权（每一客体 O 只有唯一的拥有者）。对 O 具有拥有权的主体必对 O 具有控制权，但反之则不然。

**4****．自主访问控制**

是指对某个客体具有拥有权（或控制权）的主体能够将对该客体的一种访问权或多种访问权自主地授予其它主体，并在随后的任何时刻将这些权限回收。

自主访问控制是保护计算机系统资源不被非法访问的一种有效手段，但是，它有一个明显的缺点：这种控制是自主的，虽然这种自主性为用户提供了很大的灵活性，得同时也带来了严重的安全问题。为此人们认识到必须采取更强有力的访问控制手段，这就是强制访问控制。

**5****．强制访问控制**

      系统根据主体被信任的程度和客体所包含的信息的机密性或敏感程度来决定主体对客体的访问权，这种控制往往可以通过给主、客体赋以安全标记来实现。

      强制访问控制一般与自主访问控制结合使用，在自主访问控制的基础上，施加一些更强的访问限制。一个主体只有通过了自主与强制性访问控制检查后，才能访问某个客体。

      用户可以利用自主访问控制来防范其它用户对自己客体的攻击，强制访问则提供了一个不可逾越的、更强的安全保护层。

### **二、自主访问控制（Discretionary Access Control****）**

**1、自主访问控制的矩阵模型  
**    ⑴系统状态用一个有序三元组表示 Q=(S,O,A)，

其中        S——主体的集合

              O——客体的集合

              A——访问矩阵，行对应于主体，列对应客体。A 的 (i,j) 项元素 a­­­ij 是一个集合, 该集合中列出了主体 Si 对客体 Oj 所允许的访问权限。

例：设 S={s1,s2},O={m1,m2,f1,f2,s1,s2,} 系统当前的状态如下：

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>m<sub>1</sub>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; m<sub>2</sub>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; f<sub>1</sub>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; f<sub>2­</sub>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; s<sub>1</sub>&nbsp;&nbsp;&nbsp; s<sub>2</sub></p></td></tr></tbody></table>

       

注：“拥有权”与 “控制权” 在有的系统中有区别。

系统中设置监控程序用来监控主体对客体的访问，某一主体 Si 要对客体 oj 进行访问时，监控程序要检查 aij 以决定 Si 是否可对 oj 进行访问以及可以进行什么样的访问，当 aij 中不包含主体 Si 对客体 oj 的某种访问权时，监控程序就禁止 Si 对 oj 进行相应的访问操作。监控程序可以由硬件、软件或者硬件与软件共同完成。

⑵系统状态的变化  
       系统状态是在不断变化的，变化是由于用户的一系列操作引起来的，系统状态变化，则相应的访问控制矩阵也就要发生变化。引起状态变化的操作基本上有如下几种：

1．Enter p into aij         (oj 拥有者授予主体 Si 对 Oj“p” 访问权)

2．Delete p from aij        (oj 拥有者撤销主体 Si 对 Oj“p” 访问权)

3. Create Subject s’

4. Create Object o’

5. Delete Subject s’

6. Delete Object o’

这些操作将引起访问控制矩阵的变化，且使得状态由 Q=(S,O,A) 转换到 Q’=(S’,O’,A’)

**2****、自主访问控制的实现方法**

      为了实现自主访问控制，必须将访问控制矩阵所提供的信息以某种形式保存在计算机系统中，实际上在实现自主访问控制时，并不是将矩阵整个存放在系统中，这样做，效率是很低的，因为这个矩阵很可能是一个许多项都为空的一个稀疏矩阵，这对于存储空间和查询时间都是一个很大的浪费。

实际上的实现方法可分为如下几类：

⑴基于行的自主访问控制——权力表

每个主体 Si 都有一个相应的权力表，Si 的权力表由访问控制矩阵中 Si 所对应的行中所有的非空项所组成，它是一张 Si 可以访问的所有客体的明细表。如：上例中

<table border="0" cellpadding="0" cellspacing="0"><tbody><tr><td width="64"><p align="center">O</p></td><td width="64"><p align="center">P</p></td></tr><tr><td width="64"><p align="center">m<sub>1</sub></p><p align="center">m<sub>2</sub></p><p align="center">f<sub>1</sub></p></td><td width="64"><p align="center">{r,w,e}</p><p align="center">{r}</p><p align="center">{c,r,w}</p></td></tr><tr><td colspan="2" width="128"><p align="center">S<sub>1</sub> 的权力表</p></td></tr></tbody></table>

<table align="left" border="0" cellpadding="0" cellspacing="0"><tbody><tr><td width="64"><p align="center">O</p></td><td width="64"><p align="center">P</p></td></tr><tr><td width="64"><p align="center">m<sub>1</sub></p><p align="center">m<sub>2</sub></p><p align="center">f<sub>1</sub></p></td><td width="64"><p align="center">{r,w,e}</p><p align="center">{r}</p><p align="center">{c,r,e}</p></td></tr><tr><td colspan="2" width="128"><p align="center">S<sub>2</sub> 的权力表</p></td></tr></tbody></table>

根据每一主体 Si 的权力表，可决定该主体可否对客体进行访问以及可以进行哪种模式的访问。

⑵基于列的自主访问控制——授权表（或访问控制表）

第一个客体都有一个相应的授权表，oj 的授权表由访问控制矩阵中 oj 所对应的列中所有非空项所组成，它是一张可以访问 oj 的所有主体的明细表。如上例中

<table border="0" cellpadding="0" cellspacing="0"><tbody><tr><td width="64"><p align="center">S</p></td><td width="64"><p align="center">P</p></td></tr><tr><td width="64"><p align="center">S<sub>1</sub></p><p align="center">S<sub>2</sub></p></td><td width="64"><p align="center">{r,w,e}</p><p align="center">{r}</p></td></tr><tr><td colspan="2" width="128"><p align="center">m<sub>1</sub> 的授权表</p></td></tr></tbody></table>

<table align="left" border="0" cellpadding="0" cellspacing="0"><tbody><tr><td width="64"><p align="center">S</p></td><td width="64"><p align="center">P</p></td></tr><tr><td width="64"><p align="center">S<sub>2</sub></p></td><td width="64"><p align="center">{c,r,e}</p></td></tr><tr><td colspan="2" width="128"><p align="center">f<sub>2</sub> 的授权表</p></td></tr></tbody></table>

根据每一客体 oj 的授权表可以决定哪些主体可以访问该客体以及可以进行什么样的访问。

**3.** **授权的管理方式**

      主体对客体的控制权 “c“在系统中有两种管理方式：一种是集中式管理，一种是分散式管理。

⑴集中式管理

      一个主体 si 在创建某个客体 oj 后，该主体就获得了对这一客体的 “c” 权和其它所有可能权限。“c” 权意味着可以将它对 oj 所有其它（除 “c” 权以外）的访问权限授予系统中任何一个主休，也可以撤销系统中任何主体对 oj 的其它访问权限。其它主体因为对 oj 不具有 “c” 权，因此即使他们对 oj 具有某些访问权限，但它们也无权将这些权限转授给别的主体、或撤销别的主体对 oj 的任何访问权限——在这种管理模式下，对于任一客体 oj，哪些主体可以对其进行访问，可以进行什么样的访问，完全由 oj 的拥有者决定。（在此管理模式下，“拥有权”和 “控制权” 是一致的。）

⑵分散式管理

      在这种管理模式下，一个客体 oj 的拥有者不仅可以授予其它主体对 oj 的所有其它的访问权，而且还可以授予他们对 oj 的某些访问权的授予权，因此，对于一客体 oj 的访问权，不仅 oj 的拥有者可以授权，其他的主体也有可能得到全部或部分的授予权。

      例如：下图表示数据库中对某个关系 X 的授权情况：

图中：A、B、C、D 分别表示四个主体，表示 A 对 B 授权。10，15，20，30 表示授权的时刻，R(y) 表示所授予的权限 R 可以再转授别的主体，R(n) 表示所授予的权

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>D</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>C</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>A</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>B</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p align="center">10</p><p>R(y),I(y)</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p align="center">20</p><p>R(y),I(y)</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p align="center">30</p><p>R(y),I(n)</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p align="center">15</p><p align="center">R(n)</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>A</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>B</p></td></tr></tbody></table>

限

R

不允许再转授给别的主体。

      由图中可看出：①在时刻 15——时刻 30 之间的一段时间，D 虽得到了对点系 X 的 R（Read）访问权，但他不能将此权再授给其它主体。②而在时刻 30 以后，C 授予了 D 的 R 和 I 的权限后，D 仅可将 R 权限授予其它的主体。

      在这种管理模式下，一个主体在撤销他所授予的对某个客体的某种权限时，必须将由于这一授权而引起的所有授权都予以撤销，系统的状态应该是好像该主体从来未对该权限授予过。

      例如：上例中，若时刻 40 后的某个时刻 A 撤销对 B 所授予的对关系 X 的 R 权，则此时不公 B 失去了对 X 的 R 权，且由此而引起 C 对 X 的 R 权，D 对 X 的 R 权都被撤销，此时虽然 D 保留了由 A 处得到的 R 权，但 D 不能将此权转授出去。

      对授权提出分散式管理的模式虽然有它的实际需要，但是分散式管理的缺陷是，一旦 oj 的拥有者将对 oj 的访问权的授予权授予出去后，他便无法控制系统中哪些主体可对 oj 进行访问，哪些主体不能进行访问，哪些主体对 oj 具有授予权，哪些主体对 oj 不具有授予权。例如该例中的 D，A 不让其具有 R 的授予权，但 C 却将 R 的授予授给了他。因此又有人提出了发 “黑令牌” 的方法，即 oj 的主体可对不允许访问 oj 的主体发放黑令牌。这样凡被发放黑令牌的主体，其它主体不得向他授权。（当然，可对某种访问权）

      在这种管理模式下，“拥有权”和 “控制权” 是不一致的。

**第三讲 安全策略与安全模型**
-----------------

### **一、安全策略**

**1****、安全策略的概念**

      计算机系统的安全策略是为了描述系统的安全需求而制定的对用户行为进行约束的一整套严谨的规则。这些规则规定系统中所有授权的访问，是实施访问控制的依据。

      一个计算机系统的安全策略应能说明系统在各种情形下，哪些主体对哪些信息的访问是允许的，什么样的访问是不允许的。

      相对于系统中实施安全策略的访问控制机制来说，安全策略是抽象的，指导性的原则，然而安全策略的制定是有强烈的实际背景的。

**2****、安全策略举例**

      以军事安全策略和商业安全策略为例来说明这一概念。军事部门的安全主要关心的是数据的保密性，而商业部门的安全主要关心的是数据的完整性，由于这一出发点不同使得他们的安全策略也有很大的不同。

⑴军事安全策略：

      分为两部分：自主安全策略（discretionary）和强制安全策略（ mandatory）

      · 自主安全策略：一个主体对客体的任何一种方式的访问都必须是该客体的拥有者事先对其进行了授权的。

**复习数学概念：**

1． 笛卡尔积:A×B

2． 集合 A 的幂集：P(A)=2A={s|sA}

3． 集合 A 上的偏序关系：集合 A 上的关系、自反、反对称、可传递的定义、次序图、偏序集、全序关系。

4． 有用的结论：

设 <A;≤> 和 <B;≤> 是，定义 A×B 上的关系：对任意 (a1,b1), (a2,b2) ∈A×B 当且仅当 a1≤a2，b1≤b2 时，有 (a1,b1)≤(a2,b2)。可以证明：<A×B;≤> 也是一个偏序集。

· 强制安全策略

       1．系统中每个主体和每个客体都有安全标记

      客体的安全级表示该客体所包含的信息的敏感程度或机密程度；

      主体的安全级表示该主休被信任的程度或访问信息的能力。

       2．安全标记由两个部分组成（密级，部门集）

      ①密级一般定义为四个级别：一般（U），秘密（C），机密（S）和绝密（TS）。

      用全序描述：一般≤秘密≤机密≤绝密。

      令 A={U,C,S,TS}，则 <A;≤> 是一个偏序集

      ②设某单位的部门集如下：{科技处，干部处，生产处，情报处}

令 B={科技处，干部处，生产处，情报处}，则 PB=2B={S|SB} 即 PB 中的元素均是 B 的子集，如 {科技处，干部处}∈PB，{科技处，生产处，情报处}∈PB 且 <PB;> 也是一个偏序集。

③定义笛卡尔积 A×PB={(a,H)|a∈A,H∈PB}

例如：（C，{科技处}）=class(o1)                           (可读)

        （S，{科技处，干部处}）=class(u)

        (TS,{科技处，情报处，干部处})=class(o2)            (可写)

        （C，{情报处}）=class(o3)                           (不读，不写)

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>o<sub>i</sub></p><p>写</p><p>u</p><p>读</p><p>o<sub>j</sub></p></td></tr></tbody></table>

均是

A

×

PB

中的元素，系统中主、客体的安全级由这些二元组来定义。

3．访问权的控制原则（即安全策略）

      一个主体仅能读安全级比自已安全级低或相等的客体，即 “向下读”。

             一个主体仅能写安全级比自己高或相等的客体，即 “向上写”。

       4. 安全级如何比较高低

<A;≤> 是一个偏序集，<PB;> 也是一个偏序集。

在集合 A×PB 上定义关系≤：对于（a1,H1）,（a2,H2）∈A×PB,（a1,H1）≤（a2,H2）当且仅当 a1≤a2，H1H2，可以证明：≤是 A×PB 上的一个偏序关系，即 <A×PB;≤> 也构成一个偏序集。在此，若（a1,H1）≤（a2,H2）则称（a1,H1）低于（a2,H2）。

例如：

（C，{科技处}）≤（S，{科技处，干部处}）；

（S，{科技处，干部处}）≤（TS，{科技处，情报处，干部处}）。

因此，（C，{科技处}）≤（TS，{科技处，情报处，干部处}）；

但（C，{情报处}）与（C，{科技处}）不可比，（C，{情报处}）与（S，{科技处，干部处}）不可比。

对于上述控制原则具体化：若主体 u 和客体 o 的安全级满足

若 class(u)≤class(o), 则 u 可 “写”o,

若 class(o)≤class(u), 则 u 可 “读”o.

于是上述 u 可读 o1,u 可写 o2,u 对 o3 不能读，也不能写，又如，若 class(o4)=(TS,{科技处})，则 u 不能读，也不能写。

⑵商业安全策略

主要的目的是防欺诈，防错误，防篡改，保护信息的完整性。虽然它也要防止非授权的泄露，但没有必要像军事安全中那样复杂的要求，其安全策略主要体现在以下两个方面：

①良形事务（Well-formed transaction）

用户对数据的操纵不能任意进行，而应该按照可保证数据完整性的受控方式进行，即数据应该用规定的程序，按照定义好的约束进行处理。

例：保存记录（包括修改数据的前后记录）

双入口规则，保持帐面平衡。

②职责分散 (Separation duty)

把一个操作分成几个子操作，不同的子操作由不同的用户执行，使得任何一个职员都不具有完成该任务的所有权限，尽量减少出现欺诈和错误的机会。

当然欺诈行为并不一定能就此消除，但它会在众多的职员的合作性行为中变得显而易见。

例如，购买原材料、进货并付款的过程可分解为以下几个操作来完成：

购买订单——记录到货——记录到货发票——付款

最后一个步骤只有在前三个步骤完成后才执行。

⑶军事安全策略与商业安全策略的比较

区别：

1．军事安全策略——主要关心的是数据的机密性

   商业安全策略——主要关心的是数据的完整性

2．军事安全策略——将数据与一个安全级相联系，通过数据的安全级来控制用户对数据的访问。

 商业安全策略——将数据与一组允许对其进行操作的程序相联系，通过这组程序来控制用户对数据的访问。

3．军事安全策略——用户被授权去读或写某一数据。

商业安全策略——用户被授权去执行与某一数据相关的程序。

       4．军事安全策略——用户只要获得了相应的访问权限，则他可以任意地去读或写访问该数据。

        商业安全策略——用户对数据的读、写方式不是任意的，而是隐含在那些被执行的程序动作之中。

       这一条使前者更容易受到病毒或特洛依木马的攻击。

相同之处：

1．计算机系统中必须有一种机制来保证系统实施了相应的安全策略；

2．系统中的安全机制必须防止破坏，即防止非授权的修改。

### **二、安全模型**

**1．安全模型**

       安全模型是对安全策略所表达的安全需求简单、抽象和无歧义的描述。它为安全系统的设计提供指导。

       安全模型应具有如下一些特点：

①它是精确的、无二义性的；

②它是简单、抽象的，也是易于理解的；

③它仅涉及安全性，不过分限制系统的功能及实现；

④它是安全策略的一个清晰的表达方式。

分为：

非形式化的安全模型：用自然语言对系统的安全性进行描述。其优点是直观、易于理解但不严谨，往往有二义性，表达不简洁。

形式化的安全模型：使用数学语言精确地描述系统的安全性质或规则。优点是简洁、准确、严谨，可以从理论上进行严格的证明其安全性；缺点是抽象、难于理解。

按照 TCSEC 的评估标准，B1 级要求既有自主访问控制又要有强制访问控制，这也就是要求它要制定安全策略，即非形式化的安全模型，指导系统如何进行上述两种访问控制；B2 级的计算机系统要求具有形式化的安全模型，A1 级并要求对安全模型进行形式化的证明。

由上可看出，若设计开发具有 B 类及以上的安全计算机系统必须要有安全模型作指导，对高安全级的计算机系统，形式化的安全模型则是不可少的必要条件。

  

===

[第三章 BLP 模型（Bell-La Padula 模型）](http://www.cnblogs.com/adylee/archive/2007/11/21/967547.html)
---------------------------------------------------------------------------------------------

是对安全策略形式化的第一个数学模型，是一个状态机模型，用状态变量表示系统的安全状态，用状态转换规则来描述系统的变化过程。

### **一、模型的基本元素**

模型定义了如下的集合：

S={s1,s2,…,sn} 主体的集合，主体：用户或代表用户的进程，能使信息流动的实体。

O={o1,o2,…,om} 客体的集合，客体：文件、程序、存贮器段等。（主体也看作客体 SO）

C={c1,c2,…,cq} 主体或客体的密级（元素之间呈全序关系）,c1≤c2≤…≤cq.

K={k1,k2,…,kr} 部门或类别的集合

A={r,w,e,a,c}   访问属性集，其中，r：只读；w：读写；e：执行；a：添加（只写）；                          c：控制。

RA={g,r,c,d}   请求元素集

                            g：get（得到），give（赋予）

                            r：release（释放），rescind（撤销）

                            c：change（改变客体的安全级），create（创建客体）

                            d：delete（删除客体）

D={yes,no,error,?} 判断集（结果集），其中

                            yes：请求被执行；

                            no：请求被拒绝；

                            error：系统出错，有多个规则适合于这一请求；

                            ?：  请求出错，规则不适用于这一请求。

μ={M1,M2,…,Mp} 访问矩阵集，其中元素 Mk 是一 n×m 的矩阵，Mk 的元素 MijA。

F=CS×CO×(PK)S×(PK)O，其中，

       CS={f1|f1：S→C}              f1 给出每一主体的密级；

       CO={f2|f2：O→C}             f2 给出每一客体的密级；

       (PK)S={f3|f3：S→PK} f3 给出每一主体的部门集；

       (PK)O={f4|f4：O→PK}f4 给出每一客体的部门集。

其中，PK 表示 K 的幂集（PK=2K）。

F 的元素记作 f=(f1,f2,f3,f4)，给出在某状态下每一主体的密级和部门集，每一客体的密级和部门集，即主体的许可证级（f1,f3），客体的安全级（f2,f4）。

### **二、系统状态**

V=P(S×O×A)×μ×F 是状态的集合，状态 v=(b,M,f) 用有序三元组表示，其中

       bS×O×A，是当前访问集。

       M 是访问矩阵，它的第 i 行，第 j 列的元素 MijA 表示在当前状态下，主体 Si 对客体 Oj 所拥有的访问权限。

       f=(f1,f2,f3,f4)，其中，f1(s) 和 f3(s) 分别表示主体 s 的密级和部门集，f2(s) 和 f4(s) 分别表示客体 O 的密级和部门集。  

###          

### **三、安全特性**

 **⑴自主安全性**

       状态 v=(b,M,f) 满足自主安全性，当且仅当对所有的 (si,oj,x)∈b，有 x∈Mij。

 **⑵简单安全性**

       状态 v=(b,M,f) 满足简单安全性，当且仅当对所有的 (s,o,x)∈b，有

              （i）x=e 或 x=a 或 x=c

          或 (ii) (x=r 或 x=w) 且 (f1(s)≥f2(o)，f3(s)f4(o))。

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>S</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>O</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p align="center">e,c,a</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>S</p><p>(高)</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>O</p><p>(低)</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p align="center">r,w</p></td></tr></tbody></table>

 **⑶*—性质**

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>S</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>O<sub>1</sub></p><p>(高)</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>O<sub>2</sub></p><p>(低)</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>a</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>r</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>S</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>O<sub>1</sub></p><p>(高)</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>O<sub>2</sub></p><p>(低)</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>a</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>w</p></td></tr></tbody></table>

      

状态

v=(b,M,f)

满足

*

—性质，当且仅当对所有的

s

∈

S

，若

o1

∈

b(S:w,a)

，

o2

∈

b(S:r,w),

则

f2(o1)

≥

f2(o2)

，

f4(o1)f4(o2)

，其中符号

b(S:x1,

…

,xn)

表示

b

中主体

s

对其具有访问特权

xi(1

≤

i

≤

n)

的所有客体的集合。

       解释：

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>S</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>O<sub>1</sub></p><p>(高)</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>O<sub>2</sub></p><p>(低)</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>w</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>r</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>S</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>O<sub>1</sub></p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>O<sub>2</sub></p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>w</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>w</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>(级别)</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>(级别)</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>相等</p></td></tr></tbody></table>

       一个状态 v 如果满足上述三条性质，那么 v 才是安全状态。

### **四、请求**

       R=S+×RA×S+×O×X 请求集（不是请求元素集），它的元素是一个完整的请求。其中 S+=S{}，X=A{}F。

       R 中的元素是一个五元组，代表一次请求或一个操作。

       T={1,2,…,t,…} 离散时刻的集合（标识）。用作请求序列，结果序列和状态序列的下标；

X=RT={x|x:T→R}，其中元素 x 可表示为 x=x1­x2x3…xt… 是一个请求序列，每一时刻有一请求，构成一个请求序列，因此 X 是请求序列的集合；

Y=DT={y|y:T→D}，其中元素 y=y1y2y3…yt… 是一个结果序列，每一时刻的请求导致一个判断（或结果），构成一个结果序列，Y 是结果序列的集合；

Z=VT={z|z:T→V}，其中元素 z=z1z2z3…zt… 是一个状态序列，每一 zt∈V，表示时刻 t 时系统的状态。Z 是状态序列的集合

### **五、状态转换规则**

       系统状态的转换由一组规则定义，一个规则 P 定义为：R×V→D×V。其中：R 是请求集，D 为判断集，V 是状态集。

       也就是说，P 规定对于给定的一个状态和一个请求，系统产生一个判断和下一个状态，只有当 D 的取值为 “yes” 时，请求才被执行，状态才发生转换。

       BLP 模型定义了十条基本规则（后来又有所扩充）：

       规则 1～规则 4 分别用于主体请求对客体的读（r），添加（a），执行（e）和写（w）的访问权。(φ,g,si,oj,r), (φ,g,si,oj,a), (φ,g,si,oj,e), (φ,g,si,oj,w)。

       规则 5 用于主体释放它对某客体的访问权（包括 r，或 a，或 e，或 w）。(φ,r,si,oj,x)

       规则 6 和规则 7 分别用于一个主体授予和撤销另一个主体对某客体的访问权。

(sλ,g,si,oj,r)     (sλ,r,si,oj,r)

       规则 8 用于改变静止客体的密级和类别集。(φ,c,φ,oj,f*)

       规则 9 和规则 10 分别用于创建和删除（使之成为静止）一个客体。

(φ,c,sj, oj,e)     (φ,d, si,oj,φ)

(φ,c, si,oj,φ)

规则 1：主体 si 请求得到对客体 oj 的 r 访问权

get-read P1(Rk,v)

       if σ1φ or γg or xr or σ2=φ then

              P1(RK,v)=(?,v)

       if rMij or (f1(si)<f2(oj) or f3(si)    f4(oj))

              then P1­(RK,v)=(no,v)

       if ={o|ob(si:w,a) and [f2(oj)>f2(o) or f4(oj) f4(o)]}= φ

              then P1­(RK,v)=(yes,v*=(b{(si,oj,r)},M,f))

              else P1­(RK,v)=(no,v)

       end

规则 2：主体 si 请求得到对客体 oj 的 a 访问权

get-append：P2(RK,v)

       如果 σ1φ or γg or xa or σ2=φ，则 P2(RK,v)=(?,v)

       如果 aMij，则 P2(RK,v)=(no,v)

       如果 ={o|ob(si:r,w) and [f2(oj)<f2(o) or f4(oj)f4(o)]}=φ

       则   P2(RK,v)=(yes,v*=(b{(si,oj,a)},M,f))

       否则 P2(RK,v)=(no,v)

       end

规则 3：主体 si 请求得到对客体 oj 的 e 访问权

get-execute：P3(RK,v)

       if σ1φ or γg or xe or σ2=φ then P3(RK,v)=(?,v)

       if eMij then P3(RK,v)=(no,v)

                      else P3(RK,v)=(yes,v*=(b{(si,oj,e)},M,f))

       end

规则 4：主体 si 请求得到对客体 oj 的 w 访问权

get-write：P4(RK,v)

       if σ1φ or γg or xw or σ2=φ then P4(RK,v)=(?,v)

       if wMij or [f1(si­)<f2(oj) or f3(si) f4(oj)]

              then P4(RK,v)=(no,v)

       if ={o|ob(si:r) and [f2(oj­)<f2(o) orf4(oj­)   f4(o)]}

              {o|ob(si:a) and [f2(oj­)>f2(o) or f4(oj­) f4(o)]}

              {o|ob(si:w) and [f2(oj­)f2(o) or f4(oj­)f4(o)]}=φ

       then P4(RK,v)=(yes,v*=(b{(si,oj,w)},M,f))

       else P4(RK,v)=(no,v)

       end

规则 5：主体 si 请求释放对客体 oj 的 r 或 w 或 e 或 a 访问权

release-read/write/append/execute：P5(RK,v)

       if (σ1φ) or (γr) or (xr,w,a and e) or (σ2=φ)

              then P5(RK,v)=(?,v)

              else P5(RK,v)=(yes,v*=(b-{(si,oj,x)},M,f))

       end

规则 6：主体 sλ请求授予主体 si 对客体 oj 的 r 或 w 或 e 或 a 访问权

give-read/write/append/execute P6(RK,v)

       if (σ1S) or (γg) or (xr,w,a and e) or (σ2=φ)

              then P6(RK,v)=(?,v)

       if xMλj or cMλj then P6(RK,v)=(no,v)

              else P6(RK,v)=(yes,(b,M[x]ij,f))

       end

规则 7：主体 sλ请求撤销主体 si 对客体 oj 的 r 或 w 或 e 或 a 访问权

rescind-read/write/append/execute：P7(RK,v)

       if (σ1S) or (γr) or (xr,w,a and e) or (σ2=φ) then

              P7(RK,v)=(?,v)

       if xMλj or cMλj then P7(RK,v)=(no,v)

              else P7(RK,v)=(yes, (b-{(si,oj,x)},M [x]ij,f))

       end

规则 8：改变静止客体的安全级

change-f：P8(RK,v)

       if (σ1φ) or (γc) or (σ2φ) or xF

then P8(RK,v)=(?,v)

       if f1 or f3 or [(oj)f2(oj) or (oj)f4(oj) for jA(m)]

                                                       注：A(m) 表示活动客体的集合

              then P8(RK,v)=(no,v)

              else P8(RK,v)=(yes,(b,M,f*))

       end

规则 9：主体 s 请求创建客体 oj

create-object：P9(RK,v)

       if σ1φ or γc or σ2=φ or (xe and φ) then

              P9(RK,v)=(?,v)

       if jA(m) then P9(RK,v)=(no,v)

       if x=φ then P9(RK,v)=(yes,(b,M[{r,w,a,c}]ij,f))

              else P9(RK,v)=(yes,(b,M[{r,w,a,c,e}]ij,f))

       end

规则 10：主体 s 请求删除客体 oj

delete-object：P10(RK,v)

       if σ1φ or γd or σ2=φ or xφ then

              P10(RK,v)=(?,v)

       if cMij then P10(RK,v)=(no,v)

              else P10(RK,v)=(yes,（b,M [{r,w,a,c,e}]ij,1≤i≤n,f))

       end

### **六、系统的定义**

1．R×D×V×V={(rK,dm,v*,v) | rKR,dmD,v*,vV}

       即，任意一个请求，任意一个结果（判断）和任意两个状态都可组成一个上述的有序四元组，这些有序四元组便构成集合 R×D×V×V。

       2．设ω={P1,P2,…Ps} 是一组规则的集合，定义 W(ω)R×D×V×V.

              ⑴(rk,?,v,v)W(ω) iff 对每个 i,1≤i≤s,Pi(rk,v)=(?,v)

              ⑵(rk,error,v,v)W(ω) iff 存在 i1,i2,1≤i1,i2≤s, 使得对于任意的 v*V 有 Pi1(rk,v)(?,v*) 且 Pi2(rk,v)(?,v*)。

⑶(rk,dm,v*,v)W(ω),dm?,dmerror，iff 存在唯一的 i，1≤i≤s，使得对某个 v* 和任意的 v**v，Pi(rk,v)(?,v**)，Pi(rk,v)=(dm,v*)。

以上定义说明 W(ω) 只包含 R×D×V×V 中一部分四元组，或某些特定的四元组。若某 (rk,dm,v*,v)W(ω)，则说明该四元组一定满足上述定义中（3 条）的某一条，亦即意味着在状态 v 下，发出某请求 rk 后，按照某条规则，其结果为 dm，状态 v 转换成状态 v*。因此 W(ω) 是由ω中的一组规则所定义的有序四元组所组成。

       3．X×Y×Z={(x,y,z)|xX,yY,zZ}, 其中，

              x=x1x2…xt… 是请求序列，X 是请求序列集；

              y=y1y2…yt… 是结果序列，Y 是结果序列集；

              z=z1z2…zt… 是状态序列，Z 是状态序列集。

       任意一个请求序列，任意一个结果序列和任意一个状态序列均可组成一个有序三元组，X×Y×Z 即由所有这样的有序三元组所构成。

       4．系统表示为∑(R,D,W(ω),z0)，定义为：

       ∑(R,D,W(ω),z0)X×Y×Z, 只含有其中一部分有序三元组，X×Y×Z 中的有序三元组 (x,y,z)∑(R,D,W(ω),z0),iff 对每一个 tT，(xt,yt,zt,zt-1)W(ω)。

       z0 是系统的初始状态，通常表示为 (φ,M,f)

       令   x=x1x2…xt… 是请求序列；

              y=y1y2…yt… 是结果序列；

              z=z1z2…zt… 是状态序列。

       若 (x,y,z)∑(R,D,W(ω),z0)，则意味着对于所有的 tT，(xt,yt,zt,zt-1)W(ω)，即符合ω所规定的操作规则。

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>z<sub>0</sub></p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>z<sub>1</sub></p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>z<sub>2</sub></p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>z<sub>t-1</sub></p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>z<sub>t</sub></p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p align="center">x<sub>1</sub></p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p align="center">x<sub>2</sub></p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p align="center">x<sub>t</sub></p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p align="center">y<sub>1</sub></p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p align="center">y<sub>2</sub></p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p align="center">y<sub>t</sub></p></td></tr></tbody></table>

       因此系统∑(R,D,W(ω),z0) 是一个状态机，它从一个特定的初始状态 z0 开始，接受用户的一系列请求，按照 W(ω) 的规则给出相应的结果，并进行相应的状态转换，符合上述条件的所有可能的 (x,y,z) 组成系统∑。系统 R 就是由所有这些有序三元组 (x,y,z) 所组成。

       从初始状态 z0 出发，任何一个请求序列均可导致出一结果序列和状态序列，引起一系列的状态转换。

### **七、系统安全的定义**

 **1．安全状态**

              一个状态 v=(b,M,f)V，若它满足自主安全性，简单安全性和 *—性质，那么这个状态就是安全的。

 **2．安全状态序列**

              设 zZ 是一状态序列，若对于每一个 tT，zt 都是安全状态，则 z 是安全状态序列。

 **3．系统的一次安全出现**

              (x,y,z)∑(R,D,W(ω),z0) 称为系统的一次出现。

              若 (x,y,z) 是系统的一次出现，且 z 是一安全状态序列，则称 (x,y,z) 是系统∑(R,D,W(ω),z0) 的一次安全出现。

 **4．安全系统**

              若系统∑(R,D,W(ω),z0) 的每次出现都是安全的，则称该系统是一安全系统。

### **八、模型中的有关安全的结论**

       BLP 模型中证明了：

       1．这十条规则都是安全性保持的。（即若 v 是安全状态，则经过这十条规则转换后的状态 v* 也一定是安全状态）

       2．若 z0 是安全状态，ω是一组安全性保持的规则，则系统∑(R,D,W(ω),z0) 是安全的。

       说明 BLP 模型所描述的系统是一个安全的系统。

### **九、对 BLP 安全模型的评价**

       BLP 模型是最早的一种安全模型，也是最有名的多级安全策略模型。它给出了军事安全策略的一种数学描述，用计算机可实现的方式定义。它已为许多操作系统所使用。

       由于它描述的是军事安全策略，受到美国国防部的特别推崇，以致于在很长一段时期人们将多级安全策略等同于强制访问控制策略。

       优点：①是一个最早地对多级安全策略进行描述的模型；

               ②是一个严格形式化的模型，并给出了形式化的证明；

③是一个很安全的模型，既有自主访问控制，又有强制访问控制。

④控制信息只能由低向高流动，能满足军事部门等一类对数据保密性要求特别高的机构的需求。

       1．总的来说，BLP 模型 “过于安全”。

              ①上级对下级发文受到限制；

              ②部门之间信息的横向流动被禁止；

              ③缺乏灵活、安全的授权机制。

       不安全的地方：

              ①低安全级的信息向高安全级流动，可能破坏高安全客体中数据完整性，被病毒和黑客利用。

②只要信息由低向高流动即合法（高读低），不管工作是否有需求，这不符合最小特权原则。

③高级别的信息大多是由低级别的信息通过组装而成的，要解决推理控制的问题。

2．仔细分析 BLP 模型，其描述上尚有不安全的地方，还有待改进，缺乏记忆，造成不安全性。

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>S</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>r</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>o<sub>2</sub></p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>高</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>低</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>o<sub>3</sub></p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>r</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>时刻 t<sub>1</sub></p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>时刻 t<sub>2</sub></p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>释放对 o<sub>2</sub>，o<sub>3</sub> 的访问权</p></td></tr></tbody></table>

例如：设

o1> o2> o3> o4

，

S

的安全级同

o1

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>S</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>a</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>o<sub>3</sub></p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>高</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>低</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>o<sub>4</sub></p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>r</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>时刻 t<sub>3</sub></p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>S 已含有 o<sub>2</sub> 和 o<sub>3</sub> 的信息</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>此时 S 可将 o<sub>2</sub> 的信息传送到 o<sub>3</sub></p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>(无记忆)</p></td></tr></tbody></table>

又例如：

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>oo</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>r</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>s<sub>2</sub></p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>高</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>更高</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>s<sub>1</sub></p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>a</p></td></tr></tbody></table>

<table cellpadding="0" cellspacing="0" width="100%"><tbody><tr><td><p>低</p></td></tr></tbody></table>

 **改进：针对过安全：**

1．允许高安全级的主体在受控的情况下创建低安全级的客体。（解决从上到下流的问题）。

       **２**．对客体安全级的动态约束，如（秘级，部门级，时限）。随客体内容进行动态约束（解决自上向下和横向）。

**３**．给主体发临时许可证，如（密级，部门级，时限）或（客体，权限，时限）。

 **针对不安全问题：**

       １．可否用 “推” 和“拉”来解决。用 “拉”，而不用“推”。在计算机中“推” 和“拉”如何实现？　　“同级写”

       ２．基于语义的动态控制；

       ３．问题比较复杂。
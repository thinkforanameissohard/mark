> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.csdn.net](https://blog.csdn.net/qq_22238021/article/details/80279001)

#### 一、OSI 七层模型

OSI 七层协议模型主要是：应用层（Application）、表示层（Presentation）、会话层（Session）、传输层（Transport）、网络层（Network）、数据链路层（Data Link）、物理层（Physical）。

#### 三、五层体系结构

五层体系结构包括：应用层、运输层、网络层、数据链路层和物理层。   
五层协议只是 OSI 和 TCP/IP 的综合，实际应用还是 TCP/IP 的四层结构。为了方便可以把下两层称为网络接口层。

三种模型结构：   
![](https://img-blog.csdn.net/20170822222325781?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvU2lsZW5jZU9P/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

![](https://img-blog.csdn.net/20170822224933262?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvU2lsZW5jZU9P/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

#### 四、各层的作用

##### 1、物理层：比特

主要定义物理设备标准，如网线的接口类型、光纤的接口类型、各种传输介质的传输速率等。它的主要作用是传输比特流（就是由 1、0 转化为电流强弱来进行传输, 到达目的地后在转化为 1、0，也就是我们常说的数模转换与模数转换）。这一层的数据叫做比特。 　　

##### 2、数据链路层：帧

定义了如何让格式化数据以进行传输，以及如何让控制对物理介质的访问。这一层通常还提供错误检测和纠正，以确保数据的可靠传输。 　　

##### 3、网络层：数据报

在位于不同地理位置的网络中的两个主机系统之间提供连接和路径选择。Internet 的发展使得从世界各站点访问信息的用户数大大增加，而网络层正是管理这种连接的层。 　　

##### 4、运输层：报文段 / 用户数据报

定义了一些传输数据的协议和端口号（WWW 端口 80 等），如：   
TCP（transmission control protocol –传输控制协议，传输效率低，可靠性强，用于传输可靠性要求高，数据量大的数据）   
UDP（user datagram protocol–用户数据报协议，与 TCP 特性恰恰相反，用于传输可靠性要求不高，数据量小的数据，如 QQ 聊天数据就是通过这种方式传输的）。 主要是将从下层接收的数据进行分段和传输，到达目的地址后再进行重组。常常把这一层数据叫做段。 　　

##### 5、会话层：

通过运输层（端口号：传输端口与接收端口）建立数据传输的通路。主要在你的系统之间发起会话或者接受会话请求（设备之间需要互相认识可以是 IP 也可以是 MAC 或者是主机名） 　　

##### 6、表示层：

可确保一个系统的应用层所发送的信息可以被另一个系统的应用层读取。例如，PC 程序与另一台计算机进行通信，其中一台计算机使用扩展二一十进制交换码（EBCDIC），而另一台则使用美国信息交换标准码（ASCII）来表示相同的字符。如有必要，表示层会通过使用一种通格式来实现多种数据格式之间的转换。 　　

7. 应用层：报文
---------

### 1 第五层——应用层 (application layer) 

*   应用层 (application layer)：是体系结构中的最高。直接为用户的应用进程（例如电子邮件、文件传输和终端仿真）提供服务。
*   在因特网中的应用层协议很多，如支持万维网应用的 HTTP 协议，支持电子邮件的 SMTP 协议，支持文件传送的 FTP 协议，DNS，POP3，SNMP，Telnet 等等。

### 2. 第四层——运输层 (transport layer)

*   运输层 (transport layer)：负责向两个主机中进程之间的通信提供服务。由于一个主机可同时运行多个进程，因此运输层有复用和分用的功能
*   复用，就是多个应用层进程可同时使用下面运输层的服务。
*   分用，就是把收到的信息分别交付给上面应用层中相应的进程。
*   运输层主要使用以下两种协议：   
    (1) 传输控制协议 TCP(Transmission Control Protocol)：面向连接的，数据传输的单位是报文段，能够提供可靠的交付。   
    (2) 用户数据包协议 UDP(User Datagram Protocol)：无连接的，数据传输的单位是用户数据报，不保证提供可靠的交付，只能提供 “尽最大努力交付”。

### 3. 第三层——网络层 (network layer)

*   网络层 (network layer) 主要包括以下两个任务：
*   (1) 负责为分组交换网上的不同主机提供通信服务。在发送数据时，网络层把运输层产生的报文段或用户数据报封装成分组或包进行传送。在 TCP/IP 体系中，由于网络层使用 IP 协议，因此分组也叫做 IP 数据报，或简称为数据报。
*   (2) 选中合适的路由，使源主机运输层所传下来的分组，能够通过网络中的路由器找到目的主机。
*   协议：IP,ICMP,IGMP,ARP,RARP

### 4. 第二层——数据链路层 (data link layer)

*   数据链路层 (data link layer)：常简称为链路层，我们知道，两个主机之间的数据传输，总是在一段一段的链路上传送的，也就是说，在两个相邻结点之间传送数据是直接传送的 (点对点)，这时就需要使用专门的链路层的协议。
*   在两个相邻结点之间传送数据时，数据链路层将网络层交下来的 IP 数据报组装成帧 (framing)，在两个相邻结点之间的链路上 “透明” 地传送帧中的数据。
*   每一帧包括数据和必要的控制信息 (如同步信息、地址信息、差错控制等)。典型的帧长是几百字节到一千多字节。
*   注：”透明”是一个很重要的术语。它表示，某一个实际存在的事物看起来却好像不存在一样。”在数据链路层透明传送数据”表示无力什么样的比特组合的数据都能够通过这个数据链路层。因此，对所传送的数据来说，这些数据就 “看不见” 数据链路层。或者说，数据链路层对这些数据来说是透明的。   
    (1) 在接收数据时，控制信息使接收端能知道一个帧从哪个比特开始和到哪个比特结束。这样，数据链路层在收到一个帧后，就可从中提取出数据部分，上交给网络层。   
    (2) 控制信息还使接收端能检测到所收到的帧中有无差错。如发现有差错，数据链路层就简单地丢弃这个出了差错的帧，以免继续传送下去白白浪费网络资源。如需改正错误，就由运输层的 TCP 协议来完成。

### 5. 第一层——物理层 (physical layer)

*   物理层 (physical layer)：在物理层上所传数据的单位是比特。物理层的任务就是透明地传送比特流。

### 6. 数据在各层之间的传递过程

![](https://img-blog.csdn.net/20160126223713317)
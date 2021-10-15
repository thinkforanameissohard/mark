> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.csdn.net](https://blog.csdn.net/wdscq1234/article/details/52677419)

> IPSec核心协议是AH和ESP，本文主要介绍下AH协议的数据封装与传输

> 供校验功能，并没有提供加密功能，

> AH 协议封装的数据包，会在 IP Header 和 TCP Header 之间增加一个 AH header

> 隧道模式下

> 数据报的完整性校验值
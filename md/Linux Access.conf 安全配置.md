> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [www.cnblogs.com](https://www.cnblogs.com/yizhipanghu/p/14241923.html)

> access.conf is the configuration file used to logins to the Linux or Unix systems. This file is

`access.conf` is the configuration file used to logins to the Linux or Unix systems. This file is locate at `/etc/security/` path.  With this file logins of users, groups, hosts, tty, network are defined to allows or disallowed status. Each line specifies a rule.

`access.conf`是用于登录 Linux 或 Unix 系统的配置文件。 该文件位于`/etc/security/`路径。 使用此文件，用户，组，主机，tty，网络的登录名被定义为允许或禁止状态。 每行指定一个规则。

句法 (Syntax)
===========

```
permission:users/groups:origins
```

Show Services Using Access.conf

使用 Access.conf 显示服务

允许规则 (Allow Rule)
=================

As we stated before each line is a rule. The aim of the rules are allowing or denying access with related parameters. Allow rule is sign is `+` . Each line starting with `+` means allow. After the sign there is `:` to delimit rule parameters. In the example we allow some access for the `root` user.

如前所述，每行都是一条规则。 规则的目的是允许或拒绝具有相关参数的访问。 允许规则的符号是`+` 。 每行以`+`开头表示允许。 在标志之后有`:`分隔规则参数。 在示例中，我们允许`root`用户进行某些访问。

```
+ : root : 192.168.200.1 192.168.200.4 192.168.200.9
```

拒绝规则 (Deny Rule)
================

Deny rule is used to deny access with specified parameters. Deny rules tarts with`-` sign and delimited with`:` from the rule parameters. Following example rules denies access for the root account.

拒绝规则用于拒绝具有指定参数的访问。 从规则参数中拒绝带有`-`号的规则 rules，并以`:`分隔。 以下示例规则拒绝对根帐户的访问。

```
- : root : ALL
```

只允许根访问 (Allow Only Root Access)
===============================

There are different type of access restrictions. One of them is only allowing root user to access to the server. In this rule root user can access from everywhere to the system.

有不同类型的访问限制。 其中之一是仅允许 root 用户访问服务器。 在此规则中，root 用户可以从任何地方访问系统。

```
+ : root : ALL
```

指定允许的用户 (Specify Allowed User)
==============================

We can specify the user account which can access to the server. We will give the user `ismail` access right to the server from everywhere.

我们可以指定可以访问服务器的用户帐户。 我们将使用户`ismail`从任何地方都可以访问服务器。

```
+ : ismail : ALL
```

指定允许的组 (Specify Allowed Group)
==============================

While specifying access for the user name if there area lot of users those can access to the server can be a problem for definition and management. Acess.conf supports Linux user groups. These groups can be used to give access to the server. We assume we have a group named `remoteacess` and this group members can access to the server from anywhere.

在为用户名指定访问权限时 (如果有很多用户可以访问服务器) 可能是定义和管理的问题。 Acess.conf 支持 Linux 用户组。 这些组可用于授予对服务器的访问权限。 我们假设有一个名为`remoteacess`的组，该组成员可以从任何地方访问服务器。

```
+ : @admins : ALL
```

指定允许的主机 (Specify Allowed Hosts)
===============================

Another useful option is setting hosts those can be connect to the system. Host names or IP addresses can be specified like below. In the example we only allow IP address `192.168.200.1` to connect to the system.

另一个有用的选项是设置可以连接到系统的主机。 可以如下指定主机名或 IP 地址。 在该示例中，我们仅允许 IP 地址`192.168.200.1`连接到系统。

```
+ : root : 192.168.200.1
```

指定允许的网络 (Specify Allowed Network)
=================================

Specifying IP ranges one by one is daunting task. We can use network and netmask specification do define networks to allow access. In the following example we allow `root` user access from network `10.0.0.0/24` or `10.0.0.0-255` with `10.0.0.` expression.

一一指定 IP 范围是一项艰巨的任务。 我们可以使用网络和网络掩码规范来定义允许访问的网络。 在下面的例子中，我们允许`root`从网络用户访问`10.0.0.0/24`或`10.0.0.0-255`与`10.0.0.` 表达。

```
+ : root : 10.0.0.
```

拒绝仅根访问 (Deny Only Root Access)
==============================

Previous examples we have looked how to allow some users, groups, IP addresses and networks to the system. But security comes from deny operation. Up to new we will look how to deny users with specified parameter to access to the system. In this example user `root` can not access system remotely from anywhere.

在前面的示例中，我们研究了如何允许某些用户，组，IP 地址和网络进入系统。 但是安全性来自拒绝操作。 到最新为止，我们将研究如何拒绝具有指定参数的用户访问系统。 在此示例中， `root`用户无法从任何地方远程访问系统。

```
- : root : ALL
```

指定拒绝的用户 (Specify Denied User)
=============================

We can specify user to deny access to the system. In this example user `ismail` can not access to the system from anywhere.

我们可以指定用户拒绝对系统的访问。 在此示例中，用户`ismail`无法从任何地方访问系统。

```
- : ismail : ALL
```

指定允许的组 (Specify Allowed Group)
==============================

As shown previous examples a Linux user group can be defined fo deny access to the system. In the example we will deny access for `students` group from anywhere.

如前面的示例所示，可以定义 Linux 用户组以拒绝访问系统。 在示例中，我们将拒绝从任何地方访问`students`组。

```
- : @students : ALL
```

指定拒绝的主机 (Specify Denied Hosts)
==============================

We can specify hosts to deny access to the system. We will use same syntax like allow rule but change the rule sign with `-` . In the example we  deny access from `192.168.200.1` to the system.

我们可以指定主机以拒绝对系统的访问。 我们将使用与 allow rule 相同的语法，但使用`-`更改规则符号。 在示例中，我们拒绝从`192.168.200.1`到系统的访问。

```
- : root : 192.168.200.1
```

指定拒绝的网络 (Specify Denied Network)
================================

We can specify denied network with `-` sign, username and the network address. In the example we will deny `10.0.0.0/24` from accessing with root user to the system.

我们可以使用`-`符号，用户名和网络地址指定拒绝的网络。 在该示例中，我们将拒绝`10.0.0.0/24`通过 root 用户访问系统。

```
- : root : 10.0.0.
```

异常定义 (Exception Definition)
===========================

Up to now we have specified and defined the users , host names, groups and networks. We have the ability to except these. In the example we allow all users access to the system except `root` . We can also specify group names to except.

到目前为止，我们已经指定并定义了用户，主机名，组和网络。 我们有能力排除这些。 在该示例中，我们允许除`root`之外的所有用户访问系统。 我们还可以将组名指定为 except。

```
+ : ALL EXCEPT (root) : ALL
```

全部拒绝 (Deny All)
===============

The readers who worked with firewalls knows the golden rule. After specifying different access rules the best practice is defining last rule as `DENY ALL` . This will make system very secure. This simply imply that I only allow those connections I defined and deny all others. Put this rule to the end of the rules in `access.conf` file.

使用防火墙的读者知道黄金法则。 指定不同的访问规则后，最佳做法是将最后一个规则定义为`DENY ALL` 。 这将使系统非常安全。 这仅表示我只允许我定义的那些连接，而拒绝所有其他连接。 将此规则放在`access.conf`文件中规则的末尾。

```
- : ALL : ALL
```

LEARN MORE  SSH Tutorial With Command Examples

通过命令示例了解更多 SSH 教程

> 翻译自: [https://www.poftut.com/access-conf-security-configuration-linux-unix/](https://www.poftut.com/access-conf-security-configuration-linux-unix/)
> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [www.360doc.com](http://www.360doc.com/content/19/0802/16/12765144_852599244.shtml)

> 安全开发流程（SDL）

SDL security development lifecycle（安全开发生命周期），是[微软](http://baike.baidu.com/item/%E5%BE%AE%E8%BD%AF)提出的从安全角度指导软件开发过程的管理模式。SDL 是一个安全保证的过程，起重点是**软件开发**，它在开发的所有阶段都引入了安全和隐私的原则。自 2004 年起，SDL 一直都是微软在全公司实施的强制性策略。

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAACbklEQVRoQ+2aMU4dMRCGZw6RC1CSSyQdLZJtKQ2REgoiRIpQkCYClCYpkgIESQFIpIlkW+IIcIC0gUNwiEFGz+hlmbG9b1nesvGW++zxfP7H4/H6IYzkwZFwQAUZmpJVkSeniFJKA8ASIi7MyfkrRPxjrT1JjZ8MLaXUDiJuzwngn2GJaNd7vyP5IoIYY94Q0fEQIKIPRGS8947zSQTRWh8CwLuBgZx479+2BTkHgBdDAgGAC+fcywoyIFWqInWN9BSONbTmFVp/AeA5o+rjKRJ2XwBYRsRXM4ZXgAg2LAPzOCDTJYQx5pSIVlrC3EI45y611osMTHuQUPUiYpiVooerg7TWRwDAlhSM0TuI+BsD0x4kGCuFSRVzSqkfiLiWmY17EALMbCAlMCmI6IwxZo+INgQYEYKBuW5da00PKikjhNNiiPGm01rrbwDwofGehQjjNcv1SZgddALhlJEgwgJFxDNr7acmjFLqCyJuTd6LEGFttpmkYC91Hrk3s1GZFERMmUT01Xv/sQljjPlMRMsxO6WULwnb2D8FEs4j680wScjO5f3vzrlNJszESWq2LYXJgTzjZm56MCHf3zVBxH1r7ftU1splxxKYHEgoUUpTo+grEf303rPH5hxENJqDKQEJtko2q9zGeeycWy3JhpKhWT8+NM/sufIhBwKI+Mta+7pkfxKMtd8Qtdbcx4dUQZcFCQ2I6DcAnLUpf6YMPxhIDDOuxC4C6djoQUE6+tKpewWZ1wlRkq0qUhXptKTlzv93aI3jWmE0Fz2TeujpX73F9TaKy9CeMk8vZusfBnqZ1g5GqyIdJq+XrqNR5AahKr9CCcxGSwAAAABJRU5ErkJggg==)

SDL 中的方法，试图从安全漏洞产生的根源上解决问题，通过对软件工程的控制，保证产品的安全性。

美国国家标准与技术研究所（NIST）估计，如果是在项目发布后在执行漏洞修复计划，其修复成本相当于在设计阶段执行修复的 30 倍

**阶段 1：培训**

开发团队的所有成员都必须接受适当的安全培训，了解相关的安全知识，培训对象包括开发人员、测试人员、项目经理、产品经理等。

**阶段 2：安全要求**

在项目确立之前，需要提前与项目经理或者产品 owner 进行沟通，确定安全的要求和需要做的事情。确认项目计划和里程碑，尽量避免因为安全问题而导致项目延期发布。

**阶段 3：质量门 / bug 栏**

质量门和 bug 栏用于确定安全和隐私质量的最低可接受级别。

Bug 栏是应用于整个开发项目的质量门，用于定义安全漏洞的严重性阈值。例如，应用程序在发布时不得包含具有 “关键” 或“重要”评级的已知漏洞。Bug 栏一经设定，便绝不能放松。

**阶段 4：安全和隐私风险评估**

安全风险评估（SRA）和隐私风险评估 (PRA) 是一个必需的过程，必须包括以下信息：

1、（安全）项目的哪些部分在发布前需要威胁模型？

2、（安全）项目的哪些部分在发布前需要进行安全设计评析？

3、（安全）项目的哪些部分需要并不食欲项目团队且双方认可的小组进行渗透测试？

4、（安全）是否存在安全顾问认为有必要增加的测试或分析要求已缓解安全风险？

5、（安全）模糊测试要求的具体范围是什么？

6、（安全）隐私影响评级如何？

**阶段 5：设计要求**

在设计阶段应仔细考虑安全和隐私问题，在项目初期确定好安全需求，尽可能避免安全引起的需求变更。

**阶段 6：减小攻击面**

减小攻击面与威胁建模紧密相关，不过它解决安全问题的角度稍有不同。减小攻击面通过减小攻击者利用潜在弱点或漏洞的机会来降低风险，减小攻击面包括：关闭或限制对系统服务的访问，应用 “最小权限原则”，以及尽可能进行分层防御。

**阶段 7：威胁建模**

为项目或产品面临的威胁建立模型，明确可能来自的攻击有哪些方面。

**阶段 8：使用指定的工具**

开发团队使用的编辑器、链接器等相关工具，可能会涉及一些安全相关的环节，因此在使用工具的版本上，需要提前与安全团队进行沟通。

**阶段 9：弃用不安全函数**

许多常用函数可能存在安全隐患，应当禁用不安全的函数和 API，使用安全团队推荐的函数。

**阶段 10：静态分析**

代码静态分析可以由相关工具辅助完成，其结果与人工分析相结合。

**阶段 11：动态程序分析**

动态分析是静态分析的补充，用于测试环节验证程序的安全性。

**阶段 12：模糊测试（Fuzzing Test）**

模糊测试是一种专门形式的动态分析，它通过故意向应用程序引入不良格式或随机数据诱发程序故障。模糊测试策略的制定，以应用程序的预期用途，以及应用程序的功能和设计规范为基础。安全顾问可能要求进行额外的模糊测试，或者扩大模糊测试的范围和增加持续时间。

**阶段 13：威胁模型和攻击面评析**

项目经常会因为需求等因素导致最终的产出偏离原本设定的目标，因此在项目后期对威胁模型和攻击面进行评析是有必要的，能够及时发现问题并修正。

**阶段 14：事件响应计划**

受 SDL 要求约束的每个软件在发布时都必须包含事件响应计划。即使在发布时不包含任何已知漏洞的产品，也可能在日后面临新出现的威胁。需要注意的是，如果产品中包含第三方的代码，也需要留下第三方的联系方式并加入事件响应计划，以便在发生问题时能够找到对应的人。

**阶段 15：最终安全评析**

最终安全评析（FSR）是在发布之前仔细检查对软件执行的所有安全活动。通过 FSR 将得出以下三种不同不同结果。

1、  通过 FSR。在 FSR 过程中确定所有安全和隐私问题都已得到修复或缓解。

2、  通过 FSR 但有异常。在 FSR 过程中确定所有安全和隐私问题都已得到修复或缓解，并且 / 或者所有异常都已得到圆满解决。无法解决的问题将记录下来，在下次发布时更正。

3、  需上报问题的 FSR。如果团队未满足所有 SDL 要求，并且安全顾问和产品团队无法达成可接受的折中，则安全顾问不能批准项目，项目不能发布。团队必须在发布之前解决所有可解决的问题，或者上报高级管理层进行抉择。

**阶段 16：发布 / 存档**

在通过 FSR 或者虽有问题但达成一致后，可以完成产品的发布。但发布的同时仍需对各种问题和文档进行存档，为紧急响应和产品升级提供帮助。  
从以上的过程可以看出，微软的 SDL 的过程实施非常细致。微软这些年来也一直帮助公司的所有产品团队，以及合作伙伴实施 SDL，效果相当显著。

相对于微软的 SDL，OWASP 推出了 SAMM（Software Assurance Maturity Model），帮助开发者在软件工程的过程中实施安全

 ![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAACbklEQVRoQ+2aMU4dMRCGZw6RC1CSSyQdLZJtKQ2REgoiRIpQkCYClCYpkgIESQFIpIlkW+IIcIC0gUNwiEFGz+hlmbG9b1nesvGW++zxfP7H4/H6IYzkwZFwQAUZmpJVkSeniFJKA8ASIi7MyfkrRPxjrT1JjZ8MLaXUDiJuzwngn2GJaNd7vyP5IoIYY94Q0fEQIKIPRGS8947zSQTRWh8CwLuBgZx479+2BTkHgBdDAgGAC+fcywoyIFWqInWN9BSONbTmFVp/AeA5o+rjKRJ2XwBYRsRXM4ZXgAg2LAPzOCDTJYQx5pSIVlrC3EI45y611osMTHuQUPUiYpiVooerg7TWRwDAlhSM0TuI+BsD0x4kGCuFSRVzSqkfiLiWmY17EALMbCAlMCmI6IwxZo+INgQYEYKBuW5da00PKikjhNNiiPGm01rrbwDwofGehQjjNcv1SZgddALhlJEgwgJFxDNr7acmjFLqCyJuTd6LEGFttpmkYC91Hrk3s1GZFERMmUT01Xv/sQljjPlMRMsxO6WULwnb2D8FEs4j680wScjO5f3vzrlNJszESWq2LYXJgTzjZm56MCHf3zVBxH1r7ftU1splxxKYHEgoUUpTo+grEf303rPH5hxENJqDKQEJtko2q9zGeeycWy3JhpKhWT8+NM/sufIhBwKI+Mta+7pkfxKMtd8Qtdbcx4dUQZcFCQ2I6DcAnLUpf6YMPxhIDDOuxC4C6djoQUE6+tKpewWZ1wlRkq0qUhXptKTlzv93aI3jWmE0Fz2TeujpX73F9TaKy9CeMk8vZusfBnqZ1g5GqyIdJq+XrqNR5AahKr9CCcxGSwAAAABJRU5ErkJggg==)

SAMM 与 SDL 的主要区别在于，SDL 适用于软件开发商，他们以贩售软件为主要业务；而 SAMM 更适用于自主开发软件的使用者，如银行或在线服务提供商。软件开发商的软件工程往往较为成熟，有着严格的质量控制；而自主开发软件的企业组织，则更强调高效，因此在软件工程的做法上也存在差异。

准则一：与项目经理进行充分沟通，排除足够的时间

准则二：规范公司的立项流程，确保所有项目都能通知到安全团队，避免遗漏

准则三：树立安全部门的权威，项目必须由安全部门审核完成后才能发布

准则四：将技术方案写入开发、测试的工作手册中

准则五：给工程师培训安全方案

准则六：记录所有的安全 bug，激励程序员编写安全的代码
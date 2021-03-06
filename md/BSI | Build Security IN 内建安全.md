> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [www.buildsecurityin.cn](http://www.buildsecurityin.cn/zh/article/1-software-development-and-security.html)

> BSI(Build Security In) 安全内建软件开发是一种以各种软件安全实践为主的开发实践体系，可以帮助并促使开发团队能够更早、更迅速并且持续性的在开发过程中从源头发现并解决应用安全问题。

我们开发的软件安全吗？
-----------

“Build Security In DNA”，简称 “BSI”，是一种新的构建具备安全基因的软件开发方式。正如它的名字里提到的那样，把各种安全实践内建到软件开发的各个关键节点之中，通过尽早引入安全实践以及快速获取安全反馈的方式，从问题的源头着手避免安全问题的产生。在详细介绍 BSI 之前，让我们先通过一个案例，来看看现如今企业面临着哪些安全困境。

### 案例：

A 公司是一家互联网金融类公司，计划打造一款自己的 P2P 产品，这就需要进行 Web 端、移动 App、基于 Web 的业务管理端，以及后端服务器核心业务的开发，架构示意图如下。产品上线日期早已选定，开发团队只有 3 个月的时间来完成这一任务。

![](http://www.buildsecurityin.cn/assets/images/article/article-1-1.jpg)

由于 P2P 产品本身的特点，不仅涉及到大规模资金处理又存储着大量用户隐私数据，所以它天生注定是黑客的首选攻击目标。A 公司非常明白，自己的产品一旦爆出安全事件，必然会遭受财物损失、陷入法律纠纷之中，在行业中的声誉也将一败涂地。

安全事件带来的严重后果让 A 公司在安全方面不敢懈怠，他们制定了安全规范，例如：安全编码规范、安全测试规范、信息安全规范等等，并且设立严格的惩罚规则，不仅如此，还把安全漏洞数量纳入到员工绩效考核之中，希望通过这些方式督促团队成员关注安全。A 公司的员工也认同安全的重要性，可是由于项目时间紧迫，开发工作量大，能赶在发布日之前完成开发工作已实属不易，再加上团队成员的安全技能并不多，所以在实际的开发过程中并没有人主动关注产品的安全。

这款 P2P 产品的核心功能开发完成之时，已经非常接近产品上线日期。A 公司有自己的安全团队，此时对产品进行了一次内部安全审查，检测出了一些安全问题，风险级别各有不同。虽然通过这种方式发现了潜在的安全问题，但是留给开发团队进行修复的时间相当有限，最终团队仅完成了高危险级别漏洞的修复，其余漏洞只能安排在上线之后再陆续修复。

产品发布后，不出所料遭受到了黑客的攻击，由于有提前制定的安全应急响应预案和较为完善的运营监控手段，团队立即采取了行动，及时修补了被黑客所利用的安全漏洞，同时市场部门进行危机公关，所幸没有造成严重的经济损失。

尽管 A 公司是虚构的，但是这个案例却是普遍现象。从 A 公司采取的安全措施来看，对于应对安全问题而言确实有一定的效果，但也只能起到缓解的作用，安全漏洞并没有显著减少，各种安全事件依然时有发生，其根本原因在于这些措施并不能从根源解决安全问题。

首先是安全审查介入时间太晚，不利于尽早发现并解决安全问题。这款 P2P 产品只有 3 个月的开发时间，核心功能完成之后就立即进行安全审查，开发团队基于安全报告对漏洞进行修复，看上去合情合理其实已经晚了。安全问题同业务缺陷相似，越晚发现其修复成本越高。由于安全评审只能在核心功能开发完毕后才能进行，理想情况下团队在第三个月初完成核心功能的开发，然而更多的时候，这类安全审查只能被安排在产品上线前一周左右进行，此时已经临近发布日期，因此修复安全问题的时间非常有限，给团队带来巨大的负担和压力。

![](http://www.buildsecurityin.cn/assets/images/article/article-1-2.jpg)

其次是反馈周期长。虽然能借助一些自动化的漏洞扫描工具加快速度，但是一次比较细致周全的安全审查，往往需要花费安全团队或者安全专家一周甚至几周的时间，开发团队只能耐心等待安全报告出炉，之后才能进行修复工作。而且随着项目规模的增大审查时间也会相应增加，更何况这并不是结束，团队拿到安全报告完成修复工作之后，还得再次进行安全审查以确保安全问题确实已被修复，并且没有引入新的安全问题。由于这样的安全审查时间成本高昂，所以这类审查通常只会进行一次，也就意味着开发团队在整个开发周期里只能得到一次安全问题的反馈，然而应用程序会随着新需求的加入和旧功能的调整而变化，这个过程中引入的新的安全问题并不能被及时的发现。

然后是被动的应对安全问题。在案例里，A 公司虽然有应急预案，有运营监控手段做支撑，甚至还通过安全审查来暴露问题，但这些统统都是事后弥补，对于安全问题而言，只能是发现一个解决一个。在这种情况下，开发团队就会陷入被动应对安全问题的泥潭，谁都不清楚产品里还埋藏着哪些安全问题，也不知道下一秒会不会爆发。

另外，一个相当普遍的误解是，认为产品的安全性理所当然应该由安全团队来负责，开发团队只需专注于业务功能的实现。这就容易形成矛盾，开发团队承认安全的重要性，但由于项目交付压力大，往往会认为安全团队是在给项目正常交付添乱，而安全团队则认为是开发团队不配合，安全工作流于形式，难以推动。另外，团队自身缺乏足够的安全技能既是造成这个误解的原因之一，同时也是这个误解的产物。

最后，以上提到的传统安全实践的效果如何值得商榷。安全审查确实能发现问题，但是受限于安全团队的能力，很可能无法检测出产品中的所有安全问题，于是造成了一个非常尴尬的局面：经过内部安全审查后的应用依然不安全，公司不得不聘请第三方安全公司进行二次审查，这不仅是对公司自有安全团队的沉重打击，也是相当严重的资源浪费，更何况，第三方安全公司主导的渗透测试就能发现所有的安全问题吗？很可惜答案是否定的，由于第三方安全公司不了解企业的业务，很多业务逻辑上的安全问题无法被发现。另外，公司设立了各类安全规范、行为准则，虽然有其必要性，可是效果基本是微乎其微，一个普遍现象是，每个人都知道公司有规范准则，但是没有几个人知道里面的具体内容，更不用提严格遵守和执行了。而把安全漏洞数量纳入到绩效考核之后，很容易让开发团队和安全团队形成对立，开发团队会想尽办法隐瞒安全漏洞，而不是尽早暴露尽早修复。

由于以上措施的种种不足，BSI 则应运而生：在应用开发的各个关键环节引入合适的安全实践，利用自动化的优势缩短安全问题的反馈周期，加快反馈速度，通过威胁建模、安全驱动开发等手段主动预知并化解安全问题。在减轻开发团队和安全团队负担的同时，提高发现、解决安全问题的效率。

BSI 并不是颠覆性的创新产物，早在上世纪 80 年代，螺旋模型开发方式就已经提出了类似的概念，尽管如此，时至今日依然很少有团队深刻理解了这一思想的精髓并付诸实践。如果当初他们采纳了 BSI 的话，那些被媒体报道的惨痛安全事件可能就没有发生的机会了。

既然 BSI 能很好的解决企业所面临的安全困境，那它和传统的安全实践到底有哪些区别？BSI 是如何做到能够尽早发现和解决安全问题的？它给项目团队带来了哪些影响？BSI 是今后发展的趋势吗？这些问题的答案将会在后续的章节里逐一揭晓，敬请期待。
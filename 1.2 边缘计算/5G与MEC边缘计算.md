- [5G 与 MEC 边缘计算](https://www.cnblogs.com/jmilkfan-fanguiju/p/11825026.html)

## 前言

本篇文章主要为学习记录、资料整理，文中大量内容来自网络，详见参考文献。

## 参考文献

https://www.huxiu.com/article/259186.html
 http://www.fjii.com/kj/jsc/2018/0830/179967.shtml
 https://www.sohu.com/a/125297875_465915
 https://www.sdnlab.com/19818.html
 http://blueskyfreeway.blogspot.com/2018/07/5g-1-itu-2020-ran.html
 http://blueskyfreeway.blogspot.com/2018/07/5g-2-mec-mobile-edge-computing.html
 http://blueskyfreeway.blogspot.com/2018/07/5g-3-next-generation-core-ngc-or-5g.html
 https://blog.csdn.net/gongxifacai_believe/article/details/80804841?utm_source=app
 https://blog.csdn.net/gongxifacai_believe/article/details/80807176?utm_source=app
 https://blog.csdn.net/gongxifacai_believe/article/details/80811247?utm_source=app
 https://mp.weixin.qq.com/s/-5wx2cuL7tppho0_wA9mSA
 https://www.etsi.org/deliver/etsi_gs/MEC/001_099/003/02.01.01_60/gs_MEC003v020101p.pdf
 https://www.etsi.org/deliver/etsi_gr/MEC/001_099/017/01.01.01_60/gr_MEC017v010101p.pdf
 https://www.etsi.org/images/files/ETSIWhitePapers/etsi_wp28_mec_in_5G_FINAL.pdf

## 通信网络

电信网（即电话交换网络）由终端、传输和交换三大部分组成；因特网（即计算机互联网）由终端、传输、交换以及多个计算机网络等几部分组成。随着通信行业的快速发展，传统的电信网、计算机互联网与有线电视网的融合（三网融合）已经成为网络发展的趋势。三者融合发展，互联互通，为客户同时提供语音、数据和广播电视等多重服务。这里我们将其统一称之为通信网络。相对应的，通信网络由三大部分组成：接入网、承载网、核心网。

- 接入网是 “窗口”，负责把数据收上来；
- 承载网是 “卡车”，负责把数据送来送去；
- 核心网就是 “管理中枢”，负责管理这些数据，对数据进行分拣，然后告诉它，该去何方。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924123422195.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

## 核心网演进之路

核心网（Core Network，简称 CN）或被成为骨干网（Backbone），本质就是对数据的处理和分发，即 “路由交换”。

### 早古时期

最早的时候，固定电话网的核心网，说白了就是把电线两头的电话连接起来，这种交换，非常简单，主要满足人们无线移动通话的需求。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924143219493.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

后来，用户数量越来越多，网络范围越来越大，开始有了分层。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924143238409.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)
 网络架构也复杂了，有了网络单元（Net Element，简称 NE，网元），是具有某种功能的网络单元实体。

同时，我们要识别和管理用户了，不是任何一个用户都允许用这个通信网络，只有被授权的合法用户，才能使用。于是，多了一堆和用户有关的网元设备。它们的核心任务只有三个：认证、授权和记账，简称 3A。
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924143412972.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)
 再后来，有了无线通信，连接用户的方式变了，从电话线变成无线电波，无线接入网（RAN，Radio Access  Network）诞生。接入网变了，核心网也要跟着变，于是有了无线核心网。再再后来，有了  2G、3G、4G。每一代通信标准，每一项具体制式，都有属于自己的网络架构，自己的硬件平台，自己的网元，自己的设备。

### 2G 网络架构

第二代蜂窝移动通信系统出现在数字蜂窝技术的发展与成熟之后，为了进一步提高通话的质量，推出了数字化语音业务的第二代蜂窝移动通信系统。 2G 的核心网设备如下，名字就叫 MSC（Mobile Switching Center，移动交换中心）。
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924143519510.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)
 2G 的网络架构如下，组网非常简单，MSC 就是核心网的最主要设备。HLR、EIR 和用户身份有关，用于鉴权。
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924143652654.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)
 后来，到了 2.5G，在 2G 和 3G 之间，就是 GPRS。
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924143820994.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)
 在之前 2G 只能打电话发短信的基础上，有了 GPRS，就开始有了数据（上网）业务。于是，核心网的网络架构有了大变化，开始有了  PS（Packet Switch，分组交换，包交换）核心网。如下图红色部分，包含 SGSN（Serving GPRS Support  Node，服务 GPRS 支持节点）和 GGSN（Gateway GPRS Support Node，网关 GPRS 支持节点）。SGSN 和  GGSN 都是为了实现 GPRS 数据业务。

![在这里插入图片描述](https://img-blog.csdnimg.cn/201909241439244.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)
 从 2000 年 GPRS 首商用到 2020 年 5G 到来，不禁为移动通信迅猛发展之势而感慨。数据速率从 2G GPRS 65Kbit/s 到 LTE-A 1Gbit/s，再到 5G 时代 10-20Gbit/s，增长速度令人吃惊。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924172953170.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

### 3G 网络架构

20 世纪末，IP 和互联网技术的快速发展改变了人们的通信方式，传统的语音通信的吸引力下降，人们期望无线移动网络也能够提供互联网业务，于是出现了能够提供数据业务的第三代移动通信系统。

2.5G 到了 3G，网络结构变成了下图模样。而 3G 基站，由 RNC 和 BSC 组成。
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/2019092414404810.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)
 到了 3G 阶段，设备商的硬件平台进行彻底变革升级。3G 的核心网设备如下：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924144656409.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)
 3G 除了硬件变化和网元变化之外，还有两个很重要的思路变化。其中之一，就是 IP 化。以前是 TDM 电路，就是 E1 线，中继电路。粗重的  E1 线缆 IP 化，就是 TCP/IP，以太网。网线、光纤开始大量投入使用，设备的外部接口和内部通讯，都开始围绕 IP 地址和端口号进行。

第二个思路变化，就是分离。具体来说，就是网元设备的功能开始细化，不再是一个设备集成多个功能，而是拆分开，各司其事。在 3G  阶段，是分离的第一步，叫做承载和控制分离。在通信系统里面，说白了，就两个（平）面，用户面和控制面。如果不能理解两个面，就无法理解通信系统。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924144945616.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

- 用户面，就是用户的实际业务数据，就是你的语音数据，视频流数据之类的。
- 控制面，是为了管理数据走向的信令、命令。

这两个面，在通信设备内部，就相当于两个不同的系统，2G 时代，用户面和控制面没有明显分开。3G 时代，把两个面进行了分离。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924145029218.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

从 R7 开始，通过 Direct Tunnel 技术将控制面和用户面分离，在 3G RNC 和 GGSN 之间建立了直连用户面隧道，用户面数据流量直接绕过 SGSN 在 RNC 和 GGSN 之间传输。到了 R8，出现了 MME 这样的纯信令节点。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924173058343.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

### 4G 网络架构

第四代移动通信系统提供了 3G 不能满足的无线网络宽带化。4G 网络是全 IP 化网络，主要提供数据业务，其数据传输的上行速率可达 20Mbit/s，下行速率高达 100Mbit/s，基本能够满足各种移动通信业务的需求。

4G 网络架构中，SGSN 变成 MME（Mobility Management Entity，移动管理实体），GGSN 变成  SGW/PGW（Serving Gateway，服务网关；PDN Gateway，PDN 网关），也就演进成了 4G 核心网，如下图。

MME（移动性管理实体）的主要功能是支持 NAS（非接入层）信令及其安全、跟踪区域（TA）列表的管理、PGW 和 SGW 的选择、跨  MME 切换时进行 MME 的选择、在向 2G/3G 接入系统切换过程中进行 SGSN 的选择、用户的鉴权、漫游控制以及承载管理、3GPP  不同接入网络的核心网络节点之间的移动性管理（终结于 S3 节点），以及 UE 在 ECM_IDLE  状态下可达性管理（包括寻呼重发的控制和执行）。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924145122616.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

4G LTE 网络架构（注意，基站里面的 RNC 没有了，为了实现扁平化，功能一部分给了核心网，另一部分给了 eNodeB）。2009  年，在部署 LTE/EPC（4G 核心网）的时候，有人认为核心网演进之路已经走到尽头，继续突破创新实在太难，毕竟要掌控每小区峰值速率  150Mbps 的网络王国，实在是一件不容易的事。然而，随着 VoLTE 和 VoWiFi 的出现，LTE/EPC 又引入了 S2a、S2b 和 S2c 接口，这些接口将核心网的控制范围延伸到了非 3GPP 网络，即可信 Non-3GPP 接入（Non-3GPP Trusted  Access）和非可信 Non-3GPP 接入（Non-3GPP untrusted Access）连接到 3GPP 网关  PGW。自此，核心网的构架如下图所示，图中绿色实线表示用户面 & 控制面接口。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924162414120.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

演进到 4G 核心网之前，硬件平台也提前升级了。以中兴为例，开始启用 ATCA/ETCA 平台（后来 MME 就用了它），还有 xGW T8000 平台（后面 PGW 和 SGW 用了它，PGW/SGW 物理上是一体的）。

- ATCA（Advanced Telecom Computing Architecture，先进电信计算架构）机框
- ETCA（Enhanced ATCA，增强型 ATCA）
- xGW T8000 硬件平台其实就是一个大路由器

ATCA 里面的业务处理单板，本身就是一台单板造型的 “小型化电脑”，有处理器、内存、硬盘，我们俗称 “刀片”。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924150115189.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

既然都走到这一步，原来的专用硬件，越做越像 IT 机房里面的 x86 通用服务器，那么，不如干脆直接用 x86 服务器吧。

长久以来，网络越来越庞大，越来越复杂，而那些专用的电信设备不但扩展不灵活，而且习惯了自扫门前雪，整体效率太低，如同公司的体制，这是一个庞大而臃肿的机构，仿佛背着世界前行。所以电信运营商要打破传统，用 IT  的方式来重构网络。而虚拟化打通了开源平台，让更多的第三方和合作伙伴参与进来，从而在已运行多年的成熟的电信网络上激发更多的创新和价值。这正是  NGMN 的愿景：生态、客户和商业模式。于是，网元功能虚拟化（Network Function  Virtualization，NFV）的时代到来了。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924150223731.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)
 软件上，设备商基于 OpenStack 开发自己的虚拟化平台，把以前的核心网网元，“种植” 在这个平台之上。网元功能软件与硬件实体资源分离
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924150303141.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

设备商先在虚拟化平台部署 4G 核心网，也就是，在为后面 5G 做准备，提前实验。硬件平台，永远都会提前准备。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924150404907.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

## 5G

NGMN 是这样定义 5G 的：5G 是一个端到端的生态系统，它将打造一个全移动和全连接的社会。5G 主要包括三方面：生态、客户和商业模式。它交付始终如一的服务体验，通过现有的和新的用例，以及可持续发展的商业模式，为客户和合作伙伴创造价值。

比起 2/3/4G 时代主要局限于接入网和随之演进的核心网，更多聚焦于技术。5G 的野心是 “端到端” 的系统构架。从技术上讲，5G  还将实现电信也从未有过的软件和硬件分离，并引入 IT 数据中心所采用的云化和虚拟化的概念。简而言之，2/3/4G  是技术推动单调的服务和商业模式，而 5G 要运用各种技术去满足和支持持续变化的生态和商业模式。

如果说 4G 时代的智能终端技术全面促进了传统 PC 互联网同移动网络的深度融合，那么在 5G 时代，MEC  技术将会推动云计算平台同移动网络的融合，并可能在技术及商业生态上带来新一轮的变革和颠覆。 电信产业经历过辉煌，但如今跌入低谷，5G  将是电信产业重返辉煌的机会。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924153555274.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

### 5G 网络的需求

国际电信联盟（ITU，International Telecommunication  Union）针对每一个新世代的网络，都会制定出需求及应用场景，而各大电信标准组织，再依照 ITU 所提出的需求，订定标准并向 ITU  提交标准，供 ITU 审订。5G 提交的标准为  IMT-2020（https://www.itu.int/en/ITU-R/study-groups/rsg5/rwp5d/imt-2020/Pages/default.aspx）。

ITU 在 IMT-2020 中订定了 5G 的八大  KPI（https://www.itu.int/en/ITU-D/Regional-Presence/ArabStates/Documents/events/2018/RDF/Workshop%20Presentations/Session1/5G-%20IMT2020-presentation-Marco-Carugi-final-reduced.pdf）：

1. 更好的使用者传输速率体验（User Experienced Data Rate）：100 Mb/s 以上
2. 更高的峰值传输速率（Peak Data Rate）：20Gb/s
3. 单位面积在单位时间内更高的传输数据量（Traffic Capacity）：10~100Mb/s/m2
4. 更高的频谱使用率（Spectrum Effiency）：3 倍以上
5. 更快的移动速度（Mobility）：500km/h
6. 更低的延迟（Latency）：1ms 以下
7. 更高密度的装置联机（Connection Dencity）：100 万 devices/km2
8. 更低的耗能（Network Energy Efficiency）：电力消耗为 1/100 以下

![在这里插入图片描述](https://img-blog.csdnimg.cn/2019092422554558.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

这八个 KPI 主要是要满足三大场景的应用：

1. eMBB（Enhanced Mobile Broadband，增强型移动宽带）：指的是更快速的传输速率以及更好的使用者上网体验，即解决人与人之间通信，人们上网的问题。
2. mMTC（Ultra-reliable and Low Latency Communications，海量物联网通信）： 指的是更大量、更密集的机器通信（每平方公里 100 万个以上的装置进行联机），即解决物联网的问题。
3. uRLLC（Massive Machine Type Communications，低时延、高可靠通信）：指的是更低的延迟，像是无人驾驶、工业自动化和远端医疗手术等应用。

要实现这样的愿景，5G 网络需要面临的技术挑战主要是：高速率、端到端时延、高可靠性、大规模连接、用户体验和效率。
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924172236270.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

### 5G 网络架构的设计原则

为了应对这这样的技术挑战，5G 网络设计原则为：

- 从集中化向分布式发展
- 从专用系统向虚拟系统发展
- 从闭源向开源发展

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924172317914.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

如果用四个词来概括 5G 网络的设计原则，它们是：解耦、软件化、开源化和云化。

- 解耦：软硬件解耦，控制面/用户面分离。
- 软件化：NFV、SDN、编排和网络切片。
- 开源：软硬件开源，前传、API 接口开放。
- 云化：从 CAPEX 向 OPEX 模式转型，虚拟化& DevOps 环境，动态 & 自动化运维。

### 5G 网络的逻辑架构

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190925152340336.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924172357843.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

### 5G 核心网络的关键技术

由此，5G 核心网构架主要包含三大关键技术：SBA、CUPS 和网络切片，最终实现了化整为零、由硬变软的彻底演进。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924150736759.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

#### SBA 基于服务的架构

SBA（Service Based Architecture，基于服务的架构），借鉴了 IT  领域的微服务架构（Microservices）理念，基于云原生（Cloud Native）构架的设计思想。同时，糅合了  NFV、网络切片（Network Slicing）及 Softwarization（software +  -ization，软件虚拟化）的概念，将原本的网络功能（如 MME 中的 Mobility  management、Authentication）虚拟化为 NF（Network Function，网络功能），使 5G 核心网变为更加的  灵活、可扩展（Extensible、Flexible）。

**注**：云原生的使命是改变世界如何构建软件，其主要由微服务架构、DevOps 和以容器为代表的敏捷基础架构几部分组成，目标是实现交付的弹性、可重复性和可靠性。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924151112394.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

##### 微服务化

微服务就是指将单体式架构（Monolithic）拆分为多个粒度更小的微服务（Microservices），微服务之间通过 API  交互，且每个微服务独立于其他服务进行部署、升级、扩展，可在不影响客户使用的情况下频繁更新正在使用的应用。正是基于这样的设计理念，传统硬件网元设备先是虚拟化为 NF（网络功能），然后 NF 再被分解为多个 “网络功能服务”。
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924151155309.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)
 传统硬件网元设备是一种紧耦合的黑盒设计，NFV（网络功能虚拟化）虽然从黑盒设备中解耦出 NF 软件，但解耦后的软件依然是个 “大块头”  的单体式构架，需进一步分解为细粒度化的模块化服务组件。所以，从单体式架构到微服务架构的演变，会有一个明显的外在表现，就是网元大量增加了。微服务之间通过开放 API 接口来实现集成，以提升应用开发的整体敏捷性和弹性。

**微服务化后的 5G 网络架构**：
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924151728135.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

**5G 网络的 VNF（虚拟网络功能）清单**：

- **AMF（Core Access and Mobility Management Function，接入与移动性管理）**：类似 4G EPC 网元中的 MME、SGW-C、PGW-C 和 Mobility 相关的 Function。
- **SMF（Session Management Function，会话管理）**：类似 4G EPC 网元中的 MME、SGW-C、PGW-C 和 Session 相关的 Function。
- **UPF（User plane Function，用户平面功能）**：等同于 CUPS 后的 SGW-U 和 PGW-U，主要用于 Data 的传输。
- **UDM（Unified Data Management，统一数据管理）**：包含了 UDR（Unified Data Repository）和 FE（Front End）。UDR 的功能类似于 4G EPC 网元中的 HSS，用于储存用户和管理用户资料，而 FE 的功能则是一个存取 UDR 数据的前端。
- **PCF（Policy Control function，策略控制功能）**：类似 4G EPC 网元中的 PCRF（Policy and Charging Function），主要用于计费等。
- **AUSF（Authentication Server Function，认证服务器功能）**：用于处理认证的过程，类似 4G EPC 网元中 HSS 负责用户认证（Authentication）的部分。
- **NEF（Network Exposure Function，网络能力开放）**：类似 4G EPC 网元中的 SCEF（Service Capability Exposure Function），就是允许外部元件（or AF）存取部分 UE 信息、改变 UE 的行为等。
- **NSSF（Network Slice Selection Function，网络切片选择功能）**：主要的功能为决定一个连上来的 UE，应该使用哪些服务，进而决定由哪个 AMF 服务这个 UE，这边的辨别，依照的是 NSSAI（Network Slice Selection Assistance Information）。
- **NRF（NF Repository Function，网络注册功能）**：提供一个 NF 之间沟通的桥梁，例如某一个 NF 想要知道另一个（含有特定信息/功能的）NF 是否存在以及使用该 NF 或是取得该 NF 中的信息。
- **AF（Application Function）**：可以利用 SBA 中的 NF，例如用户资料、计费方式等等，设计服务/APP，用于提供客户/UE Service，类似于 SDN Controller 上的 APP。
- **®AN/(Radio) Access Network**：等同于 LTE 里的 eNodeB。
- **DN（Data network）**：比如运营商服务、互联网接入和三方服务。
- **UE（User Equipment）**
- **SDSF（Structured Data Storage network function）**
- **UDSF（Unstructured Data Storage network function）**

**注**：在 TS 23.335 中，有提到 UDC（User Data Convergence），主要是将  UDM、AUSF 和 PCF 这三个和用户资料、计费相关的元件整合为 UDC，用以确保数据的一致性和降低 Control Plane 中重复的  Signaling。

这些网元看上去很多，实际上，硬件都是在虚拟化平台里面虚拟出来的。这样一来，非常容易扩容、缩容，也非常容易升级、割接，相互之间不会造成太大影响。这个 5G 核心网基础构架正是基于云原生的微服务构架设计原则，以模块化、软件化的构建方式来构架 5G  核心网，以高效执行不同服务类型的网络切片。我们看到上图中网络节点名称后面都带有  Function（功能），这些功能是基于软件化的，以便动态灵活调整网络。

##### 基于服务的接口

SBI（Service Based Interface，基于服务的接口）所使用的 Protocol 如下图：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924225150819.png)

- HTTP/2 adopted as the application layer protocol for the service based interfaces
- TCP adopted as the transport layer protocol;
- Use of QUIC, binary encoding (e.g. CBOR) and other aspects are left FFS for possible support in future releases;
- JSON adopted as the serialization protocol;
- REST-style service design whenever possible and custom (RPCbased) methods otherwise.

回过头来看 3GPP 于 TS 23.501 中订定 5G SBA 构架：**SBA = 网络功能服务 + 基于服务的接口**。
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924223557381.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)
 其中 NF 可由多个模块化的 “网络功能服务” 组成，并通过 “基于服务的接口” 来展现其功能，因此 “网络功能服务” 可以被授权的 NF  灵活使用。其中，NRF（NF Repository Function，NF  贮存功能）支持网络功能服务注册登记、状态监测等，实现网络功能服务自动化管理、选择和可扩展。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924151236157.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)
 在 SBA 的构架中，任何 NF 可以分为 Producer 和 Consumer，而 NRF（Network Function  Repository Function，NF 注册功能） 则做为协调者的角色，如上述例子，当一个新的 NF（Producer）加入时，这个  NF（Producer）会向 NRF 进行注册，而当有ㄧ个 NF（Consumer）需要使用一个 NF（Producer）时，则它会向 NRF  询问是否有这个 NF（Producer）存在，而这个 NF（Producer）是否是它可以被允许（由 NRF 决定）使用的，假设这个 NF  存在，NRF 也授权它（Consumer）使用，则它才向那个 NF（Producer）提出使用此一 NF（Producer）的请求，并在此一  NF（Producer）授权之后进行使用。
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/2019092422490619.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

#### CUPS 控制与用户面分离

为了摆脱专用硬件，增加 Operator 在服务的扩增和传输设备扩建上的弹性，降低 CAPEX 以及 OPEX，在现有的核心网络中引进了  SDN 将控制面（Control Plane）和数据面（Data  Plane）进行分离的概念。事实上，核心网一直也都在沿着控制面和用户面分离的方向演进。到了 4.5G 和 5G  时代，这一分离的趋势更加彻底，也更加必要。其中一大原因就是，为了满足 5G 网络毫秒级时延的 KPI。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924151611536.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)
 这就是 CUPS（Control and User Plane Separation，控制与用户面分离），又称  “杯子式”（Cups）网络构架，目的是让网络用户面功能摆脱 “中心化”  的囚禁，使其既可灵活部署于核心网（中心数据中心），也可部署于接入网（边缘数据中心），最终实现可分布式部署。这就是所谓的核心网用户面下沉。同时，也保留了控制面功能的中心化。

2017 年 R14 阶段，3GPP 将再次向分离式的核心网构架演进之路出发。可以把它叫 “全分离式” 的网络构架。在 “全分离式”  构架下，SGW 和 PGW 被分离为控制面和用户面两部分（如下图黄色填充部分，SGW分 离为 SGW-C 和 SGW-U，PGW 分离为  PGW-C 和 PGW-U），同样，SGSN 也被分离为控制面（SGSN-C）和用户面（SGSN-U）。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924162806473.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)
 5G 时代，高清视频、VR/AR 等应用必然给网络带来超大数据流量，这不但给回传带来沉重负担，而且对核心网集中处理能力也是挑战，只能核心网的用户面下沉，从集中式向分布式演进。

另外，对于毫秒级的 5G 时延，核心网的用户面下沉与分布式架构也是一个必然的选择。光纤传播速度为  200km/ms，数据要在相距几百公里以上的终端和核心网之间来回传送，显然是无法满足 5G  毫秒级时延的。物理距离受限，这是硬伤。因此，需将内容下沉和分布式的部署于接入网侧（边缘数据中心），使之更接近用户，降低时延和网络回传负荷。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924163522144.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

低时延同时也会带来小区的蓬勃生长。并不只是因为 5G 高频段覆盖范围小才不得不考虑小区，其实时延也需要小区。小区越小，相对于宏站，意味着小区无线环境越简单、干净，这可以降低由于恶劣的无线环境带来的重传问题，在高可靠、低时延的 5G 应用中同样重要。

除了降低时延，这样的构架也附送了另一个好处，将更多的互联网内容揽入电信网络的怀抱中。低时延将使得电信网络掌握更多内容控制权，这种内容控制权依赖基于 MEC 在接入网侧的内容感知，比如对 GTP-U  数据流的解析，这加强了网络对业务内容的理解，真正实现智能管道。电信产业经历过辉煌，但如今跌入低谷，5G 将是电信重返辉煌的机会。

LTE 网络内部时延是小于 20ms，如果 Ping 外部服务器还不考虑重传，这个时延通常在 40-50ms 以上。光纤的传播速度是  200km/ms，5G 在应对时延超敏感用例时要求接入网时延不超过 0.5ms，这就意味着 5G 中心机房（数据中心）与 5G  小区（基站）之间的物理距离不能超过 50  公里。面对物理时延的挑战，我们不得不考虑在接入网引入移动边缘计算（MEC）、边缘数据中心，也就是将以前核心网和应用网的一些功能下沉到接入网。

![在这里插入图片描述](https://img-blog.csdnimg.cn/2019092416314975.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

尽管这种从中心化向分布式系统的演进和电信网络一直秉承的中心化概念是背道而驰的，但是别无选择。

#### 网络切片

5G 服务是多样化的，包括车联网、大规模物联网、工业自动化、远程医疗、VR/AR 等等。多种类型的业务和多样化的通信场景对 5G  网络提出了多样化的性能需求。这些服务对网络的要求是不一样的，比如工业自动化要求低时延、高可靠但对数据速率要求不高；高清视频无需超低时延但要求超高速率；而这些多样化的性能需求显然无法通过统一的网络架构来保证， 因此 5G 网络需具备虚拟化切片的能力 ，使得每个网络切片能够适配不同的业务和通信场景，以提供合理的网络控制和高效的资源利用。

网络切片技术与 MEC 技术并称 5G  网络的两大关键技术。网络切片是指将物理网络通过虚拟化技术分割为多个相互独立的虚拟网络，每个虚拟网络被称为一个网络切片，  每个网络切片中的网络功能可以在定制化的裁剪后，通过动态的网络功能编排形成一个完整的实例化的网络架构。  通过为不同的业务和通信场景创建不同的网络切片，使得网络可以根据不同的业务特征采用不同的网络架构和管理机制，包括合理的资源分配方式、控制管理机制和运营商策略，从而保证通信场景中的性能需求，提 高用户体验以及网络资源的高效利用，例如在超密集场景下引入本地化的控制管理机制和数据传输机制，降低网络中的信令开销和传输路径的跳数。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924152853783.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

其实说白了，就是人类上网需要很快的网速，车联网、VR/AR 需要很低的延时，智能抄表这样的物联网，需要更大的覆盖和更多的连接。5G 网络，统统都要满足。

可见，这么灵活的切片工作岂是传统大块头的黑盒设备能担当的。以一个死板的固定网络结构去应对，肯定是不行的。只有拆分成模块，灵活组队，才能搞定。显然，就要虚拟化、软件化，再将网络功能进一步细粒度模块化，才能实现灵活组装业务应用。因此，3GPP 就确认了由中国移动牵头 26 家公司提出的 SBA 构架为 5G 核心网基础构架。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924153046621.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

##### 控制面

控制面被分为 AMF 和 SMF。单一的 AMF 负责终端的移动性和接入管理；SMF 负责对话管理功能，可以配置多个。基于灵活的微服务构架的 AMF 和 SMF 对应不同的网络切片。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924152307487.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

AMF 和 SMF 是控制面的两个主要节点，配合它俩的还有 UDM、AUSF、PCF，以执行用户数据管理、鉴权、策略控制等。另外还有  NEF 和 NRF 这两个平台支持功能节点，用于帮助 Expose 和 Publish 网络数据，以及帮助其他节点发现网络服务。

##### 用户面

5G 核心网的用户面由 UPF（用户面功能）节点掌控大局，UPF 也代替了原来 4G 中执行路由和转发功能的 SGW 和 PGW。4G  核心网中的 MME、SGW 和 PGW 消失了。4G 中 MME 的功能被分解到 AMF（接入和移动管理功能）和  SMF（会话管理功能）中，SGW 和 PGW 被 UPF 替代。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924152540873.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

从 2G 时代的 MSC/HLR 到软交换，再到 4G 时代引入 MME 和 GW，总得来说，核心网一直沿着分离和软件化方向演进。5G  则更加彻底。传统 “黑盒” 硬件被解耦，网络功能软件进一步分解为微服务，以灵活构建网络功能，网络功能运行于通用 COTS  服务器或迁移至云，实现灵活的网络切片。总的来说，是一次化整为零、由硬变软的彻底演进。

不过，不管怎么演进，核心网的三大功能：服务管理、会话管理和移动管理始终存在。

### 5G 无线接入网的关键技术

首先，来看一个公式：

```
Channel capacity = Frequency * Bandwidth * Numbers of area
系统总容量/传输速率 = 频谱效率 * 宽带 * 小区数量
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924170346647.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

要提升 Capacity，不外乎上面三个参数的提升。

- 提升频谱：用更高频率的频谱，例如从 900MHz 提升到 28GHz，波长越短，传输速率也就越快。
- 提升宽带：例如 20MHz 就可以提供 4 倍于 5MHz 的速率，而更高频区段，能提供的宽带也就越高，在毫米波（mmWave）的区段，甚至能提供 100MHz 的宽带。
- 提升小区数量：这里指的小区数量。是将频宽这个参数所涵盖的范围，切割为多个小区块，分别传送，例如将 600Mhz~900Mhz  的区段，切成每 20MHz 为一个内存块，所以最多可以切成 30 个内存块，如果我一次使用的小区数量越多，则我能传送的速率也就越高。

#### 提升频谱

提升频谱的本质就是缩短波长。我们知道，波长越长，单位距离里面波的数量就越少，反之则越多。举个例子，波长为 10 公分和 5  公分，则一公尺内就会有 10 个和 20 个波。所以，可以利用更短的波，去达成更快的传输速率。假设一个波可以传送 1  个位的数据，那如果波长变成一半，那么在同样的时间内，传送的数据量就变成了 2  倍。但实际上，波长并非越短越好，波长越短穿透力也会越差，所以传送的距离也会越短。如此，基站的密度就必须提升，才能够实质上的提升单位面积的传输速率。

高频段的穿透能力差，覆盖范围小：
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924170732881.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

因为，增加小区数量和提升带宽这两个方式，都意味着更高的成本。所以，运营商更喜欢通过提升频谱效率的方式来提升容量。考虑到校验纠错、编码方式等办法都接近了香农极限，最有效的办法就是多天线技术了。高阶 MIMO（Multiple Input Multiple Output）和 Massive MIMO 这种复杂的天线系统成为了 5G 的首选。

- 4*4 MIMO
   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924191935712.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)
- 64T64R，又称 Massive MIMO，使用的天线数量更加庞大
   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924215053821.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

#### 提升宽带

越高的频谱所能使用的宽带也就越大、每个小区的宽带也越宽、传输速率也越快。例如，一个宽带 10Mhz 的小区，传输速率是一个宽带 5Mhz  小区的 2 倍。目前 4G 所使用的宽带为 5Mhz~20Mhz，每 5MHz 为一个增加单位，在 sub-6GHz（目前 4G  主要使用的频段区域）的高频区希望宽带能提升到 100Mhz 以上，而 IMT-2020 则希望 6GHz 以上的频段，其宽带可以至少在  800MHz 以上。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924170631149.png)

#### 提升小区数量

目前主流是通过 Carrier Aggregation（CA）来提升小区数量，即 将好几个小区块的频段做  Aggregation，达到数倍的速率。有点像是把好几根小水管绑在一起，变成一根大水管，目前 LTE-A（4G）的 5CA，是使用 5 个  20MHz 的小区做聚合。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924191641842.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

Carrier Aggregation 又可分为三种：

1. Inter-band CA：像是使用 800MHz 和 1.9GHz 各一个小区。
2. Intra-band non-contiguous CA：像是使用 1.9GHz 底下两个不连续的小区。
3. Intra-band contiguous CA：像是使用 1.9GHz 底下两个连续的小区。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924191832410.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

#### C-RAN 利用分布式概念降低延迟

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924215644746.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

一个基地台，可以分成三个部分：

- Antena（天线）：主要用于接收和发射信号（RF）。
- RRU（Remote Radio Unit）：主要用于将 RF 信号转换为 Digital（数位）信号。
- BBU（Base-band Unit）：主要用于处理和分解信号，如压缩、编码等等，BBU 有自己的操作系统，可以管控和其相连的 RRUs，主要做为核心网络和 RRU 或其他通信节点之间的沟通桥梁。

基地台构架的演进（到 4G 为止）可以分为三个阶段，如上图：

1. 传统基地台（Traditional base station）：传统基地台的 RRU 和 BBU 为一体的，和 RF 天线之间利用  Feeder cable（传统的电视或广播天线）连接，缺点是 Feeder cable  的频宽很低，而且当天线不够时，扩增困难/弹性低、成本（OPEX、CAPEX）高昂。
2. 分离式基地台（Distributed base station）：为了解决传统基地台的问题，我们将 RRU 和 BBU 进行分离，RRU 和 BBU 之间利用光纤线（Optical cable）连接，此举增加了布建的弹性，也加大了频宽，这样未来也更方便增加天线的部署。
3. 整合型基地台（Integrated’base station）：因为频宽的大幅增加，还有技术的进步，我们可以将 RF 天线和 RRU 结合，一个 RRU 上面可以支持大量的天线（Massive MIMO）。

注：RRU 跟 BBU 之间的沟通界面，是使用一个叫做 CPRI（Common Public Radio Interface）的协定，这中间可以通过很多不同类型的基础设施网络，这里不赘述。

其实上面第三个阶段，就是使用到了 C-RAN 的概念，C-RAN 是由中国移动于 2009 年提出得概念，C 的意思是  Centralize、Cloud 的意思，当原本绑在一起的功能进行拆分之后，对电信商而言，就增加了部属的弹性，有了 Cloud  的概念，我们可以将 BBU 集体布建于一个小型的 Data Center，形成一个 BBU Pool（或 BBU Hotel），而这个 Data Center 的多个 BBU，就能跟数量庞大的 RRU 进行对接，而因为 RRU 跟 BBU  是使用光纤进行连接的，所以可以大幅提升频宽和部属的弹性。

简而言之，C-RAN 构架就是将 RRU 拉远，BBU 资源集中化，并对其进行软件化、虚拟化和云化，电信中心机房向 IT 数据中心转型，以及引入 MEC（Multi-access Edge Computing，移动边缘计算）

4G 场景中，C-RAN + Massive MIMO  当前推荐的降低延迟方案之一，主要思想是让高频段扩大覆盖范围。在这样的网络构架下，控制面和用户面分离。工作于低频段且覆盖范围大的宏小区主要负责控制面，传送控制信令；而工作于高频段的小区只负责用户面，传送用户数据流量。这样的构架不但解决了高容量和全覆盖的问题，同时，减少了切换，减少了网络信令。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924171000502.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

再来，针对 5G 时代的云化、虚拟化概念，又将 BBU 再次切分为 DU（Distributed Unit）和 CU（Central  Unit）两个部分，由 CU 对底下的 DU 进行集中化的分层管理，下图是 3GPP TR 38.801  所提出可能的几种切割方式，详细的切割方式决议，可参考 3GPP TS  38.401:NG-RAN（https://portal.3gpp.org/desktopmodules/Specifications/SpecificationDetails.aspx?specificationId=3219）。

- BBU 切割为 DU+CU 的 8 种 Options
   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924220548669.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

CU 又可以导入 SDN，切分为 CP 和 UP，并利用 Open Source 让 RAN 端更为开放、有弹性，如下图所示：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924220631724.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

## MEC 边缘计算

要实现上文中提到过的 5G 的低延时需求，所以引入了边缘计算（Edge Computing）的概念，其思想类似于计算机中的 Memory 和 Cache  的概念，我们将用户常用到的数据，放在离用户比较近的边缘云（Edge-cloud）中，达到降低用户存取网络信息/服务的延迟，同时降低核心网络的流量/负担。

MEC（Mobile Edge Computing，移动边缘计算）概念最初于 2013 年出现。IBM 与 Nokia  Siemens（诺基亚，PS：联通 5G 买了那么多诺基亚的设备，大概就是因为 MEC  的发起者是诺基亚了吧。）网络当时共同推出了一款计算平台，可在无线基站内部运行应用程序，向移动用户提供业务。ETSI（European  Telecommunications Standards Institute，欧洲电信标准协会）于 2014  年成立移动边缘计算规范工作组（Mobile Edge Computing Industry Specification  Group），正式宣布推动移动边缘计算标准化。

其基本思想是把云计算平台从移动核心网络内部迁移到移动接入网边缘，实现计算及存储资源的弹性利用。这一概念将传统电信蜂窝网络与互联网业务进行了深度融合，旨在减少移动业务交付的端到端时延，发掘无线网络的内在能力，从而提升用户体验，给电信运营商的运作模式带来全新变革，并建立新型的产业链及网络生态圈。

MEC 改变了 4G 中网络和业务分离的状态，通过对传统无线网络增加 MEC 平台网元，将业务平台（包含内容、服务、应用）下沉到移动网络边缘，为移动用户提供计算和数据存储服务。

据估计，将应用服务器部署于无线网络边缘，可在无线接入网络与现有应用服务器之间的回程线路（Backhaul）上节省高达 35%  的带宽使用。到 2018 年，来自游戏、视频和基于数据流的网页内容将占据 84% 的 IP  流量，这要求移动网络提供更好的体验质量。利用边缘云架构，可使用户体验到的网络延迟降低 50%。据 Gartner 报告，全球联网的物联网设备至  2020 年将高达 208 亿台。在图像识别方面，服务器的处理时间增加 50-100ms，能提高 10%-20%  的识别准确率，这意味着在不对现有识别算法做改进的情况下，通过引入移动边缘计算技术，就可通过降低服务器同移动终端之间的传输时延改善识别效果。

2016 年，ETSI 把 MEC 的概念扩展为多接入边缘计算（Multi-Access Edge  Computing），将边缘计算从电信蜂窝网络进一步延伸至其他无线接入网络（如 WiFi）。MEC  可以看作是一个运行在移动网络边缘的、运行特定任务的云服务器。

下图是 ETSI 在 MEC 白皮书（White Paper）中列出的 MEC 相关应用，包含了远程手术（Remote surgery）、自动驾驶车（Autonomous car）、AR 等等要求低延时的应用。
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924221143436.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

针对不同延时需求的应用，将 Content/Service（内容/服务）放在距离用户/核网不同的位置，就如同 Memory Hierarchy 距离 CPU 的距离远近，如下图所示：
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924221538310.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)
 其实同样的概念早已经被使用了，像是 CDN（Content Delivery Network），所以 CDN 本质是一个边缘应用，属于边缘计算的子集。
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924221435266.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

其中，由于高清视频切片网络要求海量视频内容缓存（Cache）、分发和用户就近访问，所以核心网用户面功能下沉到了边缘云。同样，由于任务关键型物联网对时延要求高，比如车联网，为了降低物理距离带来的时延，核心网也下沉到了边缘云，并在边缘配置车联网应用服务器。如下图，将原本放在电信运营商核心网或数据中心中的 APPs 跟 Services 迁移到了边缘云中，而使用者或是开发者只要透过 API 就能存取/使用边缘云上的资源/服务。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924222418278.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)
 再把焦点缩小到ㄧ个 MEC Server 上，如以下这张中国联通的构架图所示，电信运营商将部份服务移到 MEC Server  上，而开发者（OTT 提供者，如 Youtube 或爱奇艺）及用户，可以透过一些共同的 API 来存取电信运营商于此 MEC 上提供的服务。
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924222656416.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)
 通过 API 呼叫 Service 的方式提下：
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190924222722135.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

MEC 还可以跟 C-RAN 等技术结合，还有将核网中的ㄧ些服务、IMS 等，拉到边缘云中，降低核网的负担、提升整个系统的 Capacity。
 在未来，MEC 将构成一个庞大的生态圈，包含了用户、电信商、内容分发、设备商以及服务开发商等等。

![在这里插入图片描述](https://img-blog.csdnimg.cn/2019092422283738.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

### MEC 应用场景举例

#### MEC 应用于 VR

基于 5G 的 MEC 解决方案，该方案适用于 VR 这一典型应用场景。MEC 部署在 RAN 或 C-RAN（Cloud  RAN）侧以获取利于统计分析的关键信息，提供低时延的本地化业务服务。运营商不仅可以有效减少核心网的网络负载，还能通过本地化的部署，提供实时性高、低时延的 VR 体验，增强 VR 实时互动。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190925164648528.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

#### MEC 应用于在线视频系统

下述为英特尔中国研究院与英特尔网络平台事业部、中国移动及爱奇艺合作开发的一款在线视频系统。该系统利用 MEC 进行视频加速，视频提供商利用 MEC  的计算、存储和网络功能，通过对用户视频请求数据分组进行分析，为特定的高清付费用户提供充足带宽，以保证其观看体验。OTT（互联网应用服务）  在使用上述系统时，无需对自己的应用网络进行架构性变动，由此可以大幅降低使用成本，加速业务创新。该系统目前已在业界知名的世界移动通信大会（Mobile World Congress，MWC）上现身，并引起广泛关注，并被 ETSI MEC ISG 采纳为典型业务场景之一。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190925164800360.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

#### MEC PoC12

中国联通在 2018 年 3 月首次参与 ETSI MEC 标准化工作。在 MEC#13 次会议中，中国联通主导的《PoC12：MEC  Platform to Enable OTT Business》国际标准项目成功立项，获得审核委员会全票通过。这是 ETSI  在边缘计算领域首个实现 ICT（IT&CT）融合的立项，填补了 MEC 应用研究方面的空白。自此，中国联通牵头开启了 ETSI MEC  标准化组织与 OTT（互联网应用服务）的应用合作，具有里程碑式的重要意义。该立项建议由中国联通联合中兴通讯、INTEL 共同向 ETSI  MEC#13 提交，并由中国联通网络研究院标准专家进行立项申请陈述和答辩。该标准项目将基于业界最大的天津边缘云测试床，依托轻量化  OpenStack、Kubernetes 等虚拟化技术，以商用化部署为目标，研究 vCDN、VR/AR 等 OTT 应用对 MEC  边缘云业务平台能力及 API 的需求，并为 ETSI GS MEC 003 系统架构的进一步完善提供强有力的参考依据。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190925175451937.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

PoC12 中所展示的 APP 部署在边缘主机上，经过 Mp1 同 MEP 对接，获取 MEP 上的平台能力，平台能力的好坏直接决定了  APP 是否部署在边缘主机并接受 MEP 管控。目前 MEP  平台的最大的问题就是平台封闭性严重，不同厂家平台制式不同很难互通，接口私有化定义。造成的后果就是一旦规模部署，每款 APP  都要分别部署在各方开发的 MEP 上，因此就都要针对各家平台进行定制化的开发和业务对接，这种不友好的方式是不会被第三方 APP  所接收，因为这种方式极大地增大了第三方的业务重复开发和维护工作。目前的解决方法是，由运营商主导 MEP  平台，同时由运营商统一开展平台接口标准化和平台架构标准化，集合设备商的各类平台能力和资源，这样第三方 APP  只需要一次开发和对接即可实现快速业务部署，对第三方 APP 非常友好，平台也更为开放。

### MEC 服务器部署场景

设计 MEC 解决方案时，还必须考虑 MEC 服务器在网络中的部署位置。MEC 服务器可以被部署在网络的多个位置，例如可以位于 LTE  宏基站（eNode B）侧、3G 无线网络控制器（radio network  controller，RNC）侧、多无线接入技术（multi-radio access  technology，multi-RAN）蜂窝汇聚点侧或者核心网边缘。本节旨在介绍 MEC  服务器的几个主要的部署场景，并且对不同部署方式的优势和存在问题加以简要分析。

#### 4G EPC 架构下的 MEC 部署

- **MEC 服务器部署在无线接入网（RAN）侧** ：MEC 部署在 RAN 侧的多个 eNode B  汇聚节点之后，这是目前比较常见的部署方式。MEC 服务器也可以部署在单个 eNode B  节点之后。这种方式适合学校、大型购物中心、体育场馆等热点区域下 MEC 的部署。将 MEC 服务器部署在 RAN  侧的优势在于可以更方便地通过监听、解析 S1 接口的信令来获取基站侧无线相关信息，但是该方案需要进一步解决计费和合法监听等安全性问题。
   ![在这里插入图片描述](https://img-blog.csdnimg.cn/2019092516534695.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)
- **MEC 服务器部署在核心网（CN）侧**：MEC 服务器部署在核心网边缘。在 PGW 之后（或与 PGW  集成在一起），从而解决 RAN  部署方案下的计费和安全问题。但部署在核心网侧会存在距离用户较远、时延较大和占用核心网资源的问题。该方案是不改变现有的 EPC 架构，将 MEC  服务器与 PGW 部署在一起。UE 发起的数据业务经过 eNode B、汇聚节点、SGW、PGW+MEC 服务器，然后到互联网。
   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190925165446875.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)
   下图所示方案需要改变现有的 EPC 架构，将原 PGW 拆分成 P1GW 和 P2GW（即 DGW），其中，P1GW 驻留在原位置，DGW  下移到 RAN 侧或者核心网边缘，DGW 负责计费、监听、鉴权等功能，MEC 服务器和 DGW 部署在一起。在此方案下，P1GW 和  DGW之间为私有接口，需由同一设备厂商提供。
   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190925165539373.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

#### MEC 在 5G 网络中的部署架构

而针对 MEC 的部署，不管是 ETSI 还是中国联通，都希望使用 x86  通用架构，利用网络虚拟化技术（NFV），增加未来扩充服务、动态配置资源的弹性，像是中国联通就建议使用 OpenStack 当作管理平台，以及利用 Container（如 Docker）取代 VM，其优势是为边缘运算提供更快更有弹性的反应速度、资源利用率等等。

在 5G 架构下，MEC 服务器也有两种部署方式。MEC 服务器可以部署在一个或多个 Node B  之后，使数据业务更靠近用户侧，如图中粗实线所示，UE 发起的数据业务经过 Node B、MEC 服务器  1，然后到达互联网。在该方式下计费和合法监听问题需进一步解决。MEC 服务器也可以部署在用户平面网关 GW-UP 后，如图中粗虚线所示，UE  发起的数据业务经过 Node B、GW-UP、MEC 服务器 2，最后到达互联网。此部署方法将以牺牲一部分时延为代价。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190925165015569.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

### MEC 系统设计原则

- **网络开放**：MEC 可提供平台开放能力，在服务平台上集成第三方应用或在云端部署第三方应用。
- **能力开放（APIs 经济）**：通过公开 API 的方式为运行在 MEC 平台主机上的第三方 MEC  应用提供包括无线网络信息、位置信息等多种服务。能力开放子系统从功能角度可以分为能力开放信息、API 和接口。API  支持的网络能力开放主要包括网络及用户信息开放、业务及资源控制功能开放。
- **资源开放**：资源开放系统主要包括 IT 基础资源的管理（如 CPU、GPU、计算能力、存储及网络等），能力开放控制以及路由策略控制。
- **管理开放**：平台管理系统通过对路由控制模块进行路由策略设置，可针对不同用户、设备或者第三方应用需求，实现对移动网络数据平面的控制。
- **本地转发**：MEC 可以对需要本地处理的数据流进行本地转发和路由。
- **移动性**：终端在基站之间移动，在小区之间移动，跨 MEC 平台的移动。
- **计费和安全**。

### MEC 框架设计

MEC 框架所涉及的实体如下图所示，这些实体可以分为外部相关层、MEC 主层和 MEC系统管理层。核心是 MEC 主层，它是包含 MEC 平台和虚拟化基础设施的实体，并且可以更具体的分为 MEC 虚拟基础设施层、MEC 平台层、MEC 应用层。
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190925171905544.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

- **MEC 虚拟化基础设施层** 基于通用服务器，采用计算、存储、网络功能虚拟化的方式为 MEC 平台层提供计算、存储和网络资源，并且规划应用程序、服务、DNS 服务器、3GPP 网络和本地网络之间的通信路径。
- **MEC 平台层** 是一个在虚拟化基础设施架构上运行 MEC 应用程序的必要功能的集合，包括虚拟化管理和  MEC 平台功能组件。虚拟化管理利用基础设施作为服务（IaaS）的思想，实现 MEC  虚拟化资源的组织和配置，应用层提供一个资源按需分配、多个应用独立运行且灵活高效的运行环境。MEC  平台功能组件主要是为应用程序提供各项服务，通过开放的 API  向应用层的具体应用开放，这些功能包括无线网络信息服务、位置服务、数据平面分流规则服务、访问的持久性存储服务以及配置 DNS 代理服务等。
- **MEC 应用层** 是基于虚拟化基础设施架构，将 MEC  平台功能组件组合封装后，以虚拟机方式运行的应用程序，如本地内容快速交付、物联网数据处理、任务迁移等。MEC  应用拥有确定数量的资源要求和执行规则，如所需的计算和存储资源、最大时延、必需的服务，这些资源要求和执行规则由 MEC  系统管理层统一管理和配置。MEC 应用可以通过标准的接口开放给第三方业务运营商，促进创新型业务的研发，实现更好的用户体验。

由上述的 MEC 框架可以看出，移动网络基于 MEC 可以为用户提供诸如内容缓存、超高带宽内容交付、本地业务分流、任务迁移等应用。需要注意的是，**任务迁移能够使得终端突破硬件限制，获得强大的计算和数据存取能力，在此基础上实现用户内容感知和资源的按需分配，极大的增强用户体验。任务迁移技术对移动设备的计算能力的强化和移动应用的计算模式的改变，必然会对未来移动应用和移动终端的设计产生深远的影响**。 MEC 的任务迁移流程，如下：
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190925172352897.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

### ETSI MEC 架构参考模型

ETSI（欧洲电信标准化组织）在 2014 年率先启动 MEC 标准化参考模型项目。这一项目组旨在移动网络边缘为 **（自己、合作伙伴或第三方）应用开发商与内容提供商** 搭建一个云化计算与 IT 环境的服务平台，并通过该平台开放无线侧网络信息，实现高带宽、低时延业务支撑与本地管理。MEC 标准化的内容主要包括以下内容：研究 MEC 需求、平台架构、编排管理、接口规范、应用场景研究等。

在 2017 年底，ETSI MEC 标准化组织已经完成了 Phase I 第一阶段基于传统 4G  网络架构部署，定义边缘计算系统应用场景、参考架构、边缘计算平台应用支撑 API、应用生命周期管理与运维框架、以及无线侧能力服务  API（RNIS/定位/带宽管理）。

- ETSI MEC 架构抽象模型
   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190925175853739.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)
   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190925161027917.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

宏观来讲，MEC 基本架构中不同的功能实体可分为三个层级：

- **移动边缘系统层（Mobile Edge System Level）**：负责对 MEC 系统进行全局掌控。
- **移动边缘主机层（Mobile Edge Host Level）**：包含了移动边缘主机（ME  host）和移动边缘主机层管理实体（ME host-level management  entity）；其中，移动边缘主机又可以进一步划分为移动边缘平台（ME platform）、移动边缘应用（ME  application）和虚拟化基础设施（IaaS）。
- **网络层（Networks Level）**：包含了 3GPP 蜂窝网络、本地网络和外部网络等相关的外部实体。该层主要表示了 MEC 工作系统与局域网、蜂窝移动网或者外部网络的接入情况。
- ETSI MEC 架构参考模型
   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190925143119397.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)
   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190925161930203.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)
- **ME 主机（移动边缘主机）** 由 ME 平台、ME 应用和虚拟化基础设施组成。虚拟化基础设施可以为 ME  应用提供计算、存储和网络资源，并且可以为 ME 应用提供持续的存储和时间相关的信息，它包含一个数据转发平面来为从 ME  平台接收到的数据执行转发规则，并在各种应用、服务和网络之间进行流量的路由。
- **ME 平台（移动边缘平台，MEP）** 从 ME 平台管理器、ME 应用或 ME  服务处接收流量转发规则，并且基于转发规则向转发平面下发指令。另外，ME  平台还支持本地域名系统（DNS）、代理服务器的配置，可以将数据流量重定向到对应的应用和服务。ME 平台还可以通过 Mp3 参考点与其他的 ME  平台进行通信，在分布式 MEC 系统的协作机制中，Mp3 参考点可以作为不同 ME 平台互联的基础。
- **ME 应用（移动边缘应用，ME APP）** 是运行在 ME 虚拟化基础设施上的虚拟机实例，这些应用通过 Mp1 参考点与 ME 平台相互通信。Mp1 参考点还可提供标识应用可用性、发生 ME 切换时为用户准备或重定位应用状态等额外功能。
- **ME 平台管理器（ME platform manager，移动边缘平台管理器，MEPM）** 具有 ME  平台元素管理、ME 应用生命周期管理以及 ME 应用规则和需求管理等功能。ME 平台和 MEPM 之间使用 Mm5  参考点，该参考点实现平台和流量过滤规则的配置，并且负责管理应用的重定位和支持应用的生命周期程序。Mm2 是操作支持系统（OSS）和 MEPM  之间的参考点，负责 ME 平台的配置和性能管理。Mm3 是 MEO 和 MEPM  之间的参考点，负责为应用的生命周期管理和应用相关的策略提供支持，同时为 ME 的可用服务提供时间相关的信息。
  - ME 应用生命周期管理包括 ME 应用程序的创建和终止，并且为 ME 编排器（ME orchestrator，MEO，移动边缘编排器）提供应用相关事件的指示消息。
  - ME 应用规则和需求管理包括认证、流量规则、DNS 配置和冲突协调等。
- **ME 编排器（ME orchestrator，MEO，移动边缘编排器）** 是 ME 提供的核心功能，MEO 宏观掌控 ME 网络的资源和容量，包括所有已经部署好的 ME  主机和服务、每个主机中的可用资源、已经被实例化的应用以及网络的拓扑等。在为用户选择接入的目标 ME 主机时，MEO  衡量用户需求和每个主机的可用资源，为其选择最为合适的 ME 主机，如果用户需要进行 ME 主机的切换，则由 MEO 来触发切换程序。MEO  与OSS 之间通过 Mm1 参考点来触发 ME 应用的实例化和终止。MEO 与虚拟化基础设施管理器（VIM）之间通过 Mm4  参考点来管理虚拟化资源和应用的虚拟机映像，同时维持可用资源的状态信息。
- 从 ME 系统的角度来看，**OSS（Operations Support System 操作支持系统）**  是支持系统运行的最高水平的管理实体。OSS 从面向用户服务（Customer-Facing  Service，CFS）门户和用户终端（UE）接收实例化或终止 ME 应用的请求，检查应用数据分组和请求的完整性和授权信息。经过 OSS  认证授权的请求数据分组会通过 Mm1 参考点被转发到 MEO 进行进一步处理。
- **面向用户服务门户（Customer-Facing Service Portal，CFS Portal）** 实体相当于第三方接入点，开发商使用该接口将自己开发的各种应用接入运营商的 ME 系统中，企业或者个人用户也可以通过该接口选择其感兴趣的应用，并指定其使用的时间和地点。CFS 通过 Mx1 参考点与 OSS 实现通信。
- **用户终端应用（User app，UEAPP）**
- **用户应用生命周期代理（user app LCM proxy，UEAPPLCM proxy）** 是供 ME  用户使用来请求应用相关的实例化和终止等服务的实体。该实体可以实现外部云和 ME  系统之间的应用重定位，负责对所有来自外部云的请求进行认证，然后分别通过 Mm8 和 Mm9 参考点发送给 OSS 和 MEO  做进一步处理。值得注意的是，LCM 只能通过移动网络接入，Mx2 参考点提供了 UE 与 LCM 相互通信的基础。
- **虚拟化基础设施管理器（VIM）** 用于管理 ME  应用的虚拟资源，管理任务包括虚拟计算、存储和网络资源的分配和释放，软件映像也可以存储在 VIM 上以供应用的快速实例化。同时，VIM  还负责收集虚拟资源的信息，并通过 Mm4 参考点和 Mm6 参考点分别上报给MEO 和 MEPM 等上层管理实体。

### MEC 与 UPF

MEC 在 ETSI 的定义里面包括了用户数据平面功能（UPF）以及边缘计算平台功能，而 3GPP 的 5G 架构里面主要是定义了 UPF 网元，UPF 作为核心网的用户面下沉网元，更多是网络功能。目前两大组织也在考虑 MEC 与 UPF 的融合，一般认为 5G 网络下 MEC 与 UPF 的关系如下图所示：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190925142441846.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

UPF 是 MEC 系统的一个组成网元，MEC 系统还包括 ME C平台、MEC 平台管理、MEC 服务、MEC 应用、边缘云基础设施以及 MEC 编排（其中 MEC 平台、MEC 服务和 MEC 应用均是面向 MEC 业务服务提供，我们统称为 MEC 业务系统)，UPF  负责将边缘网络的流量分发导流到 MEC 业务系统，逻辑上 UPF 与 MEC 业务系统是分离、松耦合的，实际建设时对于 MEC 与 UPF  是否合设集成部署与统一承载存在以下多种方案：

1. MEC 与 UPF 集成部署，基于 ICT 综合边缘云统一承载。
2. MEC 与 UPF 分离部署，基于不同的边缘云各自承载。
3. MEC 与 UPF 部分共享部署。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190925142416306.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

#### ETSI MEC & NFV 架构参考模型

Phase II 第二阶段的标准化于 2018 年 9 月底完成，主要聚焦在包括 5G/Wi-Fi/固网在内的多接入边缘计算系统，重点覆盖 MEC in NFV 参考架构、端到端边缘应用移动性、网络切片支撑、合法监听、基于容器的应用部署、V2X 支撑、Wi-Fi  与固网能力开放等研究项目，从而更好地支撑 MEC 商业化部署与固移融合需求，之前完成，同期将开启第三阶段的标准维护和标准新增阶段。

ETSI MEC017 协议于 2018 年 2 月发布，重点描述了 MEC 在 NFV 环境下的部署。MEC 作为与生俱来的带有 NFV 属性的一套生态，MEC017 协议可以认为是 MEC003 协议的进一步的扩展，更加面向实际部署和落地。整个架构遵循以下原则：已有的电信网  NFV 架构网元部分尽可能的重用，MEC 模块可调用 NFV 部分功能，MEC 内部功能模块之间的信令不受 NFVO 控制，MEC 同 NFV  之间的接口要重新定义。

- NFV 参考架构
   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190925151748314.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)
- MEC 在 NFV 中的参考架构
   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190925140444463.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9pcy1jbG91ZC5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

以 ME APP、MEP、MEPM-V、VNFM（MEPLCM）、DataPlane、CFSPortal、UEAPP、UEAPPLCM  proxy、OSS、MEAO 为组合，被 MEC 参考点（MEC reference points）所连接的网元，是 MEC  原有架构部分，这部分已经在 MEC003 中定义和说明过。这些功能模块是属于 MEC 特有的网元，是基于 NFV 基础上，根据 MEC  业务特性和业务需求所设定的全新的功能模块架构。由于 NFV 的网元大多是面向电信网的网元，而 MEC 则更加偏向第三方 APP  和业务，业务种类也比 NFV 更加多样，如：定位、分流、IoT、视频编解码等等。所以，基于 MEC 业务种类繁多的特性，有必要在 NFV  的基础上增加若干个功能不一的模块来协助 MEP 实现更多的功能。这里需要说明一点，MEC 需要虚拟化资源和管理，因此，MEC 重用了 NFVI 和 VIM 的部分，可直接调用而无需二次开发。MEC 模块同 NFV 网元之间的接口，也存在着重新开发和定义的问题。

以 NFVI、VIM、OSS 为组合，可视为 MEC 和 NFV 重用的网元部分。这些网元在进行电信网 NFV 开发和部署的时候就已经建设完成了，MEC 相关业务在运行时也需要他们的支持，因此直接重用即可。

我们知道 NFV（网络功能虚拟化）指的是解耦传统电信设备的软硬件，并将软件功能运行于 x86 通用服务器硬件上，以降低成本，缩短部署周期和激发服务创新。与 NFV 一样，MEC 也强调功能软件化和平台开放化，以提升网络敏捷性，灵活性，加快部署和创新。

在标准构架上，MEC 和 NFV 看起来不无二致，但它们是有区别的。区别主要在应用服务平台和相关服务上，MEC 根据 RAN 环境对  NFV  进行了优化，它将移动接入网与互联网业务深度融合，并将云计算和云存储下沉到边缘数据中心，加速内容分发和下载，且向第三方提供开放接口以驱动创新。有了 MEC，PGW-U/SGW-U 的用户面就下沉到了移动边缘节点，且由 NFV VIM（虚拟基础设施管理）、SDN 和  Orchestrator（编排器）控制管理。

#### 第三方 APP 的管理模式

APP 的管理对 MEC 来说是重要的部分，对 APP 的管理方式其背后代表了未来计算平台的运维模式和管理策略。ME APP 既受控于有  MEC 背景的 MEPM-V，也受控于有 NFV 架构背景的 VNFM（ME APP LCM），其本质在于 ME APP 是否与 MEP  有交互，是否使用了 ME service 或获取平台能力进行优化。

- **ME APP 受控于 MEPM-V 模式**。这种方式表明了 ME APP 部署在 NFVI 上，同时经由  Mp1 接口，连接到 MEP 平台，并可能使用 ME service，遵从 MEPM-V 的管理。由于 MEPM-V 中包含了 ME APP  规则和需求管理，因此这种方式就默认了 ME APP 要受到 MEP 平台的管理。通常 MEP  可以是运营商自建也可以是设备商的集成设备。总之，这种管理方式就意味着第三方 APP 部署在 MEP  上时必须受到平台的管理，这种管理方式的好处显而易见，有利用边缘生态中 APP 的管理和调度，但是未来可能存在一个问题，如果 ME APP  只是想用这些 NFVI 的资源，而对 MEP 上的 ME service 不感兴趣，那么这种管理就使得第三方 APP 难以接受，因为目前 Mp1 接口定义的还不够充分，第三方也需要围绕MEP进行定制化开发，这些都加重了第三方的工作量，需要考虑第三方的需求和想法。但是作为 MEC  构建生态的想法，我们更倾向于提供第三方 APP 足够的 PaaS 能力。
- **ME APP 受控于 VNFM（ME APP LCM）模式**。这种管理方式，即 ME APP 仅受到  NFV 网元的管理，也就是只是对 ME APP 的生存周期进行管理。这种方式表明第三方的 APP 仅仅是租用了边缘数据中心的  NFVI，进行部署，但是不使用任何 MEP 中的 service 和平台能力，因此 ME APP  仅仅从资源层面受到管理。这种商业模式其实就是租赁机房资源、租赁机架、租赁硬件资源、租赁虚拟机的商业模式，从实现来讲受益更加直接，第三方直接获取资源自行开发相应服务，运营商也无需在 MEC 平台层面做过多的开发。但是这种方式并不是在营造 MEC 生态，因为这一管理方式彻底抛弃了 APP 同 MEP 之间的关联， Mp1  接口完全废弃，那么 MEP 也没有了存在的价值，因此这种方式只可在早期不成熟的时候采用，长期发展对 MEC 生态和建设非常不利。
- **ME APP 同时受控于 MEPM-V 和 VNFM（MEAPP LCM）模式**。这种方式结合了 MEC 中 APP 管理和 NFV 中的 APP 管理。NFV 仅对 APP 的生存周期和虚拟化资源进行管理，而 MEC 则对 ME APP  规则和需求进行管理，分工明确职责不同。同时定义好 Mp1 接口，提供ME APP 使用 MEP 中 ME service  的途径，借助边缘云平台能力可以进行 APP 的定制优化。这种方式一方面迎合了 APP 和 MEC  平台搭建方的各方需求，同时也是未来比较合适的管理方式。

​    转载请注明作者：JmilkFan 范桂飓
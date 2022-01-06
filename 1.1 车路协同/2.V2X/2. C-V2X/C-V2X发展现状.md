随着5G的落地进程加快，5G车联网大规模应用落地的帷幕已经拉开。3月24日，工业和信息化部发布《[关于推动5G加快发展的通知](https://www.zhihu.com/search?q=关于推动5G加快发展的通知&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"answer"%2C"sourceId"%3A1341859590})》，提出促进“5G+车联网”协同发展，推动车联网无线通信技术标准的研制及研发验证。

今年5月，[工信部](https://www.zhihu.com/search?q=工信部&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"answer"%2C"sourceId"%3A1341859590})发布《2020年工业通信业标准化工作要点》，明确指出以专项方式推进车联网（智能网联汽车）等重点领域标准制定，成体系地推进行业标准制定工作，促进产业基础能力和产业链现代化水平提升。

5G带来的诸如更高带宽、更大数量连接、更高移动速度都将是对V2X全面升级的重大利好。在政策的支持之下，车联网C-V2X在我国智能网联领域崭露头角的时刻也可指日而待。

要了解C-V2X，首先需要知道，V2X从哪来，这又是个什么？

## 01 V2X从哪来？

V2X相关概念早有人提出，但一直未被重视。真正被提出落地，还是因为美国新泽西州和[弗罗里达州](https://www.zhihu.com/search?q=弗罗里达州&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"answer"%2C"sourceId"%3A1341859590})的两起校车车祸。

两起车祸均因校车路过十字路口时与卡车相撞，导致车上的学生们全部死亡。这样惨痛的意外不得不引起交通系统和汽车行业的反思。

试想一下，如果事故发生时车辆上有能与其他汽车进行通信的系统，那么车辆就相当于拥有了除驾驶员之外的第二双眼睛。

即使驾驶员受外力或个人因素影响无法判定车辆的安全状态，车辆自带的联网系统仍可替代驾驶员做出正确判断，类似事故就能被避免发生。

美国[国家运输安全委员会](https://www.zhihu.com/search?q=国家运输安全委员会&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"answer"%2C"sourceId"%3A1341859590})（NTSB）对事故进行调查后提交了一份报告给美国公路交通安全管理局（下称NHTSA）。

报告建议NHTSA开始进行V2V的授权工作，为所有在高速公路行驶的车辆发布一个能安装此项技术的最低性能要求。

NTSB希望在标准公布后，汽车制造商们能够在所有新车上安装此系统。2006年，由通用汽车在一辆凯迪拉克上展示了V2V的应用。

此后，其他汽车制造商和汽车配套产品供应商纷纷开始研究这项技术。

## 02 V2X是啥？

V2X也就是Vihicle to everything，即车与任何事物的联系、车联一切。

主要包括：**V2V车与车(Vehicle)：**通过车载终端进行车辆间信息交互，车辆通过车载终端向外发送本车的速度、位置、车辆行驶状态等自身信息，同时接收其他车辆发送的相关信息。这样双向信息结合，就可以判断车辆所处环境是否存在交通危险，从而及时避免事故发生。

**V2I车与基础设施(Vechile to infrainstructure)：**通过车载终端与路侧单元(如红绿灯、交通指示牌、路侧终端等)进行信息交互，路侧基础设施可以接收附近车辆发出的信息，同时也可以向覆盖范围内的车辆发布诸如路面信息、交通意外信息、拥堵信息等实时信息。

**V2P车与人(Vehicle to people)：**通过车载终端与弱势交通群体(行人，骑车者)携带移动终端设备(如手机等)进行通信，即使驾驶员没发现前方有人，车辆仍可以通过这个人身上的通讯设备感知到对方存在，从而实现减少交通意外的发生。

**V2N车与云（Vehicle to network）：**车载终端通过接入网/核心网与云管理平台进行信息交互， 也就是车辆通过传感器，网络通讯技术与其它周边车、人、物进行通讯交流，并根据收集的信息进行分析、决策的一项技术。

车上有音响、摄像头、发动机、轮胎、[超声波雷达](https://www.zhihu.com/search?q=超声波雷达&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"answer"%2C"sourceId"%3A1341859590})等各类部件，通过传感器可以将整个车辆数字化，转变成数据来帮助车企为客户提供更好的服务。但是信息需要与外界交流，不然有再多传感器也是个自闭小车。

如OBD一类的车载工具，数据量、及时性已经略显落后，所以发展V2X和通信技术有着巨大意义。V2X在技术层面主要包括DSRC专用短距离通信技术，与C-V2X以蜂窝通信为基础的技术两种，我国就以后者为主。

C-V2X(蜂窝车联网)是基于 3GPP 的全球统一标准的车联网无线通信技术，包括 LTE-V2X和 5G-V2X及其后续演进。

## 03 3GPP是谁？

3GPP（3rd Generation Partnership Project）官方译为第三代合作伙伴计划，成立于1998年12月，最初的工作范围是为第三代移动通信系统制定全球适用的技术规范和技术报告（在欧洲GSM基础上搞出WCDMA对刚北美CDMA）。

第三代移动通信系统基于的是发展的GSM核心网络和它们所支持的无线接入技术，主要是UMTS。

随后3GPP的工作范围得到了改进，增加了对UTRA长期演进系统（LTE）的研究和标准制定。近日，国际电信联盟（ITU）无线通信部门（ITU-R）[国际移动通信工作组](https://www.zhihu.com/search?q=国际移动通信工作组&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"answer"%2C"sourceId"%3A1341859590})（WP 5D)第35次会议成功闭幕，会议确定3GPP系标准成为唯一被ITU认可的5G标准。

## 04 3GPP C-V2X 接入层标准化进程

3GPP 关于 C-V2X 的标准化工作分为四个阶段：

![img](https://pic2.zhimg.com/80/v2-12609eba827dec0f365779d25d3afede_720w.jpg?source=1940ef5c)

第一个阶段是支持 [LTE-V2X](https://www.zhihu.com/search?q=LTE-V2X&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"answer"%2C"sourceId"%3A1341859590}) **的 Release-14 标准**，该标准已于 2017 年 3 月正式发布，这也是全球 C-V2X 商用落地的主要版本；包括 Uu（基站与终端间的通信）接口以  及PC5（直接通信）接口2种通信方式，车对车（V2V）、车对基础设施（V2I）、车对人（V2P）和车对网络（V2N）4类业务模式和TR  22.885中的业务场景。同时，在业务需求方面，标准也针对LTE-V2X支持的最大移动速度、时延、消息发送频率、数据包大小等参数进行了定义。

**第二阶段是支持LTE-eV2X的Release-15标准**，已于2018年6月正式发布；是在R15中完成 对LTE-V2X技术增强，进一步提升  V2X的时延、数据效率率以及可靠性等性能，以进一步满足更高级的如编队行驶、半/全自动驾驶、感知信息交互以及远程驾驶等C-V2X增强应用场景需求。其

相关技术主要针对 PC5 的增强，可以与 LTE-V2X 用户共存且不互相影响。

**第三阶段是支持 5G-V2X 的Release-16 标准**，相关研究工作已于 2018 年 6 月启动，由于疫情影响，该版本冻结时间多次延后， 2020 年 7月3日宣布正式冻结。**这是基于5G NR新空口的第一版V2X标准。**

![img](https://pic3.zhimg.com/80/v2-36f03d2d3b97c2bd849ea1051832a7af_720w.jpg?source=1940ef5c)

在Release-16中，功能更新包括大致有以下14点——超可靠低延迟通信（URLLC）的增强增强V2X支持增强网络切片NR-U， 即5G免许可频谱设计5GS增强了对垂直行业和LAN服务的支持增强[毫米波](https://www.zhihu.com/search?q=毫米波&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"answer"%2C"sourceId"%3A1341859590})和中频段的载波聚合蜂窝物联网的支持与扩展5G定位和定位服务UE无线功能信令优化5G卫星接入5G网络自动化架构的支持无线和有线融合增强用户身份验证，多设备支持增强无线NR功能

上述功能之中，较前版本而言重要的更新包括：第一，持续增强6GHz以下和毫米波的通信。第二，更新更多与手机节能方面相关的功能和标准设计。第三，首次引入5G免许可频谱设计。第四是移动性增强，目的在于从小区到小区之间切换的时候，5G能够做到没有间断的零秒切换。第五是增强毫米波和中频段的载波聚合。

![img](https://pica.zhimg.com/80/v2-60fa9e6f0a467cce1878cc39f9706c38_720w.jpg?source=1940ef5c)

其中，与汽车行业最直接相关的莫过于对车联网（V2X）的重要增强。**面向车联网应用，该标准支持了V2V和V2I直连通信，通过引入组播和广播等多种通信方式，以及优化感知、调度、重传以及车车间链接质量控制等技术，实现V2X支持车辆编队、半自动驾驶、外延传感器、远程驾驶等更丰富的车联网应用场景。**

根据“5G通信”的统计，Rel-16对车联网部分花费了很大的篇幅，涉及到的标准如下：

[1] 3GPPTS 23.287：“ 5G系统（5GS）的体系结构增强，以支持车辆到一切（V2X）服务”。

[2] 3GPPTS 22.185：“ V2X服务的服务要求；”。

[3] 3GPPTS 22.186：“增强对V2X场景的3GPP支持；”。

[4] 3GPPTS 23.285：“ V2X服务的体系结构增强”。

[5] 3GPPTS 23.501：“ 5G系统的系统架构；”。

[6] 3GPPTS 23.503：“ 5G系统的策略和计费控制框架；”。

[7] 3GPPTS 33.536：“ 3GPP支持高级车辆到一切（V2X）服务的安全方面”。

[8] 3GPPTS 24.587：“ 5G系统（5GS）中的车辆到一切（V2X）服务；第3阶段”。

[9] 3GPPTS 24.588：“ 5G系统（5GS）中的车辆到一切（V2X）服务；用户设备（UE)策略；第3阶段”。

[10]3GPP CP-192078：“ WID：用于高级V2X服务的3GPP支持的体系结构增强的CT方面”。

第四阶段是支持增强 5G-V2X 的Release-17 标准，相关准备工作已于 2019 年底开展，目前该阶段的工作仍在讨论中，由于疫情影响，预计相关标准将于  2021 年 12  月底发布。R17标准将对R16标准进行增强演进。比如“天地一体化”通信，包括运用卫星、无人机等手段提供5G连接，都有可能会在5G  R17标准中出现。

## 05 C-V2X标准的重要优势

从技术角度看：

1、C-V2X依托现有的LTE基站，这些网络已经提供了出色的安全性和良好的覆盖范围，避免了重复建设，而且工作距离远比DSRC大。

2、支持不同网络参与者之间的可靠、实时、低延迟通信。5G之所以是对C-V2X通信速度、质量的一次升级，因为LTE-V2X一大弊端就是平均延时大于50ms。乍一听不算什么，但实际行驶中如果遇到危险，这个延时可导致致命伤害的发生。

3、C-V2X支持车辆和其他连接的设备之间的短距离和远程传输。详情查看下表：

![img](https://pic2.zhimg.com/80/v2-6ba12f6c1f67b96e7ab931fcf289d214_720w.jpg?source=1940ef5c)



![img](https://pic3.zhimg.com/80/v2-bce80602271d90fabd73b00a3daecf31_720w.jpg?source=1940ef5c) 



（图表来源：网优雇佣军)**从驾驶员角度看**，普通用户端

也将获得更多便利：比如：远程车辆诊断和预测性维护、车载电子购物平台、更加便利的UBI保险、智能停车、车内零部件风险提醒等等。

当然自动驾驶也将更好、更全面的为驾驶员提供辅助服务。

## 06 C-V2X 产业链构成

C-V2X 的产业架构由三个部分组成：C-V2X 产业链、产业支撑及产业推进构成。

C-V2X  产业链主要包括通信芯片、通信模组、终端设备、整车、智能道路、测试验证以及运营与服务环节，其中的参与方包括芯片厂商、设备厂商、主机厂、方案商、电信运营商、交通运营部门和交通管理部门等。

C-V2X 产业支撑包括科研院所、标准组织、投资机构及关联的技术产业。

C-V2X 产业推进包括链接建立、能力增强和应用升级。

![img](https://pic2.zhimg.com/80/v2-125c67088e22b54fdc17b699756dc782_720w.jpg?source=1940ef5c)

## 07 最后

**根据全球领先的汽车零部件供应商博世的数据，到2025年，联网汽车可以挽救11,000人的生命并减少260,000起事故，避免40万吨二氧化碳排放，创造2530亿美元的应用收入，并且每年节省2.8亿小时的驾驶时间。可以见得，车联网在汽车领域的落地前景十分可观，而有了5G的助力，车内外的场景也将变得更加多元化。汽车不再是简单的交通代步工具，未来形态将是人、车、路、网的全新融合。但目前，C-V2X商业化进程才刚刚处于起步阶段，还存在着诸多待解决的问题：**

1、用户隐私保护：**在C-V2X中，每辆车都主动分享自己的位置信息和驾驶意图，这使得驾驶员和汽车的数据被更大范围的暴露在外界之中，极易被跟踪。如何保护用户的隐私数据安全，已经在国内业界的讨论还在进行阶段。**

2、产品没有达到商业化程度**虽然相关的关键产品如芯片、车载终端、道路智能化终端等方便国内已经在大力发展，但整体形势离商业部署仍有差距。由此带来的如何提升道路智能化覆盖率也是关键问题。**

3、商业模式不清晰**V2X产业链条较长，包括从芯片、模组、终端、平台、测试验证、网络安全、到系统集成的各个方面，目前竞争格局未定，没有主导企业，整个产业没有核心凝聚力，导致产业推动力量发散。**

**总体来看，C-V2X真正实现商业化落地仍需要时间及包括政府、企业在内的多方努力配合。**

参考资料：

1. 《C-V2X 产业化路径及时间表研究》，中国智能网联汽车产业创新联盟（CAICV）、 IMT-2020（5G）推进组 C-V2X 工作组、[中国智能交通产业联盟](https://www.zhihu.com/search?q=中国智能交通产业联盟&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"answer"%2C"sourceId"%3A1341859590})（C-ITS）、中国智慧交通管理产业联盟（CTMA）四家单位联编制；
2.  《车联网 V2X，5G 下游应用黄金赛道》，[华安证券](https://www.zhihu.com/search?q=华安证券&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"answer"%2C"sourceId"%3A1341859590})；
3.  《C-V2X 车联网产业发展综述与展望》，首发于[电信科学](https://www.zhihu.com/search?q=电信科学&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"answer"%2C"sourceId"%3A1341859590})，作者金博、胡延明；
4.  《C-V2X行业深度报告》，[光大证券](https://www.zhihu.com/search?q=光大证券&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"answer"%2C"sourceId"%3A1341859590})；
5.  《C-V2X 技术在智能网联行业中应用探讨》，首发于中兴通讯技术第26卷第1期，作者宋蒙、[刘琪](https://www.zhihu.com/search?q=刘琪&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"answer"%2C"sourceId"%3A1341859590})、许幸荣。
6.  《深度刨析5G Rel-15、16、17技术路线及演进，高通5G创新方向指向何方？》，首发于公众号EETOP，作者Nancy Zhou。
7.  《一张表看懂5G NR与4G LTE的区别》，首发于网优雇佣军。
8.  《R16标准冻结，5G从能用变好用》，首发于[科技日报](https://www.zhihu.com/search?q=科技日报&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"answer"%2C"sourceId"%3A1341859590})。
9.  《5G标准R16版冻结！5G正式步入第二阶段》，5G通信。
10. 3GPP是干什么的？详解3GPP组织的历史，通信行业必读！》，燚[智能物联网](https://www.zhihu.com/search?q=智能物联网&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"answer"%2C"sourceId"%3A1341859590})知识。
- [智能网联汽车（V2X）测试的实践与思考](https://mp.weixin.qq.com/s?__biz=Mzg5MjEzNzg0OQ==&mid=2247507882&idx=2&sn=3c248bcaa40779d2cf965dca77d2cab1&chksm=cfc027bcf8b7aeaa02c368d43631ab58a37a49098b0ba904773ebea8182eb2b5668349c09814&scene=21#wechat_redirect)

近年来，随着智能网联汽车技术的发展，智能网联汽车测试评价技术也经历了不同的发展阶段，总体概括如下：单一功能测试→综合验证评价体系，场地测试→多支柱法测试手段，单车智能测试→智能网联融合测试。现阶段的自动驾驶技术大部分还聚焦于单车智能的技术方案，相关测试方法也处于单车智能测试阶段，面向智能化与网联化融合的技术尚处于探索期，与之对应的测试方法也需要深入探索和持续演进。

**本文将从互联互通测试评价、V2X模拟仿真测试评价、示范区C-V2X覆盖性能测试、车路协同发展与智慧道路分级评测等角度分享国家智能网联汽车创新中心在智能网联汽车（V2X）测试领域的实践与思考。**

![image-20220117233305664](https://gitee.com/er-huomeng/img/raw/master/img/image-20220117233305664.png)

图1 智能网联汽车测试评价技术发展阶段示意图

## **互联互通测试评价：协议一致性测试是基础**

伴随“三跨”、“四跨”、“新四跨”等C-V2X应用示范活动举行，协议一致性测试与认证受到终端企业、主机厂及运营商的广泛重视，也极大地促进了不同终端厂商设备间的互操作性。然而由于对标准理解的差异、软件版本或协议栈的更新迭代、加密方案的更新、物理层和应用层的不规范等，导致RSU与OBU之间的广泛互联互通仍旧未能实现，大规模的互操作依旧阻碍重重。因此，除了继续推广协议一致性测试，业内也亟需形成完整可信赖的互联互通测试评价体系及认证体系，尽早实现设备间广泛的互联互通及互操作性，为C-V2X落地应用打下坚实基础。

## **V2X模拟仿真测试评价：C-V2X场景库建设是关键**

关于C-V2X应用的仿真测试，典型的测试系统包括仿真软件、V2X信号模拟器、GNSS模拟器和V2X协议解码器等。现有仿真软件可以搭建基于V2X预警功能的3D仿真场景，生成实时周围车辆状态、车辆定位信息以及路边单元状态等数据，仿真软件可以对以上数据进行解析并打包成V2X数据报文，通过V2X模拟器发出PC5射频信号，矢量信号源用来生成各种制式卫星信号，并将模拟的定位信息转换成卫星信号通过空口发送至被测设备，同时为V2X通信提供时钟同步，V2X协议解码器将被测设备接收到的V2X消息报文进行解码，来判断被测设备是否正确收发V2X消息报文并实现预警。

针对未来智能化与网联化融合的智能网联汽车仿真测试，应将无线信道场景与传统仿真场景融合，从而使得仿真测试更加准确模拟真实环境，因此C-V2X仿真场景库的建设将是未来仿真测试的关键因素。

![image-20220117233323249](https://gitee.com/er-huomeng/img/raw/master/img/image-20220117233323249.png)

图2 C-V2X仿真场景创建示意图

## **示范区C-V2X覆盖性能测试：V2X信号覆盖性能待提升**

车联网C-V2X的应用需要低时延、高可靠数据传输，良好的无线信号覆盖是低时延和高可靠特性的基础保障。频谱资源是国家的战略性资源，2018年，工业和信息化部印发《车联网（智能网联汽车）直连通信使用5905-5925MHz频段管理规定（暂行）》的通知，为车联网的频率使用提供了政策保障，相关频谱资源的合理使用需要持续监测检测。

创新中心协同行业机构，对不同示范区的无线信号覆盖能力进行了测试，发现不少示范区仍存在信号覆盖、信号干扰、不满足协议要求等诸多问题，相关测试结果为示范区运营的优化提供了参考，也对示范区的建设和RSU的部署发挥指导意义。

![image-20220117233332145](https://gitee.com/er-huomeng/img/raw/master/img/image-20220117233332145.png)

图3 路端C-V2X信号覆盖情况示例

## **车路协同发展与智慧道路分级评测：路侧感知性能待验证**

车路协同是我国智能网联汽车发展的重要路径，车路协同的发展离不开基础设施的数字化升级。首先，全国的车联网先导区和示范区基本都进行了道路的升级改造，然而由于建设标准和实施规范的缺失，不同的先导区或示范区基础设施数字化和智能化方案不尽相同，示范区的测试结果互认尚在推进中。其次，推荐性国家标准GB/T 40429-2021《汽车驾驶自动化分级》已经发布，车侧的分级标准已经具备，路侧的分级也势在必行。

因此，在积极开展车路协同技术的大规模测试示范同时，应对路侧设施的智能化和网联化水平进行客观的测试评价，最终实现对道路的智慧化程度进行分级。不同等级智能驾驶汽车需要不同能力等级的道路支撑，以加速商业化。在智能公路的智能化等级进行划分的基础上，不同公路宜采用不同的智能化等级为目标进行规划与建设。

![image-20220117233343979](https://gitee.com/er-huomeng/img/raw/master/img/image-20220117233343979.png)

图4 V2X路侧设备感知测评系统

随着自动驾驶汽车向智能化、网联化发展，国家智能网联汽车创新中心持续聚焦V2X技术赋能高级别自动驾驶的发展趋势，着力研究智能网联汽车V2X测试方法及体系，开展关键技术创新、标准体系完善等工作，目前已经形成在V2X射频性能测试、V2X协议测试、信息安全测试、整车无线通信测试、V2X HIL仿真测试、V2X  VIL测试、V2X预警功能测试、智慧道路分级评价测试等方面的能力。同时，创新中心期待与优秀的行业伙伴携手共进、跨界融合，加快建设形成智能网联汽车测试评价体系，助力智能网联汽车产业的发展与落地。
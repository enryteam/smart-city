# Web3D智慧环卫GIS系统

原文地址：https://blog.51cto.com/u_15153979/3174476



智慧环卫，依托物联网技术与移动互联网技术，对环卫管理所涉及到的人、车、物、事进行全过程实时管理，合理设计规划环卫管理模式，提升环卫作业质量，降低环卫运营成本，用数字评估和推动垃圾分类管理实效。智慧环卫所有服务部署在智慧城市管理云端，对接智慧城市网络，以云服务方式随时为管理者及作业人员提供所需的服务。

智慧环卫系统作为智慧城市的一部分，是社会发展的需要：城乡环卫一体化，破解垃圾围城生活垃圾源头减量化，促进垃圾分类有效管理餐厨垃圾流向，杜绝地沟油严控渣土运输，杜绝建筑垃圾乱排乱放；同时也是环卫管理有力帮手：人工作业全面转向机械化作业的需要，是人多、车多、事多、设施多、运营成本高、作业效率低、保洁清运不及时等问题的可视化解决方案。

# 界面简介及效果预览

这一套可视化解决方案在设计上尝试了一种极简的风格样式，布局上采用了 HT 惯用的 图纸 + 渲染元素 的方式。

![watermark,size_14,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=](https://s4.51cto.com/images/blog/202107/23/aaa95241a73aa7e72a98951db5e49ba4.jpg?x-oss-process=image/watermark,size_14,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)

# 行业痛点及可视化应对策略

城市环卫有诸多痛点，例如：垃圾车随意到处倾倒，垃圾产量无法准确统计；突发事件无法及时处理 ；员工工作质量无法考核  ；公共设施的配置覆盖范围无法监测；载重数据无法最大化利用 ；设备设施故障 ；无法精细化管理响应垃圾分类政策  ；无法根据垃圾运量来合理配置车辆载重和中转站位置 ；渣土车漏撒问题、违规倾倒问题；无法监测控制超载 、渣土车行径路线进入违规区域等。

HT for Web 给出一套针对这些业务痛点的可视化解决方案，整个方案中应用到了 HT 的 2D 引擎、3D 引擎、GIS 引擎。

HT 可以快速实现丰富的 2D、3D、GIS  效果，可以根据需求发挥自己的想象，玩转很多新奇的功能，并且通过优势互补的作用下，完善出一套完整的可视化系统解决方案。所以在可视化系统的实现上，3D 场景采用以 HT 轻量化 HTML5 / WebGL 建模的方案，实现快速建模、运行时轻量化到甚至手机终端浏览器即可 3D  可视化运维的良好效果； GIS 引擎，能够与 3D 场景准确同步，既保留了 GIS 引擎的效果和功能，同时又不去限制设计师在 3D  场景中的发挥；而在对应的 2D 图纸上可以在各种比例下不失真，加上布局机制，解决了不同屏幕比例下的展示问题。

# 环卫车

针对“无法根据垃圾运量来合理配置车辆载重和中转站位置”，本系统提供环卫车监控功能，其中环卫车分为常见的 4 种类型，本系统将渣土车也算在其中，旨在演示监控效果。

渣土车、收运车、清扫车、抑尘车，在一个城市环卫系统中，这几种车的配置数量和出勤次数既决定了环卫工程的实施成本，同时也影响着城市清运的质量。它们的数量、分布、轨迹都是应该纳入监控和分析中来的。

本系统提供各种车辆的 定位查看 功能，远景可查看总的分布情况，近景可以查看具体车辆的相关数据。轨迹总览 功能可以直观地反映环卫车在某一时间段中的行驶轨迹，可以监控是否出现在违规区域，也可以用于分析行进路线的设计是否合理。

![watermark,size_14,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=](https://s4.51cto.com/images/blog/202107/23/2c74eba04f55d25771de9b8333034139.jpg?x-oss-process=image/watermark,size_14,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)![watermark,size_14,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=](https://s4.51cto.com/images/blog/202107/23/da2e950bbdecbeb51c1f504b9c18b1ee.jpg?x-oss-process=image/watermark,size_14,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)![watermark,size_14,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=](https://s4.51cto.com/images/blog/202107/23/045c335d5512629b010add25ea026114.jpg?x-oss-process=image/watermark,size_14,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)

渣土车、收运车的载重信息可以通过在中转站、收运点、填埋场等地进行采集上报，一方面用于分析车辆有没有被最大化利用，来减少车辆的配置数量、规划行驶路线，节约环卫成本；

另一方面可用于分析中转站、填埋场分布情况是否合理，对城市的清运效率的影响、对周边居民生活环境的影响等。

对此本系统还提供了轨迹追踪功能，更加直观地呈现环卫车清运流程。

![watermark,size_14,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=](https://s4.51cto.com/images/blog/202107/23/54aacd7180b9b384cbf856d791fbea3f.jpg?x-oss-process=image/watermark,size_14,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)

# 公共设施

针对“公共设施的配置覆盖范围无法监测” 的问题，本系统提供 回收站、公厕 的 定位 和 状态查看 功能， 另外还可以通过查看具体的人或设施的 覆盖范围，针对环卫死角进行人员补充、公共设施合理配置。

覆盖范围的效果采用扩散的半透爆破效果，能够很清晰地表达出各个环卫区间的重叠、空缺。

![watermark,size_14,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=](https://s4.51cto.com/images/blog/202107/23/686823b0f97bbe0ca316943fc8adb625.jpg?x-oss-process=image/watermark,size_14,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)

另外，小场景的动效也是 HT 的一大特色，例如建筑工地、中转站、垃圾填埋场的局部动画效果。

除了车辆运行动画外，所有小场景的动画都可以通过镜头来触发，只有在观测它的时候它才会触发动画，既保证了所有小场景的丰富性、观赏性，同时也保证了整个系统的性能。

![watermark,size_14,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=](https://s4.51cto.com/images/blog/202107/23/46a2b11f6554c46e8097e44134b92a01.jpg?x-oss-process=image/watermark,size_14,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)

# 环卫工

针对 “员工工作质量无法考核”  的问题，除了和公共设施一样的定位、数据面板呈现的展现方式外，环卫工还提供一个按照时间线进行定位回放的功能，通过智能手环等定位设备采集的数据来反应每个时刻环卫工的位置信息，对环卫工人的工作覆盖范围、每个时段的清扫工作量有一个直观的展示。

![watermark,size_14,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=](https://s4.51cto.com/images/blog/202107/23/fc6d506d86cba6d1c3904dea83c663d2.jpg?x-oss-process=image/watermark,size_14,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)

# 环卫区划、垃圾分类

针对 “无法精细化管理响应垃圾分类政策”的问题，本系统提供按照环卫管理区划来分区呈现每个管辖区的垃圾产量、垃圾分类处理情况，针对垃圾产量高、垃圾分类执行不到位的区域进行精细化整治。

![watermark,size_14,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=](https://s4.51cto.com/images/blog/202107/23/eec57c2fc81b4499cb162ebf66c12b37.jpg?x-oss-process=image/watermark,size_14,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)

系统还有诸多功能和面板就不一一展示了，通过这个系统可以看到 HT 在将强大的 3D 引擎 与 GIS 结合后能够更丰富地呈现城市级别的数据，更好地提供可视化服务。
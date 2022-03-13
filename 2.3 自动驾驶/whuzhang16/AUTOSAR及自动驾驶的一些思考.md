- [AUTOSAR及自动驾驶的一些思考_whuzhang16的博客-CSDN博客_特斯拉autosar](https://blog.csdn.net/whuzhang16/article/details/111209161)

- **AUTOSAR**

是什么呢？是一个规范，不是一个代码库

和互联网世界“talk is cheap，show me the code”不同，制造立国的国家喜欢规范，无规矩不成方圆。AUTOSAR是欧洲主导的规范，基本等同于是德国主导的。还有一个典型的例子，TRON是日本的操作系统规范。

特斯拉使用autosar吗？至少目前看来是没有，首先特斯拉并不是AUTOSAR联盟的成员。这张图不是最新的，不过最新的官网上没有。BTW，最新的图，有中国厂商，比如 百度。

![img](https://img-blog.csdnimg.cn/img_convert/e4be5a1a9e48637b8fecb77e19d1481b.png)

特斯拉不在里面，也说明了AUTOSAR肯定不是强制性的规范，对业内人士可能是废话。对门外汉来说，比如我，也是最近才知道，ISO 26262也不是强制性的规范。

- **AUTOSAR的定位**

AUTOSAR是Automotive Open System Architecture的缩写，面向和车辆强相关的部件，模块，系统。从AUTOSAR视角看到的有三个平台：CP，AP，IVI。

CP用于safety强相关的，AP用于有较高的算力需求的，智能驾驶，IVI则是车载娱乐。

从域控制器的角度，CP用于车身控制域，AP用于智能驾驶域，IVI则是娱乐域。

![img](https://img-blog.csdnimg.cn/img_convert/ca666fbf7c56bf6358e6ad260fb642e6.png)

上图为CP/AP/IVI的比较

- **架构特色**

AUTOSAR于03年成立，希望通过水平分层架构，促进汽车行业的协作。随着智能驾驶的兴起，16年开始了AUTOSAR AP的制定，而早期的AUTOSAR也就变成了AUTOSAR CP。

AUTOSAR目前由这几部分组成，其中Foundation属于，CP和AP共同的部分，包括，CP和AP的通信协作模块。

![img](https://img-blog.csdnimg.cn/img_convert/64d7cda346e722cd9d6868eedd17c873.png)

CP是纯规范，而AP则提供参考实现，原型等的代码，也是借鉴了IT行业代码为王的做法。

AUTOSAR是一个好的架构，比较聚焦，不尝试包罗万象。好的架构，目标应该是定义什么能做，而非什么都能做。

AUTOSAR AP选择POSIX PSE 51作为OS的要求，避免底层OS过于复杂，上层应用也被限制使用一些复杂的功能，从而避免overspec，相信这个对整个系统去满足ASIL的要求是极度有利的。

- **使用AUTOSAR AP有什么好处**

AUTOSAR CP的好处是显而易见的，因为有大量的业界的knowhow的积累，及成熟方案。

AP我觉得主要的优势，一个是容易和CP的软硬件模块进行集成。一个复杂的系统需要一个可靠的底座。还有一个优势我觉得是safety，包括上面提到的有节制的架构。

PHM（Platform Health Management）模块，我相信汽车业界的knowhow，将使得[自动驾驶](https://so.csdn.net/so/search?q=自动驾驶&spm=1001.2101.3001.7020)这样复杂的场景，可以聚焦在有挑战的前沿技术，而不是重新踩一遍以前的坑。

- **自动驾驶场景**

自动驾驶的技术栈：感知，规划，决策，控制。AUTOSAR AP本身没有直接覆盖这些技术点的软件栈，需要将相应的自动驾驶组件集成进来，比如百度Apollo，Autoware，ROS。

自动驾驶这么庞大的系统怎么保证安全呢？虽然26262有预期功能安全方面的讨论，短期内要形成共识，有技术，伦理各方面的难题需要克服。

我个人认为比较靠谱的方案是：基于CP的ADAS + 基于AP的自动驾驶

比如这样的一套硬件架构，按照ISO26262标准来看，当前处理器的安全完整性等级达到ASILB。通过使用冗余，仍然可以实现高度自动驾驶所需的ASIL D等级。

![img](https://img-blog.csdnimg.cn/img_convert/9c26ae0c37878bbd013a0afe5a5cf274.png)

在这样的系统中，冗余的微控制器执行两项任务：一方面，它执行监视功能；另一方面，它也可以用于在发生故障时提供降级的功能，以便系统能够继续以高度的可靠性执行其功能。

实际产品中，BMW iNext Ultra，小鹏P7等，都看到了这样的架构，引用一张谷俊丽博士的图：

![img](https://img-blog.csdnimg.cn/img_convert/e93a34c54f472871b396bb050a4ba5b1.png)

- **小结**

虽然有点“我也是普通人嘛”的味道，还是得声明一下，但是放到最后，是怕写在前面，很多人就不往下看了。我是汽车行业的门外汉，所以难免有很多描述不当的地方，欢迎指教，欢迎交流。
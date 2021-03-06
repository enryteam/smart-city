- [虚拟仿真测试介绍（7）：MIL、SIL、PIL和HIL是个啥 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/156854116)

## 一、基于模型的设计

基于模型的设计方法（MBD，Model Based Design）采用图形化设计和自动化代码生成，不同于基于手工编程和纸上规范的传统编程方法，具有如下优点：

（1）在统一的开发测试平台上，允许从需求分析阶段就开始验证，并做到持续不断的验证与测试；

（2）产品的缺陷暴露在产品开发的初级阶段，开发者把主要精力放在算法和测试用例的研究上，嵌入式代码的生成和验证则留给计算机去自动完成；

（3）大大缩短了开发周期与降低开发成本。

基于模型的设计方法的不同阶段，分别采用MIL/SIL/PIL/HIL等测试方法，有效的对嵌入式代码进行测试和验证。其中：

MIL，Model in the Loop：模型在环测试；

SIL，Software in the Loop：软件在环测试；

PIL，Processor in the Loop：处理器在环测试；

HIL，Hardware in the Loop：硬件在环测试。

## 二、MIL、SIL、PIL和HIL介绍

假设我们现在要开发一款AEB控制器：

**（1）MIL**

假设我们已经在支持MBD的工具（如Simulink）中，使用图形化的方法开发出了AEB的算法，现在想要验证该算法是否满足要求，那么我们需要开发一个（或是有现成的其他工具）被控对象模型，在这里例子里是一个车辆模型。将控制算法和车辆模型连接起来，形成闭环，并变换输入和车辆模型状态，来对控制算法的功能进行测试。如下图所示：

![img](https://pic3.zhimg.com/80/v2-04543122f4af161c8210edf1ece0882e_720w.jpg)

**（2）SIL**

现在我们将Simulink中开发的算法自动生成为c代码。但是由于代码自动生成工具本身的原因或者代码生成工具没有正确设置或者其他未知原因，自动生成代码过程可能会引入一些错误。所以我们需要验证自动生成的代码与算法模型的一致性，这就是SIL测试。SIL测试使用与MIL相同的测试用例，查看对于相同的测试用例，查看其输出是否与MIL阶段一致。为了测试的高效性，有时甚至不接入被控对象模型，而是对算法模型和生成代码进行相同的输入，查看输出是否一致。如下图所示：

![img](https://pic3.zhimg.com/80/v2-04543122f4af161c8210edf1ece0882e_720w.jpg)

**（3）PIL**

将自动生成的代码编译为目标处理器需要的形式，并下载到目标处理运行，为了防止编译过程引入新的错误，此时需要进行PIL测试。PIL测试也是等效性测试，其方式与SIL类似，不同之处是编译好的算法运行在目标处理器上，SIL测试是在算法开发环境进行的（如windows）。

**（4）HIL**

在开发出完整的控制器后，有时被控对象（整车）还未完成开发；有时使用真实被控对象进行测试太危险或成本高：出于这些不同的原因，采用真实控制控制器和虚拟被控对象的HIL测试常常被使用。如下图所示：

![img](https://pic3.zhimg.com/80/v2-3e5a2ae911f024dab13e4862c54f5d12_720w.jpg)

## 三、总结

四种测试方法各自的特点如下表所示：

![img](https://pic4.zhimg.com/80/v2-f7611386222c9954dc4800ff5c33ff77_720w.jpg)

最后谢谢您宝贵的正激励和正反馈！
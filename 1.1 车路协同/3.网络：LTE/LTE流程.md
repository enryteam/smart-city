- [LTE流程](https://www.cnblogs.com/zhangbing12304/p/9261029.html)

LTE 过程全流程 

1. UE处于关闭状态 
2. 打开UE电源。 
3.  搜索附近的频率 
4. 同步时间 
5.  小区搜索 
6.  小区选择 
7.  解码MIB 
8. 解码SIB 
9. 初始化RACH过程 
10. 注册/认证/附着 
11.  建立默认EPS承载 
12. EPS处于IDLE状态 
13. <如果此时当前小区信号变弱或者UE移动到另外的小区去的情况>小区重选 
14. <如果此时UE侦测到了寻呼消息或者UE发起了拨号>RACH过程 
15.  建立专用EPS承载 
16. 接收数据 
17. 传输数据 
18.  <如果此时网络接收到的UE信号太弱>网络向UE发出TPC指令，要求UE提高传输能量 
19.  <如果此时网络接收到的UE信号太强>网络向UE发出TPC指令，要求UE降低传输能量 
20.  <如果此时UE移动到另外的小区>网络和UE之间进行切换 
21.  用户停止通话，UE回到IDLE模式。

国际移动客户识别码(International Mobile Subscriber Identification Number) 
 为了在无线路径和整个GSM移动通信网上正确地识别某个移动客户，就必须给移动客户分配一个特定的识别码。这个识别码称为国际移动客户识别码(IMSI)，用于GSM移动通信网所有信令中，存储在客户识别模块(SIM)、HLR、VLR中。IMSI号码结构为：  
 MCC+MNC+MSIN （国际移动客户识别 +国内移动客户识别+移动客户识别码 ） 

![image-20220214135646930](https://gitee.com/er-huomeng/l-img/raw/master/l-img/image-20220214135646930.png)

MCC＝移动国家号码，由3位数字组成，唯一地识别移动客户所属的国家。中国为460。 
 MNC＝移动网号，由2位数字组成，用于识别移动客户所归属的移动网。 

- 中国移动公司GSM PLMN网为00 
- 中国联通公司GSM PLMN网为01。  

MSIN＝移动客户识别码，采用等长11位数字构成。唯一地识别国内GSM移动通信网中的移动客户。

国际移动台设备识别码(International Mobile Equipment Identity) 
 唯一地识别一个移动台设备的编码，为一个15位的十进制数数字，其结构为：

![image-20220214135655487](https://gitee.com/er-huomeng/l-img/raw/master/l-img/image-20220214135655487.png)

TAC＝型号批准码，由欧洲型号认证中心分配。 
 FAC＝工厂装配码，由厂家编码，表示生产厂家及其装配地。 
 SNR＝序号码，由厂家分配。识别每个TAC和FAC中的某个设备的。 
 SP＝备用，备作将来使用。
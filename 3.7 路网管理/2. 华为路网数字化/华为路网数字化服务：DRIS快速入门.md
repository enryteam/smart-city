## 一、设备快速接入概述

路网数字化边缘服务通过摄像头、雷达设备识别路面交通事件，通过路网数字化服务下发到路侧单元，转发车载单元。主要场景为异常车况、异常路况类事件。

路网数字化服务为您提供以下功能：

- 建立交通事件，下发至路侧单元，路侧单元转发给车载单元。主要场景为车内标牌、恶劣天气类事件。
- 城市/区域交通实时监控，覆盖交通事故数、联接车辆数、拥堵路段、车型分布 、车流量、事故高发路段排行、在线设备数等重要指标。
- RSU（Road Side Unit，路侧单元）等设备状态实时监控，帮助企业随时掌握设备情况，助力设备故障及时处理。
- 边云协同能力，可实现云上控制的路网数字化边缘服务的软件部署和更新。
- 数据存储和数据开放接口。

![点击放大](https://support.huaweicloud.com/qs-v2x/figure/zh-cn_image_0000001074383306.png)

本节内容为您介绍在购买路网数字化服务后，如何快速对接设备，构筑路网数字化服务，使能智慧交通助力自动驾驶。

## 二、快速对接一个Edge设备示例

本节内容为您介绍在购买路网数字化服务后，如何在路网数字化平台快速对接一个边缘Edge设备。

**操作步骤**

1. 进入路网数字化服务控制台，选择“设备管理 >  设备总览 >  边缘Edge >  注册Edge”。

   ![image-20211119104628833](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119104628833.png)

2. 在弹出的对话框输入设备基本信息。

   ![img](https://support.huaweicloud.com/qs-v2x/figure/zh-cn_image_0000001091143045.png)

3. 填写“设备名称”。

   该边缘设备的名称，建议统一规划。仅支持中文、字母、数字、下划线、中划线，长度不能超出128个字符。

4. 填写“设备编码”。

   该边缘设备的设备编码（ESN）。仅支持字母、数字、下划线，长度不能超出64个字符。

5. 填写“位置编码”。

   该边缘设备实际部署位置的位置编号，需统一规划。仅支持字母、数字、下划线，长度不能超出128个字符。

6. 填写“IP地址”。

   该边缘设备设置的本地IP地址，需统一规划。

7. 填写“描述”。

   该边缘设备的描述信息，由用户自定义。

8. 填写“经纬度”。

   该边缘设备的经纬位置。

9. 填写“用户名”。

   该边缘设备注册的用户名。

10. 填写“密码”。

    该边缘设备注册的密码。

11. 输入关联设备信息。

    ![img](https://support.huaweicloud.com/qs-v2x/figure/zh-cn_image_0000001090992197.png)

12. 填写“关联的RSU”。

    该Edge预期关联的RSU设备列表。

13. 选择Edge通用配置信息。

    ![img](https://support.huaweicloud.com/qs-v2x/figure/zh-cn_image_0000001075698605.png)

14. 设置“AVP场景”。

    开启选项，该Edge将用于AVP（自动泊车）场景。

15. 设置“RSM上报”。

    开启选项，该Edge将识别的RSM消息上传到云端。

16. 设置“时延补偿”。

    开启选项，该Edge可以根据交通参与者的历史时刻的位置和速度等信息预测出当前时刻的信息，以弥补机器学习算法带来的目标识别时延。

17. 获取安装命令并复制。

    ![img](https://support.huaweicloud.com/qs-v2x/figure/zh-cn_image_0000001085230062.png)

18. 获取安装命令后，参考[《ITS800连接V2Xserver》](https://support.huaweicloud.com/qs-v2x/v2x_05_0016.html)内的步骤启动边缘节点，完成线下部署设备后才能上线该Edge设备。

    ![img](https://res-img2.huaweicloud.com/content/dam/cloudbu-site/archive/china/zh-cn/support/resource/framework/v3/images/support-doc-new-notice.svg)须知： 该边缘节点安装命令的有效时间为生成后30分钟，请在30分钟内使用。

19. 添加业务通道，根据实际情况选择业务平台，单击“确定”完成注册。

    ![img](https://gitee.com/er-huomeng/l-img/raw/master/zh-cn_image_0000001085231176.png)

20. 当Edge设备列表中的Edge状态为“在线”，表示该Edge设备和路网数字化服务对接成功。后续可去Edge详情页面[开通业务通道](https://support.huaweicloud.com/qs-v2x/v2x_05_0005.html#ZH-CN_TOPIC_0000001072901551__section16159142710296)和[部署应用](https://support.huaweicloud.com/qs-v2x/v2x_05_0005.html#ZH-CN_TOPIC_0000001072901551__section209202045175513)。

### 2.1 开通业务通道

边缘节点安装完成后，单击“详情 >  业务通道 >  新增通道”，根据实际情况选择业务平台。

![点击放大](https://support.huaweicloud.com/qs-v2x/figure/zh-cn_image_0000001091016977.png)

![点击放大](https://support.huaweicloud.com/qs-v2x/figure/zh-cn_image_0000001090872953.png)

### 2.2 部署应用

1. 边缘节点安装完成后，等待边缘节点的设备状态为“在线”。

   ![image-20211119104733106](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119104733106.png)

2. 单击“详情 >  应用部署”，参照[表1](https://support.huaweicloud.com/qs-v2x/v2x_05_0005.html#ZH-CN_TOPIC_0000001072901551__table169811311316)输入应用信息。

   ![image-20211119104748410](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119104748410.png)

   | 参数名称 | 说明                                                         |
   | -------- | ------------------------------------------------------------ |
   | 应用名称 | 除了路网数字化平台默认应用外，还需要提前在[边缘应用管理](https://support.huaweicloud.com/qs-v2x/v2x_05_0008.html)添加第三方边缘应用。 下拉列表，选择新增边缘应用的名称。 |
   | 应用版本 | 下拉列表，选择当前最高版本的边缘应用。                       |

## 三、快速对接一个RSU设备示例

本节内容为您介绍在购买路网数字化服务后，如何在路网数字化平台快速对接一个路侧RSU设备。

### 3.1 操作步骤

1. 路网数字化服务的RSU设备完成现场部署后，获取RSU设备信息，其中设备编码必须和RSU设备一致，否则RSU无法完成接入。

2. 获取路网数字化服务设备侧接入地址及端口，并在RSU上配置完成。

3. 进入路网数字化服务控制台，选择“设备管理 >  设备总览 >  路侧RSU >  注册RSU”。

   ![image-20211119104827473](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119104827473.png)

4. 在弹出的对话框输入RSU基本信息。

   ![img](https://gitee.com/er-huomeng/l-img/raw/master/zh-cn_image_0000001091019189.png)

5. 填写“设备名称”。

   该RSU设备的名称，建议统一规划。仅支持中文、字母、数字、下划线、中划线，长度不能超出128个字符。

6. 填写“设备编码”。

   该RSU的设备编码（ESN）。仅支持字母、数字、下划线，长度不能超出64个字符。

7. 填写“位置编码”。

   该RSU实际部署位置的位置编号，需统一规划。仅支持字母、数字、下划线，长度不能超出128个字符。

8. 填写“Edge连接上限”。

   表示该RSU最大连接的Edge个数。

9. 填写“IP地址”。

   该RSU设置的本地IP地址，需统一规划。

10. 填写“描述”。

    该RSU的描述信息，由用户自定义。

11. 选择“RSU型号名称”。

    下拉列表，选择新增的RSU设备名称。需要提前在设备类型配置中进行[RSU类型配置](https://support.huaweicloud.com/qs-v2x/v2x_05_0009.html)。

12. 填写“RSU密钥”。

    输入字母（a-f或A-F），输入数字（最少输入8位）。

    ![img](https://res-img3.huaweicloud.com/content/dam/cloudbu-site/archive/china/zh-cn/support/resource/framework/v3/images/support-doc-new-caution.svg)注意： 该密钥很重要，请自行储存，为安全起见查询RSU时不再反显。

13. 单击“确定”完成注册。在路侧RSU的设备列表中，当设备列表中RSU设备状态为“在线”，表示该设备和路网数字化服务对接成功。

## 四、快速管理第三方边缘应用

在部署边缘Edge应用前，需要先添加边缘应用。

### 4.1 添加应用

1. 进入路网数字化服务控制台，选择“边缘应用管理 >  添加应用”。

   ![点击放大](https://support.huaweicloud.com/qs-v2x/figure/zh-cn_image_0000001072598187.png)

2. 填写应用名称及描述信息。

3. 单击“保存”，在边缘应用管理页面可查看创建好的应用，单击应用名称可查看应用详情。

### 4.2 添加版本

应用添加成功后，需要设置应用对应的版本信息。

1. 选择“边缘应用管理 > 详情  >  添加版本”，设置版本基本信息。

   ![image-20211119115231447](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119115231447.png)

   ![image-20211119115247757](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119115247757.png)

2. 填写“应用版本”。

   输入标识该应用的版本信息。

3. 选择“镜像”。

   下拉列表，根据实际情况选择我的镜像或他人共享的镜像。

   ![img](https://res-img3.huaweicloud.com/content/dam/cloudbu-site/archive/china/zh-cn/support/resource/framework/v3/images/support-doc-new-note.svg)说明： 如果没有对应镜像，请单击容器镜像服务前往上传镜像，根据[《容器镜像服务相关指导》](https://support.huaweicloud.com/qs-swr/index.html)上传镜像。

4. 选择“支持架构”。

   下拉列表选择架构信息。

5. 设置“容器规格”。

   根据实际情况配置CPU、内侧、GPU、NPU的申请配额及限制配额。

6. 单击“下一步”，进行部署配置。

7. 设置“重启策略”，单击“提交”，完成版本的添加。

   - 总是重启：当应用退出时，无论是正常退出还是异常退出，系统都会重新启动应用。
   - 失败时重启：当应用异常退出时，系统会重新启动应用。
   - 从不重启：当应用退出时，无论是正常退出还是异常退出，系统不会重新启动应用。

8. 回到应用详情页面，单击“发布”。

   ![image-20211119115310711](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119115310711.png)

   ![img](https://res-img3.huaweicloud.com/content/dam/cloudbu-site/archive/china/zh-cn/support/resource/framework/v3/images/support-doc-new-note.svg)说明： 

   - 未发布的版本为草稿，支持编辑及发布。
   - 已发布的版本，不可编辑，且版本为发布状态，无法删除应用。
   - 发布的版本，可以申请下线，下线后，可重新发布。

## 五、快速配置RSU设备类型

注册路测RSU必须预先配置设备类型。

**操作步骤**

1. 进入路网数字化服务控制台，单击“设备管理 >  设备类型配置 >  RSU类型 >  新增RSU类型”。

   ![image-20211119105049872](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119105049872.png)

2. 填写“设备类型名称”。

   输入中文、数字、字母、下划线、_?'#().,&%@!-长度不能超出64位字符。

3. 填写“设备厂商”。

   输入中文、数字、字母、下划线、_?'#().,&%@!-长度不能超出32位字符。

4. 填写“描述”。

   该设备的描述信息，由用户自定义。

5. 单击“确认”，完成配置。

## 六、在线调试

为了降低应用侧的开发难度、提升应用侧开发效率，物联网平台向应用侧开放了丰富的API。

本文档以在线调试（即API Explorer）为例，使用API Explorer可以无码化快速调用接口。

API Explorer提供在线API检索及接口调试，您可以使用在线调试快速接入物联网平台。

**操作步骤**

1. 打开[API Explorer](https://apiexplorer.developer.huaweicloud.com/apiexplorer/overview)。

2. 选择“物联网 >  路网数字化服务”。

   ![点击放大](https://support.huaweicloud.com/qs-v2x/figure/zh-cn_image_0000001072960867.png)

3. 选择需要调试的接口进行调试：

   ![Snipaste_2021-11-19_10-51-44](https://gitee.com/er-huomeng/l-img/raw/master/Snipaste_2021-11-19_10-51-44.png)

## 七、快速玩转路网数字化平台

### 7.1 手动事件下发示例

路网数字化服务场景中的大部分事件会由设备侧根据天气和路况等情况，自行识别交通事件上报至平台并转发给车载单元，同时路网数字化服务也支持用户手动下发事件。

路网数字化服务覆盖《合作式ITS车用通信系统应用层及应用数据交互标准》中306种[V2X事件](https://support.huaweicloud.com/api-v2x/v2x_04_082.html)（249种标志标牌及57种交通事件），典型交通事件单击[产品规格](https://support.huaweicloud.com/productdesc-v2x/v2x_01_0009.html)查看。

本节内容为您介绍在对接完设备之后，如何使用路网数字化平台进行手动事件下发。

#### 7.1.1 操作步骤

1. 下发事件需要完成[RSU设备接入](https://support.huaweicloud.com/qs-v2x/v2x_05_0007.html)，并且已获取事件类型、事件发生地点、影响范围、事件发生时间以及事件等级。

2. 在左侧导航栏，选择“事件管理 >  平台下发事件 >  下发事件”。

   ![image-20211119104331272](https://gitee.com/er-huomeng/l-img/raw/master/image-20211119104331272.png)

3. 填写“事件类型”。

   选择事件发生类型。若用户需要的类型未在界面上呈现，也可通过事件名称和编码进行搜索查询。

4. 填写“事件数值信息”。

   事件数值信息会根据事件类型的选择而呈现不同的显示。

   当交通事件类型为急转弯、道路最高限速、道路最低限速、沙尘暴时，该字段必填。

5. 填写“事件发生地点”。

   定位事件发生的地点，有三种添加方式：

   - 通过“事件发生地点”搜索框查找事件发生的大概位置，支持模糊搜索，搜索成功后左侧地图会自动定位到该区域。若搜索结果存在多个区域需要用户自定选择在哪个区域。
   - 在地图上单击鼠标右键，设置事件发生地点。
   - 通过经纬度定位发生地点。

6. 填写“事件影响范围”。

   设置事件影响的单个或多个范围，所有经过影响范围的已安装T-BOX的车辆都会收到事件预警信息。

   在地图上单击鼠标右键分别设置事件发生范围的起点和终点。

7. 选择“优先级”。

   优先级的划分：0-2级优先级为低，3-5级为中，6-7级为高。由低到高代表事件造成的影响从轻微拥堵到水泄不通。

8. 设置“事件发生时间”。

   设置事件发生时间，分别设置起始时间和结束时间。

9. 填写“事件描述”。

   填写事件描述信息，T-BOX侧收到的事件描述。

10. 填写“备注信息”。

    填写事件备注信息，该字段只提供用户对该事件进行备注，不会下发到T-BOX。

11. 单击“确认下发”，完成事件下发。

- [LTE基本架构](https://www.cnblogs.com/zhangbing12304/p/9261042.html)

主要介绍LTE的最基础的架构，包括LTE网络的构成，每一个网络实体的作用以及LTE网络协议栈，最后还包括对一个LTE数据流的模型的说明。

## 1 LTE网络参考模型

![这是摘自Netmanias的图](https://img-blog.csdn.net/20171205135248900?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvc3RhcnBlcmZlY3Rpb24=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast) 
 这是一张非常有名的LTE架构图，从图中可以看出，整个网络构架被分为了四个部分，包括由中间两个框框起来的E-UTRAN部分和EPC部分，还有位于两边的UE和PDN两部分。 
 在日常生活中，UE就可以看作是我们的手机终端，而PDN可以看作是网络上的服务器，E-UTRAN可以看作是遍布城市的各个基站（可以是大的铁塔基站，也可以是室内悬挂的只有路由器大小的小基站），而EPC可以看作是运营商（中国移动/中国联通/中国电信）的核心网服务器，核心网包括很多服务器，有处理信令的，有处理数据的，还有处理计费策略的等等。 
 下面详细地介绍每一个组件的名称与作用

### UE

全称是User Equipment，用户设备，就是指用户的手机，或者是其他可以利用LTE上网的设备。

### eNB

是eNodeB的简写，它为用户提供空中接口（air  interface），用户设备可以通过无线连接到eNB，也就是我们常说的基站，然后基站再通过有线连接到运营商的核心网。在这里注意，我们所说的无线通信，仅仅只是手机和基站这一段是无线的，其他部分例如基站与核心网的连接，基站与基站之间互相的连接，核心网中各设备的连接全部都是有线连接的。一台基站(eNB)要接受很多台UE的接入，所以eNB要负责管理UE，包括资源分配，调度，管理接入策略等等。

### MME

是Mobility Management Entity的缩写，是核心网中最重要的实体之一，提供以下的功能：

- NAS 信令传输
- 用户鉴权与漫游管理（S6a）
- 移动性管理
- EPS承载管理

在这里所述的功能中，NAS信令指的是三层信令，包含EMM, ESM 和NAS 安全。然后移动性管理的话主要有寻呼，TAI管理和切换。承载的话主要是EPS 承载（bearer）的建立，修改，销毁等。

### S-GW

是Serving Gateway 的缩写，主要负责切换中数据业务的传输。

### P-GW

是PDN Gateway的缩写，其中PDN是Packet Data Network  的缩写，通俗地讲，可以理解为互联网，这是整个LTE架构与互联网的接口处，所以UE如果想访问互联网就必须途径P-GW实体，从另外一方面说，如果想通过P-GW而访问互联网的话，必须要有IP地址，所以P-GW负责了UE的IP地址的分配工作，同时提供IP路由和转发的功能。此外，为了使互联网的各种业务能够分配给不同的承载，P-GW提供针对每一个SDF和每一个用户的包过滤功能。（也就是说在P-GW处，进出的每一个包属于哪个级别的SDF和哪一个用户都已经被匹配好了。这里的SDF是服务数据流Service Data  Flow的缩写，意思就是P-GW能区分每一个用户的不同服务的数据包，从而映射到不同的承载上去。以后会有关于SDF的更详细的说明）。此外，P-GW还有其他的一些功能，比如根据用户和服务进行不同的计费和不同的策略，这部分对于每个运营商都会有差异，在此不做多的赘述。

### HSS

是Home Subscriber Server的缩写，归属用户服务器，这是存在与核心网中的一个数据库服务器，里面存放着所有属于该核心网的用户的数据信息。当用户连接到MME的时候，用户提交的资料会和HSS数据服务器中的资料进行比对来进行鉴权。

### PCRF

是Policy and Charging Rules Function的缩写，策略与计费规则，它会根据不同的服务制定不同的PCC计费策略。

### SPR

是Subscriber Profile Repository的缩写，用户档案库。这个实体为PCRF提供用户的信息，然后PCRF根据其提供的信息来指定相应的规则。（这个我也不是很明白其具体内容）

### OCS

是Online Charging System 的缩写，在线计费系统，顾名思义，应该是个用户使用服务的计费的系统

### OFCS

是Offline Charging System 的缩写，离线计费系统，对计费的记录进行保存。

上面介绍完了图中所有的实体的名称以及作用，其实真实的核心网中远远不止这些实体，还有很多，鉴于我也不是很懂，在此就不多说了。

然后下面针对图中主要的几个接口说说

### LTE-Uu

LTE-Uu接口是位于终端与基站之间的空中接口。在这中间，终端会跟基站建立信令连接与数据连接，信令连接叫做RRC  Connection，相应的信令在SRB上进行传输，（这里，SRB有三类，分别是SRB0,  SRB1和SRB2，SRB可以理解为是传输信令的管道），而数据的连接是逻辑信道，相关的数据在DRB上传输。这两个连接是终端与网络进行通信所必不可少的。

### X2（控制面）

X2是两个基站之间的接口，利用X2接口，基站间可以实现SON功能（Self Organizing Network），比如PCI的冲突检测等。

### S1（控制面）

S1是基站与MME之间的接口，相关NAS信令的传输都必须建立在S1连接建立的基础上。

### X2（用户面）

X2用户面的接口是建立在GTP-U协议的基础上，连接两个基站，传输基站间的数据。（X2 handover等）

### S1（用户面）

S1用户面的接口是建立在GTP-U协议的基础上，连接基站与MME，传输基站与MME之间的数据。（S1 handover，上网的数据流等）

剩下的接口在我个人的工作中没有接触，不是很了解，这里就不多说了。

## 2 LTE协议栈

说协议栈，就得分开从两方面来讲，分别是用户面与控制面。 
 先从用户面开始说起

![LTE User Plane Protocol Stack](https://img-blog.csdn.net/20171205171429612?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvc3RhcnBlcmZlY3Rpb24=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

上图是用户面的协议栈，下面详细地介绍每一个层（主要功能）

### 2.1 LTE-Uu 接口

#### PDCP

PDCP协议针对传输地数据包执行以下的操作：

- 数据包头压缩（ROHC）
- AS层的安全（包括加密与完整性检验）
- 包的重排序和重传

#### RLC

RLC层针对传输地数据包执行以下的操作：

- 在发送端，提供数据包的分段与串联
- 在接收端，提供透明，确认模式与非确认模式三种模式
- RLC层也执行对RLC PDU的重排序与重传

#### MAC

MAC层对从高层传来的MAC PDU和从底层传来的包做以下的处理：

- 在物理层和RLC层之间提供逻辑信道的连接
- 逻辑信道的复用与解复用
- 对逻辑信道根据QoS来进行调度和分配优先级

### 2.2 S1-U/S5/X2 接口

#### GTP-U

GTP-U协议主要是用来转发用户的IP数据包，GTP-U协议还有个特点，只要GTP-U连接建立后传输数据，那么在数据结束之后总会有END Marker来标志着数据流的结束。

下面是控制面的协议栈

![LTE协议控制面](https://img-blog.csdn.net/20171207142514879?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvc3RhcnBlcmZlY3Rpb24=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

上面是关于控制面的总图，包含了LTE-Uu，S1-MME，S11等接口的，由于本人业务限制，对其他的不了解，就只简单地介绍下面几个

### 2.3 LTE-Uu接口

#### NAS

提供移动性管理和承载管理，比如说eNB的信息的更新，或者MME的配置信息的更新会触发Configuration Update信令的下发或者上载，然后E-RAB的建立，修改，销毁都是属于NAS管理的范围之内。

#### RRC

RRC协议支持传输NAS信令， 同时也提供对于无线资源的管理

- 广播系统消息，例如MIB，SIB1，SIB2 ……
- RRC连接的建立，重建立，重配置和释放
- 无线承载(RB)的建立，修改与释放。

### 2.4 X2 接口

#### X2AP

X2AP协议支持无线网（E-UTRAN）中的UE移动性管理和SON功能。比如通过X2AP的数据转发（在X2 Handover的时候的数据转发），SN status的转发（Handover时），或者时eNB之间的资源状态消息交换等。

### 2.5 S1-MME

#### S1AP

S1AP协议如前所述，是S1 连接建立的时候用来传输信令的协议，该协议负责S1接口的管理，E-RAB的管理，还有NAS信令的传输，以及UE上下文的管理。

## 3 一个简单的例子

这里通过一个简单的例子来全盘地看一下LTE系统是怎么样运转地。

首先是从终端到Internet的方向传输，也就是我们通常所说的“上行传输” 
 ![上行传输](https://img-blog.csdn.net/20171207145344658?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvc3RhcnBlcmZlY3Rpb24=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

上面这个例子记述了包从UE是怎么一步一步地通过LTE系统传输到Internet的。 
 首先，UE发出一个包时，包上面会打上UE的地址作为源地址，要去的因特网上的服务器的地址作为目的地址，传送给基站eNB，然后基站给包封装到GTP  隧道里可以传输的GTP包，每个包的源地址会被换成基站的地址，而目的地址则是被换成将要到达的Serving  Gateway，然后，每个包也会包含他们所在传输隧道的隧道ID：UL S1-TEID。当包到达Serving  Gateway时，源目地址被分别换成了Serving Gateway和P-GW的地址，同时，传输的隧道也由S1 GTP 隧道变成了S5  GTP隧道，当然隧道ID也会随之变化。最后，当包到达P-GW后，这时P-GW讲GTP解开，查看其真正的目的地址，然后将包送到互联网上。这样子就完成了一个数据包从终端的互联网的上传。

下面看一下下行的传输

![下行传输](https://img-blog.csdn.net/20171207150946863?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvc3RhcnBlcmZlY3Rpb24=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

下行的情况与上行的情况正好相反，经过P-GW，S-GW，eNB时会对数据包打包，在eNB处会解封装，然后直接把数据包传输给UE。
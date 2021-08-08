（共16讲）

# 网络工程师前景及基础介绍

# 第2专题-网络工程师前景及基础知识

## 02网络组建、协议栈以及园区网架构（2021.07.29，2h20min）：

![image-20210729170945927](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210729170945927.png)

### 1.网络组件

1. 终端系统 （AP ,ACCESS POINT,我们所说的路由器是AP）
2. 介质（传输数据的媒介：有线/无线）
3. 网络设备（又叫中间系统：一般分为一层设备Hub(集线器，非常古老，已经被淘汰，被交换机取代)，二层Switch，三层Router。最早期的网络定义为“工作组”，没有中间系统，是最原始的局域网LAN。Full Mesh，全互联。但是缺点是每台计算机的网卡数量有限，并且主板支持的网卡数量有限。后来，经过优化，微软提出了“Client Server”的概念：所有Client都连接到Server，而Client之间不需要连接就可以通信。后来再经过优化，为了调高Server的效率，发明了“Hub集线器”，因此有很多网卡且有足够的转发能力。之后又升级为交换机）

拓扑:

Topology 网络连接图

物理拓扑，预先设计的时候使用；逻辑拓扑，排错时候使用

![image-20210729173940149](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210729173940149.png)

直线代表双绞线或者光纤，是局域网线缆

闪电代表广域网线缆

MLS: 多层交换机，相等于普通二层交换机和三层路由器

### 2.协议与协议栈

Protocol:协议、规则、约定

因特网：由全球运营商维护

**协议栈：协议集合（曾经有这几种协议栈：OSI TCP/IP IPX/SPX AppleTalk）**

局域网LAN协议：**Ethernet** 以太网协议(最流行)、Token Ring 令牌环协议、FDDI光纤分布数据接口

PPP over Ethernet(PPPoE)

广域网WLAN协议:HDLC高级数据链路协议、PPP点到点协议、Frame Relay帧中继协议、ATM异步传输模式协议

Serial 串行线缆（可编程的线缆）

光纤：多模光纤、单模光纤（传输1000km）

### 3.拓扑结构

园区网（Campus Network），又叫AS自制系统。

分为两级别：

Client：客户的园区网

ISP:运营商的园区网（组成骨干线路）

IDC:因特网数据中心，存放各种服务器

3级架构：包含网络设备

1. 接入层Access Layer（端口密度比较高，比较廉价，高速率转发设备，例如集线器Hub）

2. 汇聚层Distributed Layer（MLS 光纤，两台）

3. 核心层（路由器，多层交换机MLS）



## 03 拓扑分类以及Hub&Switch工作原理(1h40min)

2021.07.30（周五）

1. 拓扑结构
2. Hub以及Switch的工作原理
3. OSI参考模型

### 1.拓扑结构

局域网（LAN）协议：Ethernet、Token Ring、FDDI

广域网（WLAN）协议：HDLC高级数据链路协议、PPP点到点协议、Frame Relay帧中继协议、ATM异步传输模式协议

注意以下的拓扑分类（注意，不是拓扑结构）

总线型Bus Topology：

集线器Hub, 双绞线，PC

**Hub是物理层设备**，不智能，总线型规定了一台计算机发送数据，其他计算机只能接收

带宽Bandwidth（描述网络的快慢）：**单位时间内**通过某一节点（Node，例如，PC的网卡、路由器的接口，这些接口是3层接口。3层表示可以配置IP地址）的数据流量的总和。带宽的单位是bit/s，1Byte = 8 bit。 在bit领域中，是1000；在字节领域中，是1024。

而集线器Hub的带宽只有10Mbit/s，现在都是1000Mbit/s。并且Hub是共享带宽，例如网络内有2台计算机，则每台的只能使用10/2=5Mbit/s。

Duplex双工模式

单工模式：只有一个单向流量。例如，光纤这种介质，一般使用两根线，一根用来发送，一根用来接受

半双工：在半双工信道上，通信双方可交替发送和接受信息，但不能同时发送和接受。

全双工：一根链路双向可以通行，并且双向流量可以同时存在

双绞线和同轴电缆既可以支持半双工，又可以支持全双工；计算机的接口两者都支持

两个QQ通信的过程：

![image-20210730093817594](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210730093817594.png)





![image-20210730085651458](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210730085651458.png)



### 2.Hub以及Switch的工作原理

#### 2.1集线器

总线型：

![image-20210730095833022](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210730095833022.png)

Flooding 泛洪处理，将收到的数据赋值为n份，通过每个接口将数据发出去

PC-A  数据冲突，形成冲突碎片

数据放大

复制n份

Ethernet称作以太网协议，是数据链路层协议

1. 定义了帧头 、帧尾

2. MAC地址（全球唯一，从IANA购买）  MA  ROM（只读存储器）
3. 定义了通信规则：自由通信
4. CSMA/CD载波侦听多路访问/冲突检测，是以太网内部的一个机制，前提是接口双工模式必须是**半双工**，看看链路是否安静，能否接受数据。

Ring型拓扑：

![image-20210730095933461](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210730095933461.png)

环形拓扑中的交换机叫做令牌环交换机，使用的协议是**Token协议**，但是提供流量带宽也是10Mbit/s，只能解决冲突，也是**半双工**模式

星型拓扑：

![image-20210730100413276](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210730100413276.png)

Catalyst发明了星型交换机，使用了CATOS交换机，最早期的45系列的交换机

交换机是数据链路层设备，是OSI的第二层，可以识别数据帧的数据报头（以太网的帧头，如，Ethernet2 IEEE 802.3 SMAC(发送主机通过哪个接口发送数据) DMAC、帧尾），而Hub不可以识别



MAC: Media Access Control，介质访问控制地址（在同一个网络中才有意义）；48bit，由12个16进制数组成。前24位是组织唯一标识符(OUI)，后24位是购买的，共有2^24=1千700万左右个。思科的MAC地址是0000.0c.....说明了思科是全球第12家购买MAC地址的厂商。后24位是Interface-ID接口。

IP地址 Node

#### 2.2交换机

它能读懂源目MAC地址

能知道自身的哪个接口连接了哪台PC 

从两个层面了解交换机：

1. 控制层面 control plane

即，一台网络设备通过什么样的方式得知网络的连接信息。网络如何获得转发信息，如何知道网络是如何连接的。

MAC地址表，叫做CAM (Content Addressful Memory)表。内容可寻址存储器，ASIC芯片，是应用专用集成电路，线速，0延迟。其中的内容是：MAC地址条目或者MAC地址表项，表示哪个接口连接哪个MAC对应的主机。因此，MAC地址表项是由**交换机自身的接口**和**该接口的PC的MAC地址**组成的。有两种方式获得MAC地址表：1. 通过Console线配置，形成静态MAC表项，但是由于维护困难不采用这种方式；2.自动学习MAC地址表项

2. 数据层面 Data Plane

当交换机获取了MAC地址表项之后，是如何通过MAC地址表项转发数据的。



# 第3专题-OSI参考模型详解

## 04：OSI以及ICP/IP协议栈（7月31日，1h42min）

上节课回顾：

![image-20210731205836561](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210731205836561.png)

以上是一个逻辑拓扑。图中网桥是二层设备，是通过服务器或者软件模拟出来的，又称为透明网桥，只拥有2个接口，目的是在总线型环境中分割冲突域。图中I、J之间使用的是集线器（Hub）,已经被省略（3层设备可以省略1/2层设备，2层设备可以省略1层设备）

本节课知识点：

## ![image-20210731200012927](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210731200012927.png)

### 1.OSI参考模型

“参考”表明不是真正使用，相反现实中使用的是“TCP/IP协议栈”

由于每种硬件厂商生产设备的时候使用不同的标准，例如因特尔使用自己的标准生产CPU，IBM使用自己的标准生产其他硬件，但是标准不同会造成不兼容。因此，国际标准化组织（ISO,international standard organization)打破了这一僵局。使用开放式系统互联（Open Standard interconnection）作为统一的协议栈。其中参考了不同厂商的私有标准。

#### 7：Application  layer

7：Application  layer--------------------->网络最终为应用提供服务,例如知名应用程序，使用Port 1-1023标识这些程序；对于其他非知名应用程序，使用Port 1024-65535标识。例如HTTP端口永远是80

#### 6：Presentation layer

6：Presentation layer------------------>表示层

否则出现乱码

例如下面的例子：

![image-20210731213219532](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210731213219532.png)

#### 5：Session layer

5：Session layer-------------------->会话层  （上三层只关注应用程序，不关注流量交互，统称为应用层）

#### 4：Transport layer

4：Transport layer------------------>传输层 （下四层统称为传输层，关注流量如何传递）

以太网协议中有个参数：MTU= 1500字节

Jumbo MTU >= 9000 9100 9216

1. 第一件事情：数据分片/数据切片
2. 数据载荷：添加数据分片报头，Layer4 Header |数据载荷 。将四层的 PDU称为 数据段 Segment

Layer4 Header含有源目端口号。四层的协议只有两种：TCP、UDP

#### 3：Network Layer

3：Layer3 Header | Layer 4 Header| 数据载荷 。将此三层的PDF称为数据包Packet

三层的协议只有IPv4或者IPv6，三层报头重要的两个信息：**SIP（源IP地址）、 DIP（目的IP地址）**。其中IP是 internet Protocol的缩写，它和 MAC地址有本质的区别。MAC地址是二层地址，是物理地址；而IP地址是三层地址，是网络地址或者协议地址。两者都可以标识接口（即一个节点，用Node标识）。但是MAC地址只能在一个网络内标识，而一个网络就是一个广播域，不同网络之间的MAC地址是无效的，只能用IP地址标识。

#### 2：Link layer

2：Link layer-------------------->二层

2层报头|3层报头|4层报头|数据载荷|2层报尾（FCS）     数据链路层的PDU成为Frame，即数据帧。

2层报头最重要的信息是SMAC DMAC

为什么不在同一个网络的两台主机通过路由器转发，MAC地址无效？例子如下：

![image-20210731220935192](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210731220935192.png)

#### 1：Phisical layer

1：Phisical layer------------->一层。在这一层中，数据帧转换为比特流。

因此接收方是从第一层到第七层，而发送方是从第七层到第一层。

以上内容总结如下：

# ![image-20210731221700306](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210731221700306.png)

# ![image-20210731221723006](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210731221723006.png)



![image-20210731221901106](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210731221901106.png)

由于OSI太复杂了，成本太高。因此TCP/IP诞生了。

### 2.TCP/IP和OSI相同和不同

4应用层						对应OSI（Open Standart Interconnection,开放式标准互联）    5,6,7

3主机到主机层			对应OSI（Open Standart Interconnection,开放式标准互联）    4

2因特网层					对应OSI（Open Standart Interconnection,开放式标准互联）    3

1网络接口层				对应OSI（Open Standart Interconnection,开放式标准互联）    2

封装机制的不同：

OSI是逐层分装；TCP/IP跃层封装

![image-20210731223543078](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210731223543078.png)



## 05：OSI物理层、数据链路层主流技术（8月2日，1h46min）



### 1.物理层

物理层的作用：将数据帧变为bit流，不进行封装、添加报头等，再将bit流变为脉冲信号通过接口发走。



![image-20210801132447087](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210801132447087.png)

10BASE5:10bit/s (支持的最大速率，基带传输)

![image-20210801132715566](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210801132715566.png)

EIA/TIA:电子工业联合会/电信工业联盟 制定了物理层各种标准

568B 橙白 橙 绿白 蓝 蓝白 绿 棕白 棕

568A 绿白 绿 橙白 蓝 蓝白 橙 棕白 棕

直通线：异类设备互联的线缆 （例如交换机连接PC）

交叉线：同类设备互联的线缆（例如路由器连接PC）

A类设备:3层及三层以下的设备，即物理层和数据链路层设备

B类设备：3层及三层以上的设备，如路由器、PC、服务器

现在端口都有自适应功能，无所谓了。

线缆有如下类型：1类 2类 3类 4类 5类 5E 6 7 8

3类线支持10M/bit的传输（集线器可以使用）

4类线支持16M/bit的传输（集线器可以使用）

5类线支持100M/bit的传输

5E（超5类线）支持1000M/bit的传输

8类线支持10000M/s，韩国10年前已经实现了1000Mbit/s



将双绞线按照其中是否含有屏蔽膜分为：UTP和STP

UTP称为非屏蔽双绞线，最大100米

STP称为屏蔽双绞线，后来STP升级为ScTP，最大25米



100BASE-T：其中T是子路twisted的缩写，搅在一起

PoE:以太网供电，3702不支持PoE。PoE分为两个规则：CIP和



光纤

![image-20210801140628079](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210801140628079.png)

光纤分为两种：

多模光纤：比较粗，62.5us,50us，使用LED发射

单模光纤：很细，9us，支持1000KM，使用激光发射



串行电缆：

![image-20210801141443016](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210801141443016.png)

DCE数字通信端

DTE数字终端端

### 2.数据链路层

最流行的局域网协议：以太网协议（Ethernet）

最流行的广域网协议：点对点协议（PPP）

PPPoE:承载在以太网之上的PPP连接

![image-20210801142601598](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210801142601598.png)



![image-20210801142738709](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210801142738709.png)





![image-20210801143953539](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210801143953539.png)

**1h20min的是开始做实验，但是我的环境没有配置好，因此耽搁了！！**

以下是通过wireshark，做有关mac地址的实验：

![image-20210805154536417](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210805154536417.png)



若不在统一网络的两台主机，mac地址是网关接口的mac地址：

![image-20210805154746267](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210805154746267.png)

## 06:OSI网络层IPv4概述（1h58min）

(Open Standard Interconnection)

TCP/IP之所以称为TCP/IP是因为这两个协议比较典型。

IPv4:是因特网第四代封装协议，与以太网协议（Ethernet协议）类似，不能产生数据，只能帮助上层应用（传输层）封装；定义了封装的报头、传输规则、地址信息等；

在TCP/IP中，一个节点（Node）表示一个接口；但是mac地址只能在一个网络内使用，否则源mac地址是网关的地址 ；secondary是辅助地址

3层4层封装的长度：必须被4字节整除。由于有些选项是可选项，因此封装的长度为20字节到60字节。

![image-20210806151943623](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210806151943623.png)

红色的几种字段：共同完成数据切片。传输层中，将应用程序产生的数据流按照MTU（最大传输单元）的规定切片，切片之后在每个“片”的前面添加一个四层报头形成数据段。但是，网络层也支持分片。

VPN的工作原理（28min:30s）:欺骗路由器

![image-20210806153141242](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210806153141242.png)

![image-20210806153714095](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210806153714095.png)

数据传输的时候要经历4种延迟：

1. 处理延迟
2. 传输延迟
3. 串行化延迟

identification字段的内容，见《计算机网络安全教程》P31

### 1.identification字段：

抖动：由于延迟的原因，传输时间不一致导致数据的分片错误重组（例如X1 X2 Y1 Y2 Y3的重组），因此可以使用标识符identification防止错误**重组**

### 2.Flags地段

共占3个比特，且最高位不使用，中间称为DF位，即Don not fragment，不要分片位；最低位称为MF位，即more fragment，更多分片位；

应用如下：

![image-20210806175341105](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210806175341105.png)

### 3.Fragment offset:分段偏移量

### 4.Time to live（TTL）

自数据包产生到接受经历的最大时间，后来因为估计太过困难，改为了最大经历的路由器的跳数（一台三层网络设备是一跳，例如路由器）。Time to live 共占1Byte，即最大值255。从中国到美国最远的路径，才17~18跳，而比较近的路径才13跳就可以到达

Protocol:类似于数据链路层以太网协议的类型Type字段；告知三层网络设备四层使用的是什么协议。

以下是四层几个经典的协议号：

ICMP 1

IGMP 2

TCP 6

UDP 17

EIGRP 88

OSPF 89

PIM 103

### 5.Header Checksum

三层报头校验和

### IP地址

使用点分十进制表示X.X.X.X，共32bit，即每个字段8bit，0~255。高位称为网络位，低位称为主机位；用来标识广播域的称为网络位，表示广播域中主机的称为主机位；

IP地址的分类

以下是主类分类或者自然类分类，其中A B C 表示**单播**地址，D是**组播**地址，E类地址是被保留地址。

![image-20210806182035701](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210806182035701.png)



![image-20210806185142727](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210806185142727.png)

#### A类：

最左边的地址8个bit是网络位（网络位用来标识广播域），并且最高位是0。且在特殊情况下，网络号全0，即0000 0000 ， 和网络号全1，即0111 1111是不可以使用的，因此共有255-128 -2 =125个可用的数字。（如何计算？？）

![image-20210806182333783](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210806182333783.png)

![image-20210806182632215](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210806182632215.png)

0.0.0.0（即0000 0000.0.0.0）:默认路由或者缺省地址。当此IP地址存在路由表项时，且路由器找不到明确的路由表项的时候，可以使用这条路由作为转发；或者作为“未指定地址”

127.0.0.0（即0111 1111.0.0.0）：称为回环地址（Lookback）。可以通过ping 127.0.0.0（即0111 1111.0.0.0）检查网卡是不是安装正确

主机位：

2^0 - 1  ~~~ 2^(24) - 1，即0 ~~ 1700万，即最多有1700万台主机。而在一个网络中，比如网络号为0010 000.X.X.X这个A类网络中，最多包含300台主机。因此浪费了很多地址。而32位的IP地址只有约42亿个。

若把一个网络号下的1700万个地址用于多个广播域，就会出现：将相同网络位的地址用于不同的广播域！而网络位是用来标识广播域的，无法区分不同的网络，不同广播域主机的IP地址网络位相同了！

如何解决这个问题？

#### 主B类地址

![image-20210806185201864](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210806185201864.png)

第一个字节的最左边2个bit位为10，即范围为1000 0000.X.X.X ~~1111 1111.X.X.X，十进制为128.X.X.X ~~191.X.X.X。前16位为网络位，后16位为主机位。即一个网络号下包含2^16个主机，共65526台主机

#### 主C类地址：

![image-20210806185925924](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210806185925924.png)

第一个字节的最左边3个bit位为110，即范围为1100 0000.X.X.X ~~1101 1111.X.X.X，十进制为192.X.X.X ~~223.X.X.X。前24bit为网络位，后8bit为主机位。即一个网络号下包含2^8个主机，共256台主机

广播域：（1h22min）

![image-20210806191440349](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210806191440349.png)

子网化：被借用过来的网络位称为子网位

![image-20210806191941535](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210806191941535.png)

当前使用的路由器成为“无类路由器”，以前使用有类路由器。FLSM：定长子网掩码；VLSM:不定长子网掩码

子网掩码：

公有地址：

私有地址

主A类中：10.X.X.X这个网段

主B类中：172.16.0.0-----172.31.0.0

主C类中：192.168.0.0----192.168.255.0

由于路由器中没有私有地址的路由表项，因此会丢包。

NAT PAT:地址转换协议

# 第4专题 TCP/UDP以及IOS命令配置详解

## 07：IPv6、TCP与UDP以及路由器硬件架构（1h47min）

本节课涉及到实验

各国运营商的最主要的收入来源：专线和VPN

### IPv6相关内容：

IPv6地址的长度：128bit。其中FEC0:表示长点本地地址，（Site Local），FC00开头

规则：冒号16分进制数。XXXX.XXXX.XXXX.XXXX.XXXX.XXXX.XXXX.XXXX/64：一个X代表十六进制数，即4bit二进制数，即XXXX代表16bit二进制，所以如上有128bit二进制数；其中前64位称为网络位，后64位称为主机位。在IPv6中，主机位称为接口标识符。2001开头的地址：全球可聚合单播地址（AGUA）；FE80开头的地址：链路本地地址（Link Local)

![image-20210808144423107](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210808144423107.png)

IPv4报头长度：20字节~60字节不等（由于可选项、填充两个字段的影响），IPv6报头长度是定长的，为40个字节

![image-20210808144956384](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210808144956384.png)

![image-20210808161436956](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210808161436956.png)

IPv6不建议对数据进行切片，因此没有四种和切片有关的字段，相反的，IPv6提供了ICMPv6控制层协议控制MTU检测（PMTU路径MUT检测）；IPv4是无连接的（发现数据传输丢失不会要求重新传送），因此使用Header checksum，但是IPv6没有。

在IPv4和IPv6的传输层协议中，对应的协议号的值不一定都相同。例如，在两种协议中，EIGRP协议号都是88，OSPF的协议号都是89，而ICMP在IPv4中协议号是1，在IPv6中协议号是58

Flow Label:配合源目地址唯一标识网络中的**“一股流”**（什么意思？？？），且配合Traffic class字段提供更好的服务（Qos）

### 传输层：

传输层属于第四层，第四层的封装有两种协议（封装协议：自身不产生任何数据，只是为高层数据提供数据封装的协议）：TCP和UDP。在TCP/IP协议栈中，将所有的封装协议分为两类：面向连接协议和无连接协议。面向连接表示可靠的，而无连接表示尽力而为，即虽然发送了，但是不一定保证接受了

MSS：最大分片大小（即传输层的MTU）

#### TCP：传输控制协议

![image-20210808162708973](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210808162708973.png)

是一种面向连接的可靠的、点对点协议，报头长度为20~60字节，只能发送单播数据

流控字段：利用窗口（windows）协商一次性最大发送的数据。因此必须建立点到点之间的连接，这种连接称为3次握手连接。即发送之后，等待确认，若收到则再发，否则重新发送；而其他无连接没有这种功能。

序列号字段（Sequence）：保证切片重组的序列性

确认号字段（Acknowledgement,ACK）：防止丢包

校验和字段（Checksum）：防止冲突和篡改

#### UDP:用户数据报协议

![image-20210808161959189](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210808161959189.png)

是一种面向无连接的不可靠协议，报头长度为8字节。“可靠”≠“安全”，早起经常出现针对TCP协议的TCP同步泛洪攻击（TCP SYN Flooding Attack），又叫拒绝服务攻击（Denial of service）。而UDP没有三次握手，因此不需要确认，所以不会有Dos的安全隐患。而基于网络发送的媒体流量（例如视频等），是采用组播或者广播的形式，需要采用UDP。VOIP（Voice over Internet Protocol）：通过网络打电话或者视频。

### IOS命令配置详解（1h17min38s）：

路由器就是专用计算机，它负责连接网络。

主板上内容：电源、CPU、内存（RAM,random access memory）、硬盘（用的不是磁盘式硬盘，用的是固态硬盘SSD，闪存Flash）、只读存储器ROM（烧录一些信息，类似于BIOS，称为ROMMON）、接口interface（数据接口、线路接口）。

当路由器开机的时候，需要loading一些信息，这些信息存放在RAM中，例如IOS（网络操作系统）、运行配置文件（running configuration）。NVRAM：非易可失性随机存储器，（百度百科：*NVRAM*（ Non-Volatile Random Access Memory） 是非易失性随机访问存储器，指断电后仍能保持数据的一种RAM。）启动配置文件：startup configuration，配置寄存器Configure register（默认0x2102）

路由器硬件：

![image-20210808165252038](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210808165252038.png)

![image-20210808164940687](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210808164940687.png)

![image-20210808170455449](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210808170455449.png)



![image-20210808165904671](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210808165904671.png)

## 08:IOS命令行架构以及基础设置（8月5日 , 1h47min）

集中模拟器的介绍：

Packet Tracert （简称PT）模拟器不是太强大，只能应付NA考试

GNS3也是一款模拟器

IOU也是模拟器

IOL

EVE也是模拟器 EVE2.0.3

SecureCRT 

IOS:互联网操作系统的简称

ZTEK利特装换器，需要装驱动。双绞线连接到笔记本的一种转换器品牌。



两种连接路由器的方式：

1. 本地连接通过Console口，但是只有一个Connsole口，一定要保护好。初始配置一定是本地登陆；或者有一个mini usb接口

2. 远程连接通过Telnet终端仿真，但是网管流量是通过明文形式发送的，不安全。因此可以选择SSH（安全外壳协议）

还有几种访问方式：

AUX:辅助端口，前提是先连接一个锚的设备

Management 接口：前提是配置一个IP地址。但是正常的数据流量不会走这个接口，因此可以实现“带外网管”，即网管流量和数据流量分开。



![image-20210805144209409](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210805144209409.png)



### 1.进入网络系统之后的几种工作模式：

#### **第一种：用户模式**

共有16种模式，权限级别依次对应0~16，用户模式权限最低

Hostname 主机名

其中，思科默认路由器主机名是Router，华为默认主机名是Huawei，思科默认交换机主机名是Switch

#### **第二种：特权模式**

使用enable（使能命令，若退回用户模式使用disable命令）之后敲回车：显示#

![image-20210805142024571](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210805142024571.png)

存盘命令：copy run

在配置的命令前面加上no命令：相当于橡皮擦，将配置擦除

copy running-config start-config//表示存盘，将X复制到Y中去

配置系统时间：

![image-20210805142915162](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210805142915162.png)

Tab键：自动补全命令

#### **第三种：全局配置模式**

如何进入全局配置模式？在enable模式下，输入configure terminal命令回车。

![image-20210805143512652](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210805143512652.png)

高级别模式可以运行低级别命令，但是有些需要加do，例如：

![image-20210805144100211](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210805144100211.png)

### 2.常用的配置命令

如何回退：exit或者end（相当于ctrl + z）

![image-20210805144502028](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210805144502028.png)



![image-20210805144542534](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210805144542534.png)

banner:横幅

Message of the Day: 启动时候的显示横幅

![image-20210805144952476](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210805144952476.png)

其中：

![image-20210805145100953](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210805145100953.png)

表示最大空闲会话超时计时器，默认5分钟自动关闭，例子中表示配置为20min30s

建议输入的几条优化命令：

![image-20210805145446802](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210805145446802.png)

关闭自动域名解析：

![image-20210805145512888](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210805145512888.png)

VTP:虚拟逻辑接口

RBAC：基于权限的用户管理

![image-20210805150123330](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210805150123330.png)

![image-20210805150200208](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210805150200208.png)

ethernet0/0的含义：

现在的路由器都是模块化的，0表示第一个模块，0/0表示第一个模块的第一个接口。参考如下：

![image-20210805150837306](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210805150837306.png)

10M以太网接口：ethernet

100M以太网接口：fast ethernet

1000M以太网接口：G/bit ethernet

10000M以太网接口：10 G/bit ethernet，

而在数据中心的交换机中，不管是那种以太网，都是ethernet，串行的都是serial

![image-20210805152102294](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210805152102294.png)

![image-20210805152146759](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210805152146759.png)



使能或者关闭接口：

物理层的状态使用state描述，数据链路层的状态使用line protocol描述

如下：

![image-20210805152457124](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210805152457124.png)



![image-20210805152803301](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210805152803301.png)

![image-20210805152839073](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210805152839073.png)







# 第28节  基础理论：CIDR解决方案解析

## 1.IPv4 地址结构 （30min）

A类地址：前8位是网络位。

127.0.0.1称为环回地址 ping不通说明硬件的驱动是不通的，驱动是没有安装成功的。

B类地址：前16位是网络位，后16位是主机位

最高字节最高两bit横为10,即首字节的取值范围为128~191

C类地址：前24位是网络位，后8为主机位

最高字节的最高三bit恒为110，即192~223

D类地址：组播地址

E类地址

**提出问题？？？？为什么要子网化？？？**

一个网络中尽量不超过300台计算机。

解决方案：

子网化：地址借位技术。被借位的称为子网位，原来是主机位。解决地址冲突和地址浪费的问题。重新定义网络位、主机位。

11.0000 0000.0.0借主机位1位称为网络位，则分成了2个子网

11.1000 0000.0.0 是一个子网：11.128.0.0

11.0000 0000.0.0 是一个子网：11.0.0.0

借位n位，则划分为2^n个子网。

FLSM: 定长子网掩码。只通过一次借位，将一个主类地址段分割为若干个网络位长度相同的子网。

VLSM:不定长子网掩码/可变长可变子网掩码

![image-20210730125742503](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210730125742503.png)



有类路由器 Classfull

不能识别子网位全0、全1的IP地址（如上面的00,11的子网）

无类路由器 Classless



2021.07.30看到这里：

![image-20210730130701700](C:\Users\wzq\AppData\Roaming\Typora\typora-user-images\image-20210730130701700.png)


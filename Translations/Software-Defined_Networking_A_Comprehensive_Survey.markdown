#	Software-Defined Networking: A Comprehensive Survey

Diego Kreutz, Member, IEEE, Fernando M. V. Ramos, Member, IEEE, Paulo Verissimo, Fellow, IEEE,
Christian Esteve Rothenberg, Member, IEEE, Siamak Azodolmolky, Senior Member, IEEE,
and Steve Uhlig, Member, IEEE

##	SOFTWARE-DEFINED NETWORKS: BOTTOM-UP

###	Layer I: Infrastructure

An SDN infrastructure, similarly to a traditional network, is composed of a set of networking equipment (switches, routers and middlebox appliances). The main difference resides in the fact that those traditional physical devices are now simple forwarding elements without embedded control or software to take autonomous decisions. The network intelligence is removed from the data plane devices to a logically-centralized control system, i.e., the network operating system and applications, as shown in Figure 6 (c). More importantly,
these new networks are built (conceptually) on top of open and standard interfaces (e.g., OpenFlow), a crucial approach for ensuring configuration and communication compatibility and interoperability among different data and control plane devices. In other words, these open interfaces enable controller
entities to dynamically program heterogeneous forwarding devices, something difficult in traditional networks, due to the large variety of proprietary and closed interfaces and the distributed nature of the control plane.

与传统网络相似， SDN 基础设施，是包括交换机，路由器和 middlebox 设备在内的一系列网络设备的集合。一个主要的区别在于，传统的物理设备仅仅简单地转发信息而没有嵌入式控制或者软件控制下的自主选择。网络智能被从数据层剥离到一个逻辑中心化的控制系统，如图6所示的网络操作系统与应用。更加重要的是，这些新型网络是建立在开放、标准的接口上（如 OpenFlow），这保证了不同数据层与控制层设备之间配置与通信的兼容性与互操作性。换句话说，这些开放的接口使得控制器实体动态地对多样化的转发设备进行编程提供可能。由于各种专利与封闭的接口以及控制层的分布式 nature ，这在传统网络中恰恰是非常困难的。

In an SDN/OpenFlow architecture, there are two main elements, the controllers and the forwarding devices, as shown in Figure 7. A data plane device is a hardware or software element specialized in packet forwarding, while a controller is a software stack (the “network brain”) running on a commodity
hardware platform. An OpenFlow-enabled forwarding device is based on a pipeline of flow tables where each entry of a flow table has three parts: (1) a matching rule, (2) actions to be executed on matching packets, and (3) counters that keep statistics of matching packets. This high-level and simplified model derived from OpenFlow is currently the most widespread design of SDN data plane devices. Nevertheless, other specifications of SDN-enabled forwarding devices are being pursued, including POF [31], [120] and the Negotiable Datapath Models (NDMs) from the ONF Forwarding Abstractions Working Group (FAWG) [121].

如图7，在 SDN/OpenFlow 架构中，控制器与转发设备是两个主要的组成部分。数据层设备是一种专注于包转发的硬件或软件，而控制器是在日常硬件平台上运行的一个软件栈（网络中枢）。支持 OpenFlow 的转发设备基于流表的管道。流表的每一个入口具有三个部分：(1) 匹配规则，(2) 对匹配包的操作，以及(3) 记录匹配包数据的计数器。由 OpenFlow 派生出来的这种高层与简化的模型被广泛用于 SDN 数据层设备设计。不过依然存在其他形式的支持 SDN 的转发设备，例如 POF [31], [120] 以及 ONF FAWG [121] 的 NDMs。

Inside an OpenFlow device, a path through a sequence of flow tables defines how packets should be handled. When a new packet arrives, the lookup process starts in the first table and ends either with a match in one of the tables of the pipeline or with a miss (when no rule is found for that packet). A flow rule can be defined by combining different matching fields, as illustrated in Figure 7. If there is no default rule, the packet will be discarded. However, the common case is to install a default rule which tells the switch to send the packet to the controller (or to the normal non-OpenFlow pipeline of the
switch). The priority of the rules follows the natural sequence number of the tables and the row order in a flow table. Possible actions include (1) forward the packet to outgoing port(s), (2) encapsulate it and forward it to the controller, (3) drop it, (4) send it to the normal processing pipeline, (5) send it to the next flow table or to special tables, such as group or metering
tables introduced in the latest OpenFlow protocol.

在 OpenFlow 设备中，一系列流表规定了包的处理方式。当有新包到达时，一个查询过程将遍历流表寻找匹配的规则。如图7，这些规则涉及不同的匹配方式。如果没有缺省的规则，未匹配的包将被忽略。不过，普遍的处理方式是创建一个缺省规则以将未匹配的包发送到控制器或者交换机上的普通非 OpenFlow 管道。规则的优先级由流表的序列号和表中各规则的排列顺序确定。可能的处理规则包括：(1) 将包转发到出口，(2) 将其封装并发送给控制器，(3) 丢弃，(4) 发送到普通处理管道，(5) 发送给下一个流表或者特表例如最新的 OpenFlow 协议规定的组或者 metering 表。

As detailed in Table III, each version of the OpenFlow specification introduced new match fields including Ethernet, IPv4/v6, MPLS, TCP/UDP, etc. However, only a subset of those matching fields are mandatory to be compliant to a given protocol version. Similarly, many actions and port types are optional features. Flow match rules can be based on almost arbitrary combinations of bits of the different packet headers using bit masks for each field. Adding new matching fields has been eased with the extensibility capabilities introduced in OpenFlow version 1.2 through an OpenFlow Extensible
Match (OXM) based on type-length-value (TLV) structures. To improve the overall protocol extensibility, with OpenFlow version 1.4 TLV structures have been also added to ports, tables, and queues in replacement of the hard-coded counterparts of earlier protocol versions.

如表3所示，OpenFlow 的各版本引入了包括以太网， IPv4/v6，MPLS，TCP/UDP 等许多新的匹配方式。然而，只有一部分匹配方式被这些版本要求强制支持。相似地，许多行为与端口类型是可选特性。使用各自的位掩码，流匹配规则几乎可以基于何种包头中任意位的组合。基于 TLV 结构，OpenFlow v1.2 提供的 OXM 支持可扩展的匹配方式，这缓解了 OpenFlow 加入新的匹配方式的进程。为了提高协议的扩展能力，端口、流表、队列将早起版本中硬编码的匹配方式替换为 OpenFlow v1.4 TLV 结构。

*Overview of available OpenFlow devices*

Several OpenFlow-enabled forwarding devices are available on the market, both as commercial and open source products (see Table IV). There are many off-the-shelf, ready to deploy, OpenFlow switches and routers, among other appliances. Most of the switches available on the market have relatively small Ternary Content-Addressable Memory (TCAMs), with up to 8K entries. Nonetheless, this is changing at a fast pace. Some of the latest devices released in the market go far beyond that figure. Gigabit Ethernet (GbE) switches for common business purposes are already supporting up to 32K L2+L3 or 64K L2/L3 exact match flows [122]. Enterprise class 10GbE switches are being delivered with more than 80K Layer 2 flow entries [123]. Other switching devices using high performance chips (e.g., EZchip NP-4) provide optimized TCAM memory that supports from 125K up to 1000K flow table entries [124]. This is a clear sign that the size of the flow tables is growing at a pace aiming to meet the needs of future SDN deployments. 

由表3可见，市场上有多种或商用、或开源的支持 OpenFlow 的转发设备。在这些设备中，不少 OpenFlow 交换机与路由器现货供应，随时可以部署。市场上大多数的交换机具有可达 8K 的相对小的 TCAMs。然而，这种局面正在迅速改变。市场上最新的设备已经远远超出了这些参数。普通商用的 GbE 交换机已经支持了高达 32K L2+L3 或 64K L2/L3 的精确匹配流 [122]。企业级的 10GbE 交换机可以提供超过 80K L2 流入口 [123]。使用EZchip NP-4 等高性能芯片的其他交换机提供优化的 TCAM 支持 125K 到 1000K 的流表入口 [124]。这说明流表的大小将能满足未来的 SDN 部署需求。

Networking hardware manufacturers have produced various kinds of OpenFlow-enabled devices, as is shown in Table IV. These devices range from equipment for small businesses (e.g., GbE switches) to high-class data center equipment (e.g., high-density switch chassis with up to 100GbE connectivity for edge-to-core applications, with tens of Tbps of switching capacity).

由表4可见，网络硬件制造商已经生产了多种型号的支持 OpenFlow 的设备。这些设备覆盖了小公司需要的 GbE 交换机到高级数据中心部署高密度交换机架以及具有 100GbE 连通性与 10Tbps 级别交换容量的 edge-to-core 应用。

Software switches are emerging as one of the most promising solutions for data centers and virtualized network infrastructures [147], [148], [149]. Examples of software-based OpenFlow switch implementations include Switch Light [145], ofsoftswitch13 [141], Open vSwitch [142], OpenFlow Reference [143], Pica8 [150], Pantou [146], and XorPlus [46]. Recent reports show that the number of virtual access ports is already larger than physical access ports on data centers [149]. Network virtualization has been one of the drivers behind this
trend. Software switches such as Open vSwitch have been used for moving network functions to the edge (with the core performing traditional IP forwarding), thus enabling network virtualization [112].

An interesting observation is the number of small, startup enterprises devoted to SDN, such as Big Switch, Pica8, Cyan, Plexxi, and NoviFlow. This seems to imply that SDN is springing a more competitive and open networking market, one
of its original goals. Other effects of this openness triggered by SDN include the emergence of so-called “bare metal switches” or “whitebox switches”, where the software and hardware are sold separately and the end-user is free to load an operating system of its choice [151].

###	Layer II: Southbound Interfaces
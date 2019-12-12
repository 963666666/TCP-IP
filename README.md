# -
TCP/IP
======
OSI分层，已经各个层之间的协议
------
	*应用层
	邮件点击发送就进入了应用层，应用层还包括接收方无法接受这类问题的处理（邮件发送，文件传输，远程连接）
	*表示层
	数据格式的转换，按照规定格式的编码转化成相应的数据
	*会话层
	决定以某种方式连接（传输五封邮件，可以建立五次连接发送，可以建立一次连接发送，同时建立五次连接一起发送）
	*传输层
	建立连接或断开连接的处理，主机之间创建逻辑上的通信连接，确认数据包传输，没有传输成功，进行重发
	*网络层
	网络节点的管理和选择
	*数据链路层
	通过传输介质互联的设备之间进行数据处理 （介质访问控制层和逻辑链路控制层）
	*物理层
	将包含MAC地址信息的首部附加到网络层转发过来的数据上，将其发送到网络

面向有连接和面向无连接
------

电路交换和分组交换
------
	*电路交换
	独占网络
	*分组交换
	将要发送的数据分成多个数据包，按照一定的数据分别发送，提高通信线路的利用率
根据接收端数量分类
------
	*单播
	*广播
	*多播
	*任播
地址的层次性
------
	*MAX地址 没有层次性
	*IP地址 有层次性
	
TCP/IP
======
网络层
------
IP协议
------
	*不具备重发机制，属于非可靠性协议
ICMP协议
------
	*数据包在发送过程中发生异常导致无法发送到对端，发送端发送一个异常的通知
ARP协议
------
	*将IP地址解析成物理地址（mac地址）
	
传输层
------
TCP协议（传输层）
------
	*一种面向有连接的传输层协议，能够正确处理传输过程中丢包、传输数据错乱等异常情况，  
	*此外TCP还能有效利用带宽，缓解网络拥堵（不适合做视频会议，音频，视频的数据量既定）
UDP协议（传输层）
------
	*一种面向无连接的传输层协议，不能确定对端是否接受到数据包，需要对端的应用程序实现（视频会议）
应用层
------
HTTP协议
------
HTML（表示层的协议）
------
文件传输（FTP）
------
	*进行文件传输时会建立两个TCP连接（发出请求时所要用到的控制连接与实际传输数据时所要用到的数据连接）
远程登录（SSH，TELNET）
------
以太网帧体格式
------
	*比特 二进制中最小的单位，每个比特的值要么是0，要么是1
	*字节 通常8个比特构成一个字节
	*8位字节 8个比特也被称为8个字节
	*目标mac地址      源mac地址      类型（2字节）      数据（46-1500个字节）      FCS（4字节）
	*FCS检测帧是否有所损坏
LCP与NCP
------
	*再开始传输数据之前要先建立PPP级的连接，PPP的功能主要包括两个协议，一个是不依赖上层的LCP协议，另一个是依赖上层的NCP协议
	*LCP主要负责建立和断开连接，设置最大连接数，设置验证协议以及设置是否进行通信质量的检测
	
IP协议
======
IP寻址，路由，IP分包与组包
------
	*多条路由是指路由器或主机在转发IP数据包时只指定下一个路由器或者主机，而不是将到最终目标地址为止的所有通路都指定出来  
	*为将数据包发送给目标主机，所有主机都维护这一张路由控制表  
IP多播
------
	*多播用于将包发送给特定组内的所有主机，1对N，N对N通信的需求明显上升，具体实现采用复制1对1通信的数据（路由器负责复制）
	IP多播与地址
	------
	*多播使用D类地址，从首位开始到第四位是“1110”， 从224.0.0.0到239.255.255.255都是多播地址的可用范围
	*IP地址  
	172     .20      .100     .52  
	10101100 00010100 01100100 00110100  
	*子网掩码
	255     .255     .255     .192
	11111111 11111111 11111111 11000000
	*网络地址
	172     .20      .100     .0
	10101100 00010100 01100100 00000000
	*多播地址
	172     .20      .100     .63
	10101100 00010100 01100100 00111111
	
路由控制
------
    *IP本身没有定义制作路由控制表的协议，该表是由一个叫做“路由协议”的协议制作而成的  
    *路由控制表中记录了网络地址和下一步应该发送至路由器的地址。
    *如果路由表中下一个路由器的位置记录着某个主机或路由器的网卡的IP地址，那就意味着“发送的目标地址属于同一个链路  
    
IP报文的分片与重组
------
    *只能有目标主机进行分片之后的IP数据报文的重组

IPv4首部
------
    *版本       由4比特构成，表示标识IP首部的版本号
    *首部长度   由4比特构成，表示IP首部的长度，单位为4字节
    *区分服务   由8比特构成，用来表明服务质量
    *总长度     表示IP首部与数据部分合起来的总字节数，长16比特
    *标识       由16比特构成，用于分片重组（即使ID相同，如果目标地址、源地址或协议不同的话，也被认为是不同的分片）
    *标志       由3比特构成，表示包被分片的相关信息
    *片偏移     由13比特构成，用来标识被分片的每一分段相对于原始数据的位置
    *生存时间    由8比特构成，指可以中转多少个路由器
    *协议       由8比特构成，表示IP首部的下一个首部隶属于哪个协议
    *首部校验和  由16比特构成，该字段只校验数据报的首部，不校验数据部分。
    *源地址
    *目标地址
    *可选项
    *填充
    *数据
IPv6首部格式
------
    *版本
    *通信量类
    *流标号      由20比特构成，准备用于服务质量控制
    *有效载荷长度 是指包的数据部分
    *下一个首部   相当于IPv4的协议字段
	*跳数限制     与IPv4的生存时间意思相同
	*源地址
	*目标地址
IP协议相关技术
======
ICMP
------
    *确认IP包是否成功送达目标地址
    *通知在发送过程中当中IP包被废弃的具体原因
    *改善网络设置

NAT的工作机制
------
    *在发送包的时候，NAT路由器将发送源的地址从10.0.0.10转换为全局IP地址（202.244.174.37），在发送数据  
    *当包从地址163.221.120.9发过来的时候。目标地址（202.244.174.37）先被转换成私有IP地址10.0.0.10以后再被转发  
    
    
    *即使在一个没有NAT的环境里，根据所制作的应用，用户完全可以忽略NAT的存在而进行通信。  
    在NAT的内侧（私有IP地址的一边）主机上运行的应用为了生成NAT转换表，需要先发送一个  
    虚拟的网络包给NAT外侧。而NAT不知道这个虚拟包究竟是什么，还是会照样读取包首部中的  
    内容并自动生成一个转换表，如果转换表结构合理，NAT外侧的主机与内侧的主机之间也能够  
    进行相互通信
    
IP隧道
------
    *网络层首部的后面继续追加网络层首部的通信方法叫“IP隧道”
IP多播相关技术
------
    *IGMP 主要有两大作用
    *1. 向路由器表明想要接收多播消息（并通知想接收多播的地址）
    *2. 向交换集线器通知想要接收多播的地址
    
    *由于从IGMP（MLD）包中可获知多播发送的地址和端口，从而不会再向毫无关系的端口发送多播帧
IP任播
------
    *IP任播是指为那些提供同一种服务的服务器配置同一个IP地址，并与最近的服务器通信的一种方法
控制通信质量的机制
------
    DiffServ
    *在DiffServ域中的路由器会对所有进入该域IP包首部中的DSCP字段进行替换。对于期望被优先处理的包  
    设置一个优先值，对于没有这种期望的包设置无需优先值。在发生网络拥塞时还可以丢弃优先级低的包。
显示拥塞通知
------
    *ECN的机制概括起来就是在发送IP首部中记录路由器是否遇到拥塞，并且在返回包的TCP首部中通知是否  
    发生过拥塞
    *拥塞检查在网络层中进行，而拥塞通知在传输层中进行
    
    
    
TCP与UDP
======
TCP
------
    *TCP为提供可靠性传输，实行“顺序控制”或“重发控制”机制。此外还具备“流控制”、“拥塞控制”、提高网络 
    利用率等众多功能
    
    *TCP通过校验和、序列号、确认应答、重发控制、连接控制以及窗口控制等机制实现可靠性传输。  
    *确认应答处理、重发控制以及重复控制等功能都可以通过确认序列号实现。  
    *序列号是按顺序给发送数据的每一个字节（8位字节）都标上号码的编号。接收端查询接收数据TCP首部中的  
    序列号和首部的长度，将自己下一步应该接收的序号作为确认应答反送回去。  
    *面向有连接是指在数据通信开始之前先做好通信两端之间的准备工作。  
    *利用窗口控制提高速度，TCP以1个段为单位。发送端主机在发送了一个段以后不必要一直等待确认应答。  
    而是继续发送，窗口大小为4个段
    *流控制 为了防止接收端在高负载的情况下无法接受数据包，TCP提供一种机制可以让发送端根据接收端的实  
    接收能力控制发送的数据。 发送端主机会根据接收端主机的指示，对发送数据的量进行控制。  
    *拥塞控制 在发送数据包时，将拥塞窗口的大小与接收端主机通知的窗口大小作比较，然后按照他们当中较小  
    的那个值，发送比其还要小的数据量。  
    *TCP文件传输中，绝大多数是每两个数据段返回一次应答。
    
    首部格式
    *源端口号
    *目标端口号
    *序列号  字段长32位，序列号是指发送数据的位置。没发送一次数据吗，就累加一次该数据字节数的大小
    *确认应答号  字段长度32位。是指下一次应该受到的数据的序列号
    *数据偏移  表示TCP所传输的数据部分应该从TCP包的哪个位开始计算。如果该字段的值为5，那说明从TCP  
    包的最一开始到20字节位置都是TCP首部，余下的部分为TCP数据。
    *保留  
    *控制位  
    *窗口大小  该字段长为16位，用于通知从相同TCP首部的确认应答号所指位置开始能够接收的数据大小。
    *校验和  
    *紧急指针  该字段长为16位。
    *选项
    
    *窗口大小与吞吐量
    TCP通信的最大吞吐量由窗口大小和往返时间决定。假定最大吞吐量为T，窗口大小为W，往返时间是RTW的话，  
    那么最大吞吐量的公式  T=W/RTW
    
    
    
UDP
------
    *在UPD的情况下，虽然可以确保发送消息的大小，却不能保证消息一定会到达。  
    *在多播与广播通信中也是用UDP而不是TCP。
    
    *经常用于以下几个方面
    包总量较少的通信
    视频、音频等多媒体通信（即时通信）
    限定于LAN等特定网络中的应用通信
    广播通信（广播、多播）
    
    
    首部格式
    *源端口号
    *目标端口号
    *包长度
    *校验和  
    
套接字
------
    *应用程序利用套接字，可以设置对端的IP地址、端口号，并实现数据的发送与接收
	
	*TCP/IP或者UDP/IP通信中通常采用5个信息来识别一个通信。“源IP地址”、“目标IP地址”、“协议号”、  
	“目标端口号”。只要其中一项不同，则被认为是其他通信
	
	
如果需要应用自己处理一些更为细节上的控制，使用UDP协议是不错的选择。如果转发数据量较多，  
、对可靠性要求比较高时，可以选择使用TCP。  

SCTP
------
    *与TCP一样，都是一种提供数据到达与否相关可靠性检查的传输协议。其主要特点：
        *以消息为单位发送
        TCP中接收端并不知道发送端应用所决定的消息大小，在SCTP中可以。
        *支持多重宿主
        再有多个NIC的主机中，即使其中能够使用的NIC发生变化，也仍然可以继续通信。
        *支持多数据流通信
        TCP中建立多个连接以后才能通信的效果，在SCTP中一个连接就可以。
        *可定义消息的生存期限
        超过生存期限的消息不会被重发。
DCCP
------
    *与UDP一样不能提供发送数据的可靠性。
    *面向连接，具备建立连接与断开连接的处理。在建立和断开连接上是具备可靠性的。  
    *能够根据网络拥堵情况，进行拥塞控制。  
    *为了进行拥塞控制，接收端收到包以后返回确认应答（ACK）。该确认应答被用于重发与否的判断。  
	
	
路由协议
======
动态路由的基础
------
    *会给相邻路由器发送自己已知的网络连接信息，而这些信息就像接力一样依次传递给其他路由，直至整个网络  
    都了解时，路由控制表就制作完成了。
    
路由算法
------
    *距离向量算法
    *链路状态算法  从网络代理获取路由信息表。
    
广播路由控制信息
------
    *RIP将路由控制信息定期（30秒一次）向全网广播。
    *RIP2
        使用多播
        支持子网掩码
        路由选择域
        外部路由标志
        身份验证秘钥  只有在自己能够识别这个密码时才接收数据，否则忽略这个RIP包
    *RIP是选择路由个数最少的路径，而OSPF是选择总的代价较小的路径。
    *OSPF为了减少计算负荷，引入了区域的概念。内部路由器只了解区域内部的链路状态信息，并在该信息的 
    基础上计算出路由控制表。
    
    *BGP  需要放眼整个互联网进行路由控制。
    *BGP中数据包送到目标网络时，会生成一个中途经过所有AS的编号列表。这个表格也叫做AS路径信息访问  
    列表。如果针对同一个目标地址出现多条路径时，BGP会从AS路径信息访问列表中选择一个较短的路由。
    
    *MPLS  对每个IP包都设定一个叫做“标记”的值，然后根据这个“标记”在进行转发。
    *MPLS的优点
    一个是转发速度快
    利用标记生成虚拟的路径，在上面实现IP数据包的通信。
    
    
应用协议
======
远程登录
------
    *TELNET
    *SSH
    *文件传输
        FTP  使用两条TCP连接：一条用来控制，另一条用于数据（文件）的传输
            *用于控制的TCP连接主要在FTP的控制部分使用。例如登录用户名和密码的验证、发送文件的名称、
            发送方式的设置。在这个连接上无法发送数据，数据需要一个专门的TCP进行连接。  
            *FTP控制用的连接使用的是TCP21端口，在TCP21号端口上进行文件GET、PUT、以及文件一览等操作  
            时，每次都会建立一个用于数据传输的TCP连接。当数据传送完毕之后，传输数据的这条连接也会被
            断开，然后会在控制用的连接上继续进行命令或应答的处理。
            *通常，用于数据传输的TCP连接是按照与控制用的连接相反的方向建立的。因此，在通过NAT连接  
            外部FTP服务器的时候，无法直接建立传输数据时使用的TCP连接。此时，必须使用PASV命令修改建
            立连接的方向。
            
        
    
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
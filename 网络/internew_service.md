
## OSI 7 model
> Open Systems Interconnection model 

Application (layer 7)
Presentation (layer 6)
Session (layer 5)
Transport (layer 4) — Gateway, the up layer from here, deal with high layer protocols  
Network (layer 3)  —Router , change to different sub network 
Data Link (layer 2)  — Bridge & Switch , change to different 网段
Physical (layer 1)  —— 中继器 （Repeater, just make it can be transferred farer）

---

## IP (Internet Protocols)
> main: TCP/IP protocols 

[image:FB9067C9-CE2D-4D8F-B5F7-0D98249D7319-356-00001BBC734C8F70/417323E6-16F8-43E9-979B-063DB67F7CC5.png]

* IP地址
A、B、C、D、E有五类地址
[网络地址][子网地址][主机地址]

ABC 点对点通信
D 组播地址 multicast, broadcast 
	* （网络中必须有组播路由器，能识别组播地址）
	* 主机要能发送组播（IP软件+网络接口软件）

* 主要操作 
	* 数据包生存期
		* 经过一个路由器+1， 防止无休止巡回
	* 分段和重装配
	* 差错控制和流控 
		* 丢弃一个数据报时，尽可能向源点返回一些信息，源点可相应更改发送策略等
		* 出错原因：超过生存期、网络拥塞、FCS校验出错

* IP协议数据报头
[image:8FEBF8AB-C29B-49D2-8766-B8110FFB14D5-356-00001D1252EC8D09/386A6622-4BC6-4BAE-A6AC-B4D61B386137.png]

* ICMP

> Internet Control Message Protocol 与IP同属网络层
用于传输有关通信问题的消息，例如数据报不能到达目的站、路由器没有足够的缓存空间等 
封装在IP数据报中发送

* 传输层协议： TCP／UDP
	* TCP 
	可分段传送，对字节流进行传送，所以一定要按字节量标志发送／接受顺序位。有可能分段发送位为20, 40, 60,接受为60 表明都接收到了
[image:238078B2-C731-415E-81FB-A0526BA8E593-356-00001D6B50540966/F50746C9-5445-44CC-8A4D-8BBA50CC6B63.png]
       三次握手
	            1. 发送方同步请求：SYN，发送顺序X
	            2. 接收方同步确认并请求：SYN+ACK，接收顺序号X+1， 发送顺序位Y
	            3. 发送方同步确认：ACK，应答顺序号为Y+1
	            4. 握手完成，连接就正式建立了 
	
	此外，URG标志表示紧急数据
	TCP+IP报头20字节
	  


												MQTT

MQTT（Message Queuing Telemetry Transport，消息队列遥测传输协议），是一种基于发布/订阅（publish/subscribe）模式的"轻量级"通讯协议，该协议构建于TCP/IP协议上，由IBM在1999年发布。MQTT最大优点在于，可以以极少的代码和有限的带宽，为连接远程设备提供实时可靠的消息服务。作为一种低开销、低带宽占用的即时通讯协议，使其在物联网、小型设备、移动应用等方面有较广泛的应用。

MQTT是一个基于客户端-服务器的消息发布/订阅传输协议。MQTT协议是轻量、简单、开放和易于实现的，这些特点使它适用范围非常广泛。在很多情况下，包括受限的环境中，如：机器与机器（M2M）通信和物联网（IoT）。其在，通过卫星链路通信传感器、偶尔拨号的医疗设备、智能家居、及一些小型化设备中已广泛使用。


要想指定某一个设备收到此条消息，那么就必须根据topic主题来识别

ClientID
客户端唯一标识，服务端用于关联一个Session。只能包含这些 大写字母，小写字母 和 数字（0-9a-zA-Z），23个字符以内，同一时间内 Server 和同一个 ClientID 只能保持一个 TCP 连接，再次连接会踢掉前一个连接的客户端。
Keep Alive
顾名思义，目的是保持长连接的可靠性，以及双方对彼此是否在线的确认。客户端在Connect的时候设置 Keep Alive 时长。如果服务端在 1.5 * KeepAlive 时间内没有收到客户端的报文，它必须断开客户端的网络连接。
Will
遗嘱，遗愿；遗嘱消息（Will Message）存储在服务端，当网络连接关闭时，服务端必须发布这个遗嘱消息，所以被形象地称之为遗嘱，可用于通知异常断线。
retain
0： 服务端不能存储这个消息，也不能移除或替换任何 现存的保留消息 。
1： 服务端必须存储这个应用消息和它的QoS等级，以便它可以被分发给未来的订阅者，所以如果后面未来有客户端订阅了这个主题，那么这个客户端一上线就会收到此消息。
qos
0： 【最多一次】 没有回复，不需要存储。有可能丢失（网络异常断开，业务层繁忙或者错误） 。
1： 【至少一次】确保消息到达，但消息重复可能会发生。
2： 【只有一次】确保消息到达一次；
poyload
用来传输用户的数据，最大允许 256MB ，发布的消息的 Payload允许为空。在很多场合下，代表将持久消息（或者遗嘱消息）清空；格式为UTF-8编码；




由于物联网的环境是非常特别的，所以MQTT遵循以下设计原则：

（1）精简，不添加可有可无的功能；
（2）发布/订阅（Pub/Sub）模式，方便消息在传感器之间传递；
（3）允许用户动态创建主题，零运维成本；
（4）把传输量降到最低以提高传输效率；
（5）把低带宽、高延迟、不稳定的网络等因素考虑在内；
（6）支持连续的会话控制；
（7）理解客户端计算能力可能很低；
（8）提供服务质量管理；
（9）假设数据不可知，不强求传输数据的类型与格式，保持灵活性。



MQTT协议实现方式
实现MQTT协议需要客户端和服务器端通讯完成，在通讯过程中，MQTT协议中有三种身份：发布者（Publish）、代理（Broker）（服务器）、订阅者（Subscribe）。其中，消息的发布者和订阅者都是客户端，消息代理是服务器，消息发布者可以同时是订阅者。

MQTT传输的消息分为：主题（Topic）和负载（payload）两部分：

（1）Topic，可以理解为消息的类型，订阅者订阅（Subscribe）后，就会收到该主题的消息内容（payload）；
（2）payload，可以理解为消息的内容，是指订阅者具体要使用的内容。

网络传输与应用消息
MQTT会构建底层网络传输：它将建立客户端到服务器的连接，提供两者之间的一个有序的、无损的、基于字节流的双向传输。

当应用数据通过MQTT网络发送时，MQTT会把与之相关的服务质量（QoS）和主题名（Topic）相关连。



MQTT客户端
一个使用MQTT协议的应用程序或者设备，它总是建立到服务器的网络连接。客户端可以：

（1）发布其他客户端可能会订阅的信息；
（2）订阅其它客户端发布的消息；
（3）退订或删除应用程序的消息；
（4）断开与服务器连接。

MQTT服务器
MQTT服务器以称为"消息代理"（Broker），可以是一个应用程序或一台设备。它是位于消息发布者和订阅者之间，它可以：

（1）接受来自客户的网络连接；
（2）接受客户发布的应用信息；
（3）处理来自客户端的订阅和退订请求；
（4）向订阅的客户转发应用程序消息。




https://blog.csdn.net/xh870189248/article/details/81181707		//mqtt介绍




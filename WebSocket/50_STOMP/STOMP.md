
消息格式——让客户端和服务器相互可以理解的格式。这种格式可以自定义，或特定于框架，或使用标准的消息传递协议。

Spring框架提供了对使用STOMP子协议的支持。
STOMP，Streaming Text Orientated Message Protocol，流文本定向消息协议。STOMP是一个简单的消息传递协议， 是一种为MOM（Message Oriented Middleware，面向消息的中间件）设计的简单文本协议。
STOMP提供了一个可互操作的连接格式，允许STOMP客户端与任意STOMP消息代理（Broker）进行交互，类似于OpenWire协议（一种二进制协议）。






# 一、STOMP协议介绍

  STOMP即Simple (or Streaming) Text Orientated Messaging Protocol，简单(流)文本定向消息协议，它提供了一个可互操作的连接格式，允许STOMP客户端与任意STOMP消息代理（Broker）进行交互。STOMP协议由于设计简单，易于开发客户端，因此在多种语言和多种平台上得到广泛地应用。
  
  STOMP协议的前身是TTMP协议（一个简单的基于文本的协议），专为消息中间件设计。
  
  STOMP是一个非常简单和容易实现的协议，其设计灵感源自于HTTP的简单性。尽管STOMP协议在服务器端的实现可能有一定的难度，但客户端的实现却很容易。例如，可以使用Telnet登录到任何的STOMP代理，并与STOMP代理进行交互。

# STOMP协议分析

STOMP协议与HTTP协议很相似，它基于TCP协议，使用了以下命令：

CONNECT
SEND
SUBSCRIBE
UNSUBSCRIBE
BEGIN
COMMIT
ABORT
ACK
NACK
DISCONNECT

STOMP的客户端和服务器之间的通信是通过“帧”（Frame）实现的，每个帧由多“行”（Line）组成。
第一行包含了命令，然后紧跟键值对形式的Header内容。
第二行必须是空行。
第三行开始就是Body内容，末尾都以空字符结尾。
STOMP的客户端和服务器之间的通信是通过MESSAGE帧、RECEIPT帧或ERROR帧实现的，它们的格式相似。


# 二、STOMP的实现
业界已经有很多优秀的STOMP的服务器/客户端的开源实现，下面就介绍一下这方面的情况。

RabbitMQ	1.0 1.1 1.2	基于Erlang、支持多种协议的消息Broker，通过插件支持STOMP协议 http://www.rabbitmq.com/plugins.html#rabbitmq-stomp
Stampy	1.2	STOMP 1.2规范的一个Java实现 

Gozirra	1.0	Java客户端库 http://www.germane-software.com/software/Java/Gozirra/
libstomp	1.0	C客户端库，基于APR库 http://stomp.codehaus.org/C
Stampy	1.2	Java客户端库 http://mrstampy.github.com/Stampy/
stomp.js	1.0 1.1	JavaScript客户端库 http://jmesnil.net/stomp-websocket/doc/




# 参考

http://blog.csdn.net/chszs/article/details/46592777
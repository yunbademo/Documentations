# 云巴的发布/订阅模式
##利用云巴为全球的设备提供订阅、发布以及推送消息等服务。
云巴利用订阅/发布模式进行实时数据流和设备信号，使得您在极短的时间内建立并且维护接口连接到任何一个全球的任何一个设备上，将信息推送给用户。

通过云巴，主动、及时地向您的用户发起交互，向其推送聊天消息、日程提醒、活动预告、进度提示、动态更新等。精准的目标用户和有价值的推送内容可以提升用户忠诚度，提高留存率与收入。

>* 强大的实时沟通功能 
>* 可扩展的语言架构--- **Erlang**
>* 稳定的框架和协议---**MQTT**

##**理论基础**

发布/订阅模式，又称为观察者模式，定义对象间的一种一对多的依赖关系，一个发布者可以对应多个订阅者。当发布者发生变化的时候，他可以将消息一一通知给所有的订阅者，即:当一个对象的状态发生改变时，所有依赖于它的对象都得到通知并被自动更新。
总的来说，发布/订阅消息模型基本是一个基于推送的模型，其中消息自动地向消费者广播。
而对于订阅者而言，有两种不同类型的订阅者。
1 非持久订阅者：只有在主动侦听主题时才接收消息
2 持久订阅者：订阅者将接收到每条消息的副本以便在“离线状态”下接收推送的消息。
![Yunba发布/订阅模式][1]

 1. 这种模式不同于传统的点对点模式，发布/订阅模式由于采用了广播技术，发布到一个主题的信息，可以由多个订阅者所接收。
 2. 广泛应用的物联网协议MQTT也是基于发布/消息模式，提供一对多的消息发布。该协议支持所有平台，几乎可以把所有联网物品和外部连接起来，成为目前主流的物联网协议。
 
云巴作为实时发布订阅系统，选择了MQTT协议。其优点包括：非常精简的二进制，适合做大量的节点弱、网络差的场景；天然的发布订阅场景；开源的协议和方便的扩展。
同时，该协议的固定长度的头部字节很小，利于小型传输，做到交换最小化，降低网络流量的同时也减少了很大的开销。

```seq 
Title: MQTT协议示例
发布者->代理: 发布消息 
代理->订阅者: 推送消息
订阅者->代理: 订阅消息
```
![MQTT协议示例][2]
3. 在这种机制下，多个发布应用和多个订阅应用通过建立在代理服务器中的特定主题作为中介互相通信。发布者与订阅者不需要通过TCP建立直接的通信连接。

 云巴就是基于这种消息模式并结合运用MQTT协议以及Socket.IO技术为企业与用户之间提供发布/订阅服务。


----------


##**应用实例**

以著名的iReader(掌悦)为例，应用云巴提供的服务后，相当于在用户与客户端之间架起了一座桥梁。例如，用户订阅了iReader历史类型的书籍的服务，所以每当有新的历史类书籍上架，通过云巴，iReader 都可以在第一时间将该类书籍的信息推送给订阅该类的所有用户，而对于那些“离线用户”，消息也会在用户上线后立即推送，以便用户及时阅读书籍。



  [1]: https://cloud.githubusercontent.com/assets/12043658/7466369/3762def8-f314-11e4-86d0-f75947d95d21.png
  [2]: https://cloud.githubusercontent.com/assets/12043658/7466383/60a0aa02-f314-11e4-9744-4065c86dd30d.png
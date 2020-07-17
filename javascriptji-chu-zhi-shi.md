+ TCP(Transmission Control Protocol传输控制协议)三次握手
    - 位码即tcp标志位，有6中标识：   
        SYN(synchronous建立联机)、ACK(acknowledgement确认)、
        PSH(push传送)、FIN(finish结束)、RST(reset重置)、URG(urgent紧急)、   
        Sequence number(顺序号码)、Acknowledge number(确认号码)
        
    ```text
    第一次握手：主机A发送位码为syn=1,随机产生seq number=1234567的数据包到服务器。主机B由syn=1,知道A要求建立连接；
    第二次握手：主机B确认联机信息，向A发送ack number=(主机A的seq number+1),syn=1,ack=1,随机产生seq number=7654321的包；
    第三次握手：主机A收到后检查ack number是否正确，即第一次发送的seq number+1,以及位码ack是否为1。  
              若正确，主机A会再发送ack number=(主机B的seq number+1),ack=1。
              主机B收到后确认seq number的值与ack=1则连接建立成功
    ```
    
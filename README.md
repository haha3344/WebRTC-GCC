### 缩写
- RTT - round trip time
- SR - sender report
- RR - receive report
- REMB - Receiver Estimated Maximum Bitrate

### 概述
* Loss-based controller:发送端，根据丢包率、RTT和REMB，计算出一个目标发送码率
* delay-based controller:接收端，根据收到包的信息，或是SR包的信息，计算出一个最大码率REMB，传回给发送端

### 实现
以上两种controller共同工作，实现了拥塞控制算法
#### 都工作在发送端
- WebRTC目前采用该方法，两张算法分别计算目标码率，然后取最小值
- Delay-based control:A_hat
- Loss-based controller:As_hat
#### 都工作在接收端

#### Delay-based control
- a pre-filtering
- an arrival-time filter
- an over-use detector
- a rate controller

#### Loss-based controller
- 从RR中获取丢包率
- 根据如下公式计算

$$\[{As\text{ \_ }hat \left( i \left) ={ \left\{ \begin{array}{*{20}{l}}
{As\text{ \_ }hat \left( i-1 \left) ,\text{ }\text{ }2\text{%} < p < 10\text{%}\right. \right. }\\
{As\text{ \_ }hat \left( i-1 \left) * \left( 1-0.5p \left) ,\text{ }\text{ }10\text{%} < p\right. \right. \right. \right. }\\
{1.05*As\text{ \_ }hat \left( i-1 \left) ,\text{ }\text{ }p < 2\text{%}\right. \right. }
\end{array}\right. }\right. \right. }\]$$
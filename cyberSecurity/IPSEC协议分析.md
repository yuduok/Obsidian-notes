#### 工作原理

IPSec的工作原理类似于包过滤防火墙，可以把它看做是包过滤防火墙的一种扩展

a) 流量触发

- 当有IP数据包需要发送时，系统会检查是否需要应用IPSec策略。
- 这通常基于预配置的IPSec策略，如特定的源/目标IP地址或端口。

b) 策略查找

- 系统查询安全策略数据库（**SPD**）。
- SPD定义了哪些流量应该被保护，以及如何保护。（对接收到的IP数据包进行转发、丢弃或IPSec处理）

c) 安全关联（SA）协商

- 如果需要IPSec保护且没有现存的SA，则启动IKE（Internet Key Exchange）过程。
- IKE协商分为两个阶段：
    - 第一阶段：建立安全的通信通道（ISAKMP SA）
    - 第二阶段：协商特定的IPSec SA

IKE第一阶段（主模式）：

1. 提议和接受加密/认证算法
2. Diffie-Hellman密钥交换
3. 身份验证（预共享密钥或证书）

IKE第二阶段（快速模式）：

1. 协商IPSec SA参数
2. 生成密钥材料
3. 建立IPSec SA

d) 数据处理

- 基于协商的SA，对数据进行处理：
    - 使用AH：计算并添加认证头
    - 使用ESP：加密数据并添加ESP头尾

处理步骤（以ESP为例）：

1. 生成IV（初始化向量）
2. 加密IP数据包载荷
3. 计算并添加完整性校验值（ICV）
4. 封装ESP头和尾

e) 传输

- 处理后的数据包通过网络发送到目的地

#### IPSec工作模式

IPsec使用认证头标（**AH**）和封装安全净载（**ESP**）两种安全协议来提供安全通信

a) 传输模式（用在主机到主机的通信）
- 仅加密/认证IP数据包的载荷
- 原始IP头保持不变

b) 隧道模式（用在其他任何方式的通信）
- 加密整个原始IP数据包
- 添加新的IP头

#### 主要协议

1. AH（认证头）协议

	特点：
	- 提供数据完整性和源认证
	- 不提供数据加密
	- 使用HMAC算法进行数据认证
	
	**数据包结构**：
	- 下一头
	- 载荷长度
	- 保留字段
	- 安全参数索引（SPI）
	- 序列号
	- 认证数据

2. ESP（封装安全载荷）协议

	也有两种工作模式：
	- **传输模式**
	- **隧道模式**
	
	功能：
	- 提供数据加密
	- 提供数据完整性
	- 提供源认证
	
	**数据包结构**：
	- SPI（安全参数索引）
	- 序列号
	- 加密载荷
	- 完整性校验值（ICV）

3. IKE（密钥交换）协议

	主要阶段：
	- 第一阶段：建立安全信道
	- 第二阶段：协商安全关联（SA）
	
	密钥交换特点：
	- 使用 Diffie-Hellman 密钥交换
	- 支持**证书**和**预共享密钥**认证
	- 周期性重新协商密钥

4. 安全关联（SA）

	定义：
	- **单向**逻辑连接（所以在进行双向安全通信时，需要两个SA，SA（out）、SA（in））
	- 定义安全参数
	- 包含加密算法、密钥等信息
	
	SA 管理：
	- 手动配置
	- 自动协商（IKE）

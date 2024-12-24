
TLS记录协议位于传输层与应用层之间

TLS握手协议、TLS密钥交换协议和TLS报警协议均与HTTP和FTP一样属于应用层协议

#### TLS记录协议

1. 基本功能
	- 负责数据的**加密、压缩和完整性保护**
	- 将上层协议（如 HTTP）的数据进行封装和保护
	- 确保数据在传输过程中的机密性和完整性

2. **记录协议工作流程**
	- **数据分片**：将上层协议的数据分割成多个记录
	- **数据压缩**（可选）
	- **数据加密**
	- 添加消息认证码（**MAC**）以保证完整性

3. 加密过程
	- 使用协商好的对称加密算法（如 AES）
	- 使用会话密钥进行加密
	- 生成消息认证码（MAC）

#### TLS密钥交换协议

TLS 密钥交换协议用于在客户端和服务器之间安全地协商和建立共享的会话密钥，更新用于当前连接的密码组

#### TLS告警协议

TLS 告警协议（Alert Protocol）用于传递错误和状态信息

告警类型分为两大类：
- 致命告警（**Fatal** Alerts）：导致连接立即终止
- 警告告警（**Warning** Alerts）：不一定终止连接，通常只是记录日志

#### TLS握手协议

使得服务器和客户端能够相互鉴别对方，协商具体的**加密算法**和**MAC算法**以及**保密密钥**。

1. 握手协议的主要目标
	- 协商 TLS **版本**
	- 选择**加密算法**（密码套件）
	- **验证**服务器身份（可选验证客户端）
	- **建立会话密钥**

2. 基本握手流程（TLS 1.2）

```plaintext
客户端                                               服务器
ClientHello            -------->
                                          ServerHello
                                         Certificate*
                                   ServerKeyExchange*
                                  CertificateRequest*
                      <--------      ServerHelloDone
Certificate*
ClientKeyExchange
CertificateVerify*
ChangeCipherSpec
Finished              -------->
                                   ChangeCipherSpec
                      <--------           Finished
应用数据              <------->         应用数据
```

3. **详细握手步骤**

	A. 第一阶段：建立连接
		ClientHello：
		  - 支持的 TLS 版本
		  - 客户端随机数
		  - 支持的密码套件
		  - 压缩方法
		
		ServerHello：
		  - 选择的 TLS 版本
		  - 服务器随机数
		  - 选择的密码套件
		  - 选择的压缩方法
	
	B. 第二阶段：服务器认证
		- 服务器发送证书链
		- 可选的 ServerKeyExchange
		- 可选的客户端证书请求
		- ServerHelloDone 标志
	
	C. 第三阶段：密钥交换
		- 客户端验证服务器证书
		- 发送 ClientKeyExchange
		- 生成预主密钥（Pre-Master Secret）
	
	D. 第四阶段：完成握手
		- 双方计算主密钥和会话密钥
		- 发送 ChangeCipherSpec
		- 发送 Finished 消息

4. TLS 1.3 改进
	- 减少握手往返次数（1-RTT）
	- 支持 0-RTT 恢复会话
	- 移除了不安全的加密算法
	- 简化了密码套件


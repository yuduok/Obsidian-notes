## 企业网远程接入
### 企业网

SDH：同步数字体系（广域网），是一种重要的数字传输技术标准。网络中所有节点共用同一个时钟源。

特点
- 企业拥有企业网全部资源（包括SDH），是专用网络
- 公共通信服务商提供SDH点对点物理链路
- 企业网封闭，外人难以嗅探/截获

缺点
- 成本高
- 难度大
- 不容易扩展，LAN变动要调整SDH
- 灵活性差，SDH带宽难以调整

### 远程接入

如出差员工接入内部网络的过程，路由器完成**对远程用户的身份鉴别过程，为远程终端分配内部网络IP地址**，并建立路由项

特点
- 可以随时随地连接到公共交换电话网（PSTN）
- 可以按需建立与路由器之间的语音信道

缺点
- 成本高
- 间歇性和突发性决定了语音信道的利用率不高
- 数据传输速率受限

## VPN

Virtual Private Network虚拟专网

指通过一个公用网络（通常是因特网）建立一个临时、安全的隧道，是一条穿过公用网络的安全稳定的隧道，是对企业内部网的扩展

#### 功能

- 加密数据
- 信息认证和身份认证
- 访问控制（不同用户不同权限）

#### 特点

- 费用低
- 安全保障
- 服务质量保障
- 可扩充性和灵活性
- 可管理性

#### 关键技术

- 隧道技术
- 加解密技术
- 密钥管理技术
- 身份认证技术
- 访问控制

#### 隧道协议与VPN

在隧道中，数据包被重新封装发送

- 链路层中的隧道协议：PPTP、L2TP、L2F等；主要用于构建远程访问VPN
- 网络层中的隧道协议：IPSec、GRE（通用路由封装）等；主要用于构建LAN-TO-LAN型VPN

**封装**：在原IP分组添加新的标头（源地址C、目的地址D）再删除旧的标头（源地址A、目的地址B）；最终封装成**以隧道两端的全球IP地址为源和目的IP地址的IP分组格式**

**发送**：
- 发端VPN在对IP数据包前加新报头封装后，将封装后的数据包通过Internet发送给收端VPN
- 收端VPN在接收到封装数据包后，将隧道标头删除再发送给目标主机

### VPN分类

#### 第三层（网络）隧道VPN

   - 用于实现企业局域网之间以私有IP为源和目的IP地址的IP分组传输
   - IP分组需要封装成**以隧道两端的全球IP地址为源和目的IP地址的IP分组格式**
   - 需要完成隧道两端的**双向身份认证**和IP分组的**保密性和完整性**

经过隧道传输时，IP分组封装成GRE格式

IPSec和安全传输过程：
1. 建立安全传输通道（完成双向身份认证和协商加密算法、报文摘要算法以及密钥生成机制）
2. 建立安全关联（约定安全协议即ESP或AH）
3. 最后通过定义IP分组类型确定经过安全关联传输的IP分组

#### 第二层（链路）隧道和IPSec

   - 实现PPP（点对点协议）帧传输
   - IP分组需要封装成**以隧道两端的全球IP地址为源和目的IP地址的IP分组格式**
   - 需要完成隧道两端的**双向身份认证**和IP分组的**保密性和完整性**

路由器为了实现远程终端VPN接入过程，需要在注册用户库中配置注册用户名、口令和鉴别机制。为了给远程终端分配用于访问内部网络的本地IP地址，需要给路由器定义本地IP地址池

PPTP（Point to Point Tunnel Protocol）
- 让远程用户拨号连接到本地ISP，访问本地网络

L2F（Layer 2 Forwarding）
- 可以在多种介质上建立**多协议**的安全虚拟专用网
- 将链路层的协议封装起来传送

L2TP（Layer 2 Tunneling Protocol）
- 结合了PPTP和L2F
- 适合组建远程接入方式VPN

缺陷：
- VPN对远程终端的访问权限没有限制
- 远程终端要安装**专用客户端**
- **内部网络对于远程终端都不是透明的**
- **无法实现基于用户授权**

#### TLS/SSL VPN

传输层安全协议VPN

   - 核心设备是**SSL VPN网关**，SSL VPN网关一端连接互联网，另一端连接内部网络
   - **远程终端分配全球IP地址**，通过互联网访问SSL VPN网关
   - 远程终端通过基于SSL协议的HTTPS访问SSL VPN网关
   - 通过SSL VPN网关实现双向身份鉴别
   - SSL VPN网关作为**中继设备**，负责消息转发

最大优点：用户**不需要安装和配置客户端软件**，只需要安装一个浏览器，且TLS协议允许使用数字签名和证书，可以提供强大的认证功能

TLS VPN的实现方式：**在企业的防火墙后面放置一个TLS代理服务器**

连接过程：
1. 首先在浏览器输入一个URL
2. 该连接请求被TLS代理服务器取得
3. 用户通过身份认证
4. TLS代理服务器提供用户与各种不同应用服务器之间的连接
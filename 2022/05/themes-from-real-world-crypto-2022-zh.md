# 来自 Real World Crypto 2022 的主题

上周，来自世界各地的 500 多名密码学家齐聚阿姆斯特丹，参加 Real World Crypto 2022，这是两年多来的第一次面对面会议。

与往年一样，我们派遣了一些研究人员和工程师参加会议，听取演讲并闲聊观察目前主导密码学研究和实际（现实世界！）工程之间关系的主题。

以下是我们从 Real World Crypto 2022 中收集到的主要主题：

1. **可信硬件并不那么可信**：可信硬件的实施者（无论是可信执行环境 (TEE)、HSM 还是安全飞地）继续犯下从根本上违反硬件完整性承诺的工程错误。
2. **安全工具仍然太难使用**：或者“你可以把马牵到水边，但你不能让它运行./configure && make && make install。”
3. **无处不在的侧信道**：当上帝关上一扇门时，他打开了一个侧信道。
4. **加密上下文中的 LANGSEC**：弄清楚你在说哪个协议是计算机科学中的第三个难题。

让我们开始吧！

## 受信任的硬件并不那么值得信赖

可信硬件中的基本非加密漏洞并不是什么新鲜事。多年的漏洞导致英特尔决定从其下一代消费类 CPU 中[删除 SGX](https://www.bleepingcomputer.com/news/security/new-intel-chips-wont-play-blu-ray-disks-due-to-sgx-deprecation/)，而 [ROCA](https://www.cve.org/CVERecord?id=CVE-2017-15361) 在 2017 年影响了[四分之一的 TPM](https://www.theregister.com/2017/10/16/roca_crypto_vuln_infineon_chips/)。

*新的趋势*是可信硬件在*面向消费者的角色*中的流行。普通用户越来越多地（并且在不知不觉中！）在他们的手机和计算机上通过密码管理器和 WebAuthn 等 2FA 方案与安全飞地和 TEE 进行交互。这从根本上扩大了与受信任硬件漏洞相关的风险：受信任硬件的破坏现在对个人用户构成*直接风险*。

这就是 RWC 2022 中的第一个亮点：“**信任在黑暗中消亡：揭示三星的 TrustZone 加密设计**”（[幻灯片](https://iacr.org/submit/files/slides/2022/rwc/rwc2022/58/slides.pdf)、视频、[论文](https://eprint.iacr.org/2022/208.pdf)）。在本次会议中，演讲者描述了 [TEEGRIS](https://developer.samsung.com/teegris/overview.html) （即三星的 TrustZone 操作系统）的两个关键弱点：**IV 重用攻击**，允许攻击者提取受硬件保护的密钥，以及**降级攻击**，即使是最新的和修补过的三星旗舰设备也容易受到攻击到第一种攻击。我们将看看两者。

### TEEGRIS 中的 IV 重用

TEEGRIS 是一个完全独立的操作系统，与“普通”主机操作系统 (Android) 独立运行并并行运行。为了与主机通信，TEEGRIS 提供了一个可信应用程序 (TA)，它在 TEE 内运行，但通过 [Keymaster](https://source.android.com/security/keystore/implementer-ref)（一种由 Google 标准化的命令和响应协议）向普通主机公开资源。

Keymaster 包含“blob”的概念：加密密钥本身已使用 TEE 的密钥材料加密（“包装”）并存储在主机操作系统上。由于打包后的密钥存储在主机上，因此其安全性最终取决于 TEE 在密钥打包期间正确应用加密的安全性。

那么 TEEGRIS Keymaster 是如何包装密钥的呢？使用 AES-GCM！

您会记得，分组密码 (AES) 与操作模式 (GCM) 相结合（通常）有三个参数：

* *密钥*，用于初始化分组密码
* *初始化向量 (IV)*，用于扰乱密文并防止 [ECB 企鹅](https://words.filippo.io/the-ecb-penguin/)（注：密码学的一个著名的隐喻，意即使用ECB方式加密的企鹅图片还能够看出是企鹅）
* 我们打算加密的*明文本身*（在这种情况下，另一个加密密钥）

AES-GCM 的安全性取决于假设 IV 永远不会被重复用于相同的密钥。因此，可以强制在多个“会话”（在本例中为密钥包装）使用密钥和 IV 的攻击者可能会违反 AES-GCM 的安全性。演示者发现三星 Keymaster 实现中的错误违反了两个安全假设：密钥派生函数 (KDF) 不能被操纵以多次生成相同的密钥，以及攻击者无法控制 IV。就是这样：

* 在 Galaxy S8 和 S9 上，用于生成密钥的 KDF 仅使用**攻击者控制的输入**。换句话说，攻击者可以强制给定 Android 应用程序的所有加密 blob 使用**完全相同的 AES 密钥**。在这种情况下，只要攻击者不能强制 IV 重用，这是可以接受的，除非……
* …Android 应用程序可以在生成或导入密钥时设置 IV！三星在 Galaxy S9 上的 Keymaster 实施信任主机传入的 IV，允许攻击者多次使用同一个 IV。

此时，流密码本身的属性为攻击者提供了从另一个 blob 恢复加密密钥所需的一切：恶意 blob、恶意密钥和目标（受害者） blob 的 XOR目标，这是解包的加密密钥！

最终，演示者确定这种特殊攻击仅在 Galaxy S9 上有效：S8 的 Keymaster TA 从攻击者控制的输入生成密钥，但不使用攻击者提供的 IV，从而防止 IV 重用。

该演讲的主持人在 2021 年 3 月报告了此错误，并分配了 [CVE-2021-25444](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-25444)。


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


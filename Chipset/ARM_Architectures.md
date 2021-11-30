ARM Architectures

| 功能                             | 架构版本                  | 描述                                                         | 备注                                                         |
| -------------------------------- | ------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| AArch64                          | 8.0-A, 9.0-A              | 64-bit执行环境                                               | [64位](https://developer.arm.com/architectures/learn-the-architecture/a-profile) |
| AArch32                          | 8.0-A, 9.0-A（仅支持EL0） | （与v7-A兼容）                                               | [32位](https://developer.arm.com/architectures/learn-the-architecture/a-profile) |
| 虚拟化                           | 8.0-A, 9.0-A              | 支持Hypervisor和虚拟化                                       | [Virtualization](https://developer.arm.com/documentation/102142/latest) |
| TrustZone                        | 8.0-A, 9.0-A              | CPU中的硬件隔离区                                            | [TrustZone](https://developer.arm.com/documentation/102418/latest/) |
| Realm Management Extension (RME) | v9-A                      | Realm Management Extension (RME) 建立在 TrustZone 之上，具有以下功能：<br>1. 两个额外的安全状态；<br>2. 两个额外的物理地址空间；<br/>3. 在安全状态之间动态移动资源的能力。<br/>这些功能支持 Arm 机密计算架构 (Arm CCA) 和动态 TrustZone。 | [Arm 机密计算架构](https://developer.arm.com/architectures/architecture-security-features/confidential-computing) |
| 硬件加速的密码算法               | v8.0-8.2-A, 9.0-A         | 相对于软件加密性能3到10倍的提升。                            | [AArch64指令集架构](https://developer.arm.com/documentation/102374/latest/) |
|                                  |                           |                                                              |                                                              |


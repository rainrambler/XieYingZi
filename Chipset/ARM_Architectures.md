ARM Architectures

| 功能                                                | 架构版本                  | 描述                                                         | 备注                                                         |
| --------------------------------------------------- | ------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| AArch64                                             | 8.0-A, 9.0-A              | 64-bit执行环境                                               | [64位](https://developer.arm.com/architectures/learn-the-architecture/a-profile) |
| AArch32                                             | 8.0-A, 9.0-A（仅支持EL0） | （与v7-A兼容）                                               | [32位](https://developer.arm.com/architectures/learn-the-architecture/a-profile) |
| 虚拟化                                              | 8.0-A, 9.0-A              | 支持Hypervisor和虚拟化                                       | [Virtualization](https://developer.arm.com/documentation/102142/latest) |
| **TrustZone**                                       | 8.0-A, 9.0-A              | CPU中的硬件隔离区                                            | [TrustZone](https://developer.arm.com/documentation/102418/latest/) |
| Realm Management Extension (RME)                    | v9-A                      | Realm Management Extension (RME) 建立在 TrustZone 之上，具有以下功能：<br>1. 两个额外的安全状态；<br>2. 两个额外的物理地址空间；<br/>3. 在安全状态之间动态移动资源的能力。<br/>这些功能支持 Arm 机密计算架构 (Arm CCA) 和动态 TrustZone。 | [Arm 机密计算架构](https://developer.arm.com/architectures/architecture-security-features/confidential-computing) |
| **硬件加速的密码算法**                              | v8.0-8.2-A, 9.0-A         | 相对于软件加密性能3到10倍的提升。                            | [AArch64指令集架构](https://developer.arm.com/documentation/102374/latest/) |
| Neon                                                | 8.0-A, 9.0-A              | 一种封装的SIMD架构                                           | [Neon](https://developer.arm.com/architectures/instruction-sets/simd-isas/neon/neon-programmers-guide-for-armv8-a) |
| 虚拟化主机扩展(VHE)                                 | 8.1-A, 9.0-A              | 提升2型Hypervisor的性能。                                    |                                                              |
| **Privilege Access Never (PAN)**                    | 8.1-A, 9.0-A              | PAN 允许内核阻止访问非特权位置，从而提供更高的健壮性。       | [AArch64内存模型](https://developer.arm.com/documentation/102376/latest/Permissions-attributes) |
| Statistical Profiling Extension (统计分析扩展，SPE) | 8.2-A, 9.0-A              |                                                              | [统计分析扩展](https://community.arm.com/developer/ip-products/processors/b/processors-ip-blog/posts/statistical-profiling-extension-for-armv8-a) |
| Scalable Vector Extensions (SVE)可缩放向量扩展      | Armv8.2-A                 | SIMD可变向量长度                                             | [SVE](https://developer.arm.com/documentation/dai0548/latest) |
| **指针验证**（Pointer authentication）              | 8.3-A, 9.0-A              | 将寄存器的内容用作间接分支或数据引用的地址之前对其进行身份验证。抵御ROP和JOP攻击。 | [代码重用攻击](https://community.arm.com/developer/tools-software/tools/b/tools-software-ides-blog/posts/code-reuse-attacks-the-compiler-story) |
| 嵌套虚拟化                                          | 8.3-A, 8.4-A, 9.0-A       |                                                              | [AArch64虚拟化](https://developer.arm.com/documentation/102142/latest) |
| **内存标记扩展**（Memory Tagging Extension，MTE）   | 8.5-A, 9.0-A              | 识别程序中的内存安全违规。                                   | [从架构增强内存安全](https://community.arm.com/developer/ip-products/processors/b/processors-ip-blog/posts/enhancing-memory-safety) <br>[MTE白皮书](https://developer.arm.com/-/media/Arm%20Developer%20Community/PDF/Arm_Memory_Tagging_Extension_Whitepaper.pdf?revision=3cf83df4-b695-43fa-b254-a88133c2126b&hash=A4CBFF993EA90FD081B275CF31A3325A) |
| **分支目标标识**(Branch Target Identification, BTI) | 8.5-A, 9.0-A              | 识别非直接分支的有效目标。是对**指针验证**的补充。增加对JOP的防御。 | [代码重用攻击](https://community.arm.com/developer/tools-software/tools/b/tools-software-ides-blog/posts/code-reuse-attacks-the-compiler-story) |
| GEneral Matrix Multiply (GEMM)                      | 8.6-A, 9.1-A              | 增强SIMD和SVE指令                                            |                                                              |
| BFloat16                                            | 8.6-A, 9.1-A              | 增强SIMD和SVE指令支持BFloat16类型                            |                                                              |
| 高精度计时器                                        | 8.6-A, 9.1-A              | 1GHz高精度计时器                                             | [ARM 8.5-A架构开发2018](https://community.arm.com/developer/ip-products/processors/b/processors-ip-blog/posts/arm-a-profile-architecture-2018-developments-armv85a) |
| 64-byte存取                                         | 8.7-A, 9.2-A              | 使用 64 字节原子加载或存储访问的加速器。                     | [ARM A系列架构开发2020](https://community.arm.com/developer/ip-products/processors/b/processors-ip-blog/posts/arm-a-profile-architecture-developments-2020) |
| SVE2指令集                                          | 9.0-A                     | 可缩放向量扩展的超集。                                       | [ARM A系列架构开发2020](https://community.arm.com/developer/ip-products/processors/b/processors-ip-blog/posts/arm-a-profile-architecture-developments-2020) |
| 事务内存扩展(Transactional Memory Extension, TME)   | 9.0-A                     | 硬件事务内存 (HTM) 支持。 事务内存用于解决编写高并发、多线程程序的困难，通过减少由于锁争用导致的序列化，粗粒度、线程级并行的数量可以随着 CPU 的数量更好地扩展。 | [A系列架构的新技术](https://community.arm.com/developer/ip-products/processors/b/processors-ip-blog/posts/new-technologies-for-the-arm-a-profile-architecture) |
| 分支记录缓存扩展(BRBE)                              | 9.2-A                     | 用于调试和热点分析。                                         |                                                              |

Ref:

[A-Profile Architectures](https://developer.arm.com/architectures/cpu-architecture/a-profile#mte)


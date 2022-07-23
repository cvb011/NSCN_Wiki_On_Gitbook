---
description: Tweaks and tricks to improve both your experience in hosting and others' in playing on your server
---

# 最佳实践


TODO: 如果您有什么与架设北极星服务器有关的经验想要分享的话，请提交 [pull request](https://github.com/R2Northstar/NorthstarWiki/pulls).


## 最低系统要求

在目前的阶段下，架设一个北极星服务器所需的最低配置如下:

**在宿主机上运行服务器的要求:**

- 5GB 的空闲磁盘空间 (如果您使用的是 Window 操作系统，由于origin和运行库的存在，需 +3 GB)
- 3+ CPU线程 ( 尽管双核 **可能** 可以运行 )
- 6GB+ 总可用运行内存 (RAM 或 swap 均可)
- Windows 8.1 ( 并使用内置的 WARP [添加 `-softwared3d11` 参数] 或一张亮机卡) 
- Linux 下需设置 wine 6.0.0+ ( 需要 dxvk+lavapipe+x11, wined3d+llvmpipe+x11, 或者一张亮机卡用于设置 dxvk 或 llvmpipe) (在 [这里](https://github.com/pg9182/northstar-dedicated) 查看更多)

**对于每一服务器实例:**

- 2GB RAM (此为真实的使用量; 但在一段时间后可以降至 ~1.2GB)
- 15 Mbps 上行带宽, 10 Mbps 或许也是可行的, 25 Mbps 则可以避免在大量玩家回到大厅/新的一局游戏开始时出现连接断开

**Note:** 目前任建议将您的服务器规格堆至最低要求之上. 目前的在线服务器数量已经覆盖了每日活跃的玩家甚至是峰值时期的玩家量. 如果您打算自行搭建一个服务器来为这整个玩家群体做贡献的话，由于上述原因，我们建议您的服务器可以填补空缺 ( 例如某种常年满员的模式的服务器 ) 或者提供比现存服务器更好的条件 (更低的延迟, 更高的稳定性, etc.).

## 可选的命令 (Optional)

| Command                          | Description                                                                                                                    |
| -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| `net_compresspackets 1`          | 启用数据包压缩                                                                                                        |
| `net_compresspackets_minsize 64` | 将20人PVP模式的所需带宽由 ~12-16 mbps 降低至 ~6-8 mbps 或者将12人军备竞赛模式的所需带块由 ~9-12mbps 降低至 ~5-7 mbps   |
| `sv_maxrate 127000`              | 设置服务器每秒允许的最大上 (下) 载带宽量  (以 bytes 的形式)                                        |

**Note:** 命令的效果取决于您的操作系统类型, 系统性能, etc. 因此，您应该逐条尝试上述指令以查看您的服务器能否从中受益.

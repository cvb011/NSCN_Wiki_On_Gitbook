# 在 Linux 上搭建服务器

该页面目前的状态是 **work-in-progress**.

Linux 用户可以通过使用 Docker 或者 Wine 来搭建服务器.
如果您的系统中没有支持 DirectX 11 的 GPU ( 比如云服务器场景 ), 你可能会需要搭建一个 **Headless server.**

# <a name="Headless_Servers">Headless Servers</a>

## Using Docker
目前可使用的 Docker 镜像有如下两个:
- [pg9182/northstar_dedicated](https://github.com/pg9182/northstar-dedicated) : 提供服务器管理工具与更好性能的高级服务器 Docker 镜像 *(推荐)*
- [legonzaur/northstar-server-headless](https://github.com/Legonzaur/northstar-server-headless) : 无管理工具的基础镜像

更详细的镜像使用方法请在这些项目的 `README` 中查找

## 不使用Docker

> 我们并不推荐直接在 Linux 系统上搭建服务器, 因为您需要构筑自己的镜像.

您可以在这个仓库中找到使用 Wine 搭建服务器的介绍 [pg9182's repository.](https://github.com/pg9182/northstar-dedicated#running-with-wine)

这一个[ GitHub comment ](https://github.com/R2Northstar/Northstar/issues/49#issuecomment-1001094694) 也提到到了在Linux上搭建服务器的少许信息

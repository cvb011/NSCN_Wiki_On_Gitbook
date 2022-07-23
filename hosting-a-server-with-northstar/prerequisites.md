# 准备阶段

**TL;DR:** 需要转发的端口是 `37015` (UDP) 与 `8081` (TCP)

确保您已正确安装了 Northstar [as described here（尚未翻译）](../installing-northstar/basic-setup.md).

## 敬告：

**搭建您自己的服务器需要相当量的网络基础知识!\
您所需要的知识包括但不限于 **`端口转发` `光猫桥接`** 等. 即使是在云服务器上搭建也相当棘手.\
在您没有足够知识的前提下，我们建议您游玩由他人提供的服务器**

## 检查您是否有转发对应端口的条件

由于其他想要加入您的游戏的人必须能直接连接到您的电脑. 在绝大多数情况下您的路由器是工作在 NAT 模式中的，所以您所需要的步骤是转发对应的端口，具体可以参考 [这篇](https://www.asus.com/support/FAQ/114093/) 来自华硕的文章.

## 运营商级NAT

由于我们无法确认您是否在 [运营商级NAT](https://en.wikipedia.org/wiki/Carrier-grade\_NAT) 的高墙后 （即所谓的没有公网IP）， 因为这通常情况下意味着您 [完全无法搭建服务器](https://en.wikipedia.org/wiki/Carrier-grade_NAT#Disadvantages).

验证您是否有公网IP的方式十分简单：

 * 在百度搜索 `IP` 以获知您的出口IP
 * 将此IP与您路由器获取到的IP进行对比

如果二者不同（大概率是的），那么您是无公网IP的用户，您可以尝试去找运营商去要（移动大概率是要不到的），否则您是无法成功搭建服务器的。

## 端口转发

通过网页控制界面访问您的路由器并转到端口转发子菜单中

* `37015` (UDP) 用于处理游戏逻辑
* `8081` (TCP) 用于与主服务器验证以在主服务器中显示您的服务器

本地IP地址为您跑着服务器的那台pc的IP地址.

## 防火墙

您需要在防火墙中允许 `NorthstarLauncher.exe` 连接到互联网. 在默认情况下，系统应该会在您第一次运行时弹出窗口，记得允许.

如果您不小心点了拒绝（取消）按钮，那么手动设置的过程如下.

* 打开 `Windows Defender 防火墙`
* 选择 `允许应用或功能通过 Windows Defender 防火墙`
* 点击允许其他应用
* 点击浏览
* 定位到 NorthstarLauncher.exe 选择它
* 单击添加

## 最终检查

如果您想要检查设置是否正确，随便开启一个 Notrhstar 的服务器. 其他的 Northstar 用户应该可以在服务器浏览器中发现并加入您的服务器.\
您也可以使用网页端的 [服务器浏览器](https://www.wolf109909.top/tf2/) 去查找您的服务器.

您还可以使用 [第三方网站](https://www.ipfingerprints.com/portscan.php) 来确认您的TCP端口 (通常为 `8081`) 是否正常 来确认您的服务器是否已经启动.

![Example check](https://raw.githubusercontent.com/R2Northstar/NorthstarWiki/main/docs/images/portforwarding-testing.png)

![Working portforwarding for the TCP port](https://raw.githubusercontent.com/R2Northstar/NorthstarWiki/main/docs/images/portforwarding-working.png)

这样的测试只适用于 TCP 端口 因为 UDP 与 Northstar 的工作方式与之不同.

注意在默认状态下，您的服务器名字为 `Unnamed Northstar Server`. 请注意去更改他.

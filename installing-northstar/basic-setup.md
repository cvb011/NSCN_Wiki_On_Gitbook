# 基本安装设置

## 安装 Northstar

请记住， Northstar 客户端仅在 PC 端可用 **并且需要您同时拥有并安装游戏，游戏路径中 `不能` 有中文**.

1. 在 [releases](https://github.com/R2Northstar/Northstar/releases) 页面下载最新版本的北极星
2. 将zip压缩包的所有文件拷贝至 `Titanfall2` 文件夹中. 其位置会因你的下载平台与自定义设置而有所区别.
   * **For Steam** - 右键单击 _Titanfall 2_ > _属性_ > _本地文件_ > _浏览_\
     其默认位置为: `C:\Program Files (x86)\Steam\steamapps\common\Titanfall2`
   * **For Origin** - 遵循以下方法以找到游戏的安装目录 _Origin_ -> _應用程式設置_ -> _安裝與儲存_ -> _在你的電腦上_ -> _游戲庫位置_\
     使用资源管理器定位至上述文件夹中的 `Titanfall2` 子文件夹.\
     其默认位置为: `C:\Program Files (x86)\Origin Games\Titanfall2`
   * **For EA App** - 遵循以下方法以找到游戏的安装目录 _Settings_ -> _Download_\
     Go to the directory under "Install location" using File Explorer and open the `Titanfall2` folder.\
     其默认位置为: `C:\Program Files\EA Games\Titanfall2`
3. 使用 `NorthstarLauncher.exe` 以启动 Northstar
   * 在第一次启动，我们将会询问您是否同意与主服务器进行验证. 如果您希望在Northstar服务器中游玩，单击 _Yes_ (在这之后该选项可以在 Mod 菜单中更改)\
     ![Authentication Agreement](../Doc/images/titleagreement.png)
4. 选择 _启动 Northstar_\
   ![Launch Northstar](../Doc/images/titlelaunchnorthstar.png)
5. 在多人游戏菜单中，您可以在服务器浏览器中加入由社区玩家主持的服务器.\
   ![Server Browser](../Doc/images/lobbyserverbrowser.png)

如果您在游玩过程中遇到了任何的 issues/warnings/errors , 请优先查看 [troubleshooting](troubleshooting.md) 页面.

## 更新 Northstar

更新北极星的过程十分简单 —— 您只需重复安装过程即可. 在复制过程中记得选择 "_替换_".\
注意，如果您更改了类似 `ns_startup_args.txt` 的文件, 这些文件也同样会被替换. 如果您想保留这些设置，记得备份此类文件.

## 除此之外

由于北极星的启动不直接依赖于 steam/origin. 您可能会需要将自定义启动项添加至 `ns_startup_args.txt`, 该文件位于TTF2根目录中.

如果北极星似乎没有正确安装, 或者您在进入大厅时遇到问题, 尝试运行一遍原版游戏. 我们无法保证魔改后的 VPK 是否会与 Northstar 产生冲突, 所以避免此类问题的最好办法就是不要魔改.

## Linux

Linux 下的安装请参考 [这里](playing-on-linux.md).

## SteamDeck

蒸汽甲板的安装请参考 [这里](playing-on-linux.md#steamdeck).

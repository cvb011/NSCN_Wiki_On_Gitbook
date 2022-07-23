<!--
 * @Author: HK560
 * @Date: 2021-12-27 18:29:16
 * @LastEditTime: 2021-12-28 23:44:24
 * @LastEditors: HK560
 * @Description:
 * @FilePath: \NorthStarCN_WIKI\Doc\howToPackMod.md
-->
# 创造你的第一个mod

## 基础
<!-- When creating a mod with Northstar the most basic things to start off with are a workspace with:
 1. A file called `mod.json`
 2. and a folder named `mod` -->

当想要创建一个NorthStar能使用的Mod时候，你需要先给你的mod工程文件夹创建一些东西：
1. 一个叫`mod.json`的文件
2. 一个名为`mod`的文件夹

你在`mod`文件夹中存放的文件将会直接读被引擎的虚拟文件系统读取。如果你弄过vpk的mod大概就明白了，这是类似的。
<!-- The files you put inside the `mod` folder are loaded directly into the virtual file system of the engine (similar to how VPK modding is if you've done that). -->

如果在这个文件夹添加游戏已经存在的文件的话，将会覆写掉原本存在的同名文件。

举个例子，如果你现在mod文件夹路径下有如下文件`My.Mod/mod/resource/coolfile.png`,那么将会覆写任何读取`resource/coolfile.png`的文件。

可以给mod文件添加 par scripts ，不过需要在`mod.json`里面定义，已经存在的scripts不需要定义。

<!-- Adding pre-existing files here will overwrite any previous你 ones with the same name, such as `My.Mod/mod/resource/coolfile.png` would overwrite any file loaded `resource/coolfile.png`. New files can be added par scripts which require being defined in `mod.json`. Existing scripts do not need to be defined. -->

Mods可以通过读取优先级(priority)来覆写其他mods。优先级`0`为开始读取的第一个，然后数字增大就按着数字顺序读取。比如，`MyCoolAwesomeSwag.Mod`设置的优先级是`0`,那么会被第一个读取，然后`MyTerribleAwful.Creation`优先级设置的是`1`,那么它会被第二个读取。

<!-- Mods can also overwrite files of other mods using a load priority. Priority starts at 0 for first loaded and each increment is loaded after. For example: MyCoolAwesomeSwag.Mod has a load priority of 0, which is loaded first, whilst MyTerribleAwful.Creation with a priority of 1 is loaded second. -->

## 编写 mod.json

```json
{
  "Name": "Example.Mod",
  "Description": "Woo yeah wooo!",

  "LoadPriority": 0,
  "ConVars": [],
  "Scripts": [],
  "Localisation": []
}
```

上面提供了样例来给你使用

快速总结一下上面用到所有的参数：
  - `"Name"`: Mod会在菜单和控制台显示的名字
  - `"Description"`: 简单描述mod作用
  - `"LoadPriority"`: mod读取的优先级
  - `"ConVars"`: Source ConVars the mod defines which can have flags (see [ConVars]())
  - `"Scripts"`: Custom squirrel scripts the mod loads (see [Scripts]())
  - `"Localisation"`: mod文件的位置

<!-- A quick summary of all the features shown:
  - `"Name"`: Name of the mod shown when loaded in console and in UI
  - `"Description"`: Quick description of the mod
  - `"LoadPriority"`: Priority mod should have on load
  - `"ConVars"`: Source ConVars the mod defines which can have flags (see [ConVars]())
  - `"Scripts"`: Custom squirrel scripts the mod loads (see [Scripts]())
  - `"Localisation"`: Location for mod's localisation files -->

See [Cheatsheet]() for a more comprehensive list

### 添加定制 Scripts
任意你新创建的 .nut/.gunt 文件必须在在你的mod.json文件中的`"Scripts"`项定义
举个例子:

<!-- Any new .nut/.gnut you create must be defined in the `"Scripts"` section of your mod file -->
```json
  "Scripts": [
      {
          "Path": "path/to/my.nut",
          "RunOn": "( CLIENT || SERVER ) && MP"
      },
      {
          "Path": "path/to/my_second.nut",
          "RunOn": "( CLIENT || SERVER ) && MP",
          "ClientCallback": {
              "Before": "ClientPreMapspawnThing",
              "After": "AfterMapspawnClientThing"
          },
          "ServerCallback": {
              "Before": "ServerPreMapspawncrap",
              "After": "ServerAfterMapspawnWoo"
          }
      }
  ],
```

`Path` 指的是你脚本文件的路径，然后 `RunOn` 指的是需要被编译用于脚本的 VM contexts

>`Path` specifies the path to the script file and `RunOn` are the VM contexts for the script to be compiled on.

客户端和服务端的回调（callbacks）能发生在 mapspawn 之前或之后。他们会执行一个你脚本中定义的一个函数（function），当然，这依据于你运行在什么 VM context 上。未来可能会增加支持更多回调。

Client and server callbacks can either happen before or after mapspawn. They will call a function defined in your script, of course, these depend on what VM context you're running. Future support may be added for more callbacks.

-------

### [原文章链接](https://gist.github.com/VITALISED/b585b882af91370caf4f2137d9fb927a)



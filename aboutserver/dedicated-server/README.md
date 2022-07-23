# 搭建一个专用服务器

## 搭建一个专用服务器

### 搭建步骤

该文档中的内容允许您在 **不使用完整客户端** 的前提下搭建一个专用服务器, 这可以使服务器更为轻量化并更容易长时间运行. Northstar 的服务段目前仍处于开发阶段, 尽管可以正常使用, 但您任会遇到许多的 BUG 或者其他问题.\
想要启动一个 Northstar 的专用服务器, 您只需以 `-dedicated` 参数启动 `NorthstarLauncher.exe` , 这可以手动完成, 然而我们也提供了 `r2ds.bat` 这一批处理文件, 来自动进行此操作.\
当你运行专用服务器时，启动参数将会从 `ns_startup_args_dedi.txt` 中加载, 而不是 `ns_startup_args.txt`.

#### Useful configuration files

* `ns_startup_args_dedi.txt`\
  包含服务器的 [启动参数](./#startup-arguments)
* `R2Northstar\mods\Northstar.CustomServers\mod.json`\
  保存着 [ConVars](./#convars) 的默认参数
* `R2Northstar\mods\Northstar.CustomServers\mod\cfg\autoexec_ns_server.cfg`\
  保存着 [ConVars](./#convars) 的覆写参数

### 有关专用服务器的告诫信息

截至目前,专用服务器端任需要 DirectX 11 以正常工作, 尽管事实上没有什么GPU计算, 但通常来说这需要一块工作的 GPU, 我们预计这会在无GPU的服务器中造成一些问题, 所以请使用 `-softwared3d11` 这一参数来让 DirectX 工作在软件模拟模式中.\
尽管这并非完美, 但这是目前搭建专用服务器的最好方案, 出人意料的是, 这几乎不占用任何的处理器资源, 尽管她能随便吃掉 1GB 的 RAM.\
提到内存占用, 目前来说, 专用服务器能轻松吃掉大量内存资源, 通常为 1.5-2GB, 随着开发的深入, 我认为未来的占用会更少.

### 故障排查

See [troubleshoot](../../hosting-a-server-with-northstar/dedicated-server/troubleshoot.md)

## 启动参数

启动参数可以在 `ns_startup_args_dedi.txt` 中添加.\
Example: `+setplaylist private_match +mp_gamemode ps`

| 参数                         | 接受值                                                           | 描述                                                                                        |
| -------------------------- | ------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| `+setplaylist`             | 参考 [Gamemodes](./#gamemodes) (应该与 `mp_gamemode` 相同v除非您想要私人比赛) | 设置服务器类型 (如果其不是 `private_match`, 那么请确保 `+map` 已正确应用且 **不是** `mp_lobby` 否则您可能无法在一下子发现您的服务器) |
| `+setplaylistvaroverrides` | 参考 [PlaylistOverrides](./#playlist-overrides)                 | 设置服务器的各种行为                                                                                |
| `-port`                    | `1-65535` 之间的整数值                                              | 设置服务器监听的UDP端口                                                                             |
| `+mp_gamemode`             | 参考 [Gamemodes](./#gamemodes)                                  | 强制服务器载入某一模式                                                                               |
| `+map`                     | 参考 [Maps](./#maps) (如不指定，则为 `mp_lobby`)                       | 强制服务器载入特定初始地图                                                                             |

| 特殊标识                  | 描述                                                    |
| --------------------- | ----------------------------------------------------- |
| `-maxplayersplaylist` | 允许 [PlaylistOverrides](./#playlist-overrides) 覆写最大玩家数 |
| `-enablechathooks`    | 允许在聊天框中直接输入指令                                         |

### Playlist overrides

Playlist overrides 决定了服务器的行为. PlaylistOverrides 可以通过 `ns_startup_args_dedi.txt` 中的 `+setplaylistvaroverrides` 参数进行添加.

所有参数必须位于引号中并以空格分开.\
Example: `+setplaylistvaroverrides "run_epilogue 0 featured_mode_amped_tacticals 1"`

| PlaylistOverrides                            | 接受值   | 默认值 | 描述                                                                                                 |
| -------------------------------------------- | ----- | --- | -------------------------------------------------------------------------------------------------- |
| `max_players`                                | `int` |     | 需要与 [`-maxplayersplaylist`](./#Startup\_flags-maxplrplst) 标签一同使用                                   |
| `custom_air_accel_pilot`                     |       |     |                                                                                                    |
| `pilot_health_multiplier`                    |       |     |                                                                                                    |
| `run_epilogue`                               | `0-1` | `1` | 启用撤离运输船                                                                                            |
| `respawn_delay`                              |       |     | 重生间隔                                                                                               |
| `boosts_enabled`                             | `0-1` | `0` | Disable boosts. Doesn't disable Titanmeter. Note that unlike the name suggests `1` disables boosts |
| `earn_meter_pilot_overdrive`                 | `0-1` |     |                                                                                                    |
| `earn_meter_pilot_multiplier`                |       |     |                                                                                                    |
| `earn_meter_titan_multiplier`                |       |     |                                                                                                    |
| `aegis_upgrades`                             | `0-1` | `0` | Enable titan aegis upgrades                                                                        |
| `infinite_doomed_state`                      | `0-1` |     |                                                                                                    |
| `titan_shield_regen`                         | `0-1` | `0` | 启用泰坦护盾在发生                                                                                          |
| `scorelimit`                                 |       |     |                                                                                                    |
| `roundscorelimit`                            |       |     |                                                                                                    |
| `timelimit`                                  |       |     |                                                                                                    |
| `oob_timer_enabled`                          | `0-1` |     | 出界计时器                                                                                              |
| `roundtimelimit`                             |       |     |                                                                                                    |
| `classic_rodeo`                              | `0-1` |     |                                                                                                    |
| `classic_mp`                                 | `0-1` | `1` | 启用开场运输船                                                                                            |
| `fp_embark_enabled`                          |       |     | 第一人称上机与处决                                                                                          |
| `promode_enable`                             | `0-1` | `0` |                                                                                                    |
| `riff_floorislava`                           | `0-1` | `0` | 将全图地面以电烟覆盖                                                                                         |
| `featured_mode_all_holopilot`                | `0-1` | `0` |                                                                                                    |
| `featured_mode_all_grapple`                  | `0-1` | `0` |                                                                                                    |
| `featured_mode_all_phase`                    | `0-1` | `0` |                                                                                                    |
| `featured_mode_all_ticks`                    | `0-1` | `0` |                                                                                                    |
| `featured_mode_tactikill`                    | `0-1` | `0` |                                                                                                    |
| `featured_mode_amped_tacticals`              | `0-1` | `0` |                                                                                                    |
| `featured_mode_rocket_arena`                 | `0-1` | `0` |                                                                                                    |
| `featured_mode_shotguns_snipers`             | `0-1` | `0` |                                                                                                    |
| `iron_rules`                                 | `0-1` | `0` | 禁用弹射与离机                                                                                            |
| `riff_player_bleedout`                       | `0-1` |     |                                                                                                    |
| `player_bleedout_forceHolster`               | `0-1` |     |                                                                                                    |
| `player_bleedout_forceDeathOnTeamBleedout`   | `0-1` |     |                                                                                                    |
| `player_bleedout_bleedoutTime`               | `int` |     |                                                                                                    |
| `player_bleedout_firstAidTime`               | `int` |     |                                                                                                    |
| `player_bleedout_firstAidTimeSelf`           | `int` |     |                                                                                                    |
| `player_bleedout_firstAidHealPercent`        | `int` |     |                                                                                                    |
| `player_bleedout_aiBleedingPlayerMissChance` | `int` |     |                                                                                                    |

## Convars

Convars 位于 `R2Northstar\mods\Northstar.CustomServers\mod\cfg\autoexec_ns_server.cfg` 中.

它允许管理员更改服务器资料，例如TCP端口，名称，描述等.

| 名称                                               | 描述                                                      | 默认值                            | 接受值                              |
| ------------------------------------------------ | ------------------------------------------------------- | ------------------------------ | -------------------------------- |
| `ns_server_name`                                 | 您的服务器在服务器浏览器中的名称                                        | `"Unnamed Northstar Server"`   | `string`                         |
| `ns_server_desc`                                 | 您的服务器在服务器浏览器中的描述                                        | `"Default server description"` | `string`                         |
| `ns_server_password`                             | 进入服务器所需的密码, 当您启用了不安全的验证方式之后,该设置可以被 connect 命令绕过         | `""`                           | `string`                         |
| `ns_report_server_to_masterserver`               | 决定您的服务器是否与主服务器交换验证信息，用于将您的服务器显示于服务器浏览器中                 | `1`                            | `0-1`                            |
| `ns_report_sp_server_to_masterserver`            | 决定您的服务器是否在单人模式时与主服务器交换验证信息, 用于将您的服务器显示于服务器浏览器中          | `0`                            | `0-1`                            |
| `ns_auth_allow_insecure`                         | 允许客户端在不与主服务器验证的情况下使用 `connect <ip>` 连接到您的服务器            | `0`                            | `0-1`                            |
| `ns_erase_auth_info`                             | 决定您的服务器是否在验证握手结束后抹除客户端的验证信息, 可能对于开发有帮助，但建议为1            | `1`                            | `0-1`                            |
| `ns_player_auth_port`                            | 服务器用于和主服务器交换验证信息使用的`TCP`端口                              | `8081`                         | `1-65535`                        |
| `everything_unlocked`                            | 是否在服务器中默认解锁所有的武器，强化等                                    | `1`                            | `0-1`                            |
| `ns_should_return_to_lobby`                      | 是否在对局结束后返回私房大厅，如为0，则会按 playlist 或插件设置进行地图轮换             | `1`                            | `0-1`                            |
| `ns_private_match_only_host_can_change_settings` | 0 --> 玩家可以更改所有设置；1 --> 玩家只能更改地图与模式；2 --> 玩家不能更改任何参数     | `0`                            | `0-2`                            |
| `ns_private_match_countdown_length`              | 在私房菜单点击开始游戏后，私房的倒数计时器时间                                 | `15`                           | `int`                            |
| `ns_private_match_last_mode`                     | 覆写私房大厅的默认模式                                             | `tdm`                          | 所有的 [Gamemode](./#gamemodes)     |
| `ns_private_match_last_map`                      | 覆写私房大厅的默认地图                                             | `mp_forwardbase_kodai`         | 所有的 [Map](./#maps)               |
| `ns_disallowed_weapons`                          | 武器黑名单                                                   |                                | 任何 [Weapons](./#weapons) 以半角逗号分隔 |
| `ns_disallowed_weapon_primary_replacement`       | 替换黑名单武器为                                                |                                | 一件 [Weapon](./#weapons)          |
| `ns_should_log_unknown_clientcommands`           | 未知的控制台命令是否在终端中显示，如烦人可关闭                                 | `1`                            | `0-1`                            |
| `net_chan_limit_mode`                            | 0 --> 不限制网络通道超时客户端；1 --> 剔除网络通道超时客户端；2 --> 将超时客户端显示在终端中 | `2`                            | `0-2`                            |
| `net_chan_limit_msec_per_sec`                    | net\_chan\_limit\_mode 中的超时时间设定 (ms)                    | `30`                           | `int`                            |
| `base_tickinterval_mp`                           | 服务器时间刻的间隔，时间刻的值为 1 / 设置值                                | `0.016666667`                  | `float`                          |
| `sv_updaterate_mp`                               | 服务器每秒发送数据包的最大次数，即所谓 tickrate                            | `20`                           | `int`                            |
| `sv_max_snapshots_multiplayer`                   | 服务器所存储的用于回放的tick数量，应为 sv\_updaterate\_mp \* 15          | `300`                          | `int`                            |
| `host_skip_client_dll_crc`                       | 服务器是否允许魔改了 `client.dll` 的玩家加入，颜色修改等 mod 通常会改变此文件        | `1`                            | `0-1`                            |

## Gamemodes

Gamemodes 可以通过 [`+mp_gamemode`](./#Startup\_args-mpgamemode) 启动参数指定

如果您使用 [`ns_should_return_to_lobby 0`](./#Convars-returntolobby) convar 的话, [`ns_private_match_last_mode`](./#Convars-lastmode) convar 也需要被正确设定

### Vanilla

| Playlist       | Title               |
| -------------- | ------------------- |
| private\_match | 私人比赛                |
| ~~aitdm~~      | ~~消耗战~~             |
| ~~at~~         | ~~赏金猎人~~            |
| coliseum       | 竞技场                 |
| cp             | 强化据点                |
| ctf            | 夺旗                  |
| ~~fd\_easy~~   | ~~边境防御 (Easy)~~     |
| ~~fd\_hard~~   | ~~边境防御 (Hard)~~     |
| ~~fd\_insane~~ | ~~边境防御 (Insane)~~   |
| ~~fd\_master~~ | ~~边境防御 (Master)~~   |
| ~~fd\_normal~~ | ~~边境防御 (Regular)~~  |
| lf             | 烈火战场                |
| lts            | Last Titan Standing |
| mfd            | Marked For Death    |
| ps             | 铁驭对铁驭               |
| solo           | Campaign            |
| tdm            | 小规模战斗               |
| ttdm           | 泰坦争斗                |

### Vanilla (Featured)

| Playlist      | Title                     |
| ------------- | ------------------------- |
| alts          | Aegis Last Titan Standing |
| attdm         | 神盾泰坦争斗                    |
| ffa           | Free For All              |
| fra           | Free Agents               |
| holopilot\_lf | 大骗局                       |
| rocket\_lf    | Rocket Arena              |
| turbo\_lts    | Turbo Last Titan Standing |
| turbo\_ttdm   | 涡轮泰坦争斗                    |

### Northstar.Custom

| Playlist  | Title              |
| --------- | ------------------ |
| chamber   | One in the Chamber |
| ctf\_comp | Competitive CTF    |
| fastball  | Fastball           |
| gg        | 军备竞赛               |
| hidden    | 幽灵猎杀               |
| hs        | 追迷藏                |
| inf       | 感染                 |
| kr        | Amped Killrace     |
| sbox      | 沙盒                 |
| sns       | Sticks and Stones  |
| tffa      | Titan FFA          |
| tt        | Titan Tag          |

### Northstar.Coop

| Playlist | Title             |
| -------- | ----------------- |
| sp\_coop | Singleplayer Coop |

## Weapons

| Weapon Code                  | Weapon name    |
| ---------------------------- | -------------- |
| mp\_weapon\_car              | CAR            |
| mp\_weapon\_alternator\_smg  | 转换者            |
| mp\_weapon\_hemlok\_smg      | 电能冲锋枪          |
| mp\_weapon\_r97              | R-97           |
| mp\_weapon\_hemlok           | 汗洛             |
| mp\_weapon\_vinson           | 平行步枪           |
| mp\_weapon\_g2               | G2             |
| mp\_weapon\_rspn101          | R-201          |
| mp\_weapon\_rspn101\_og      | R-101          |
| mp\_weapon\_esaw             | Devotion       |
| mp\_weapon\_lstar            | L-STAR         |
| mp\_weapon\_lmg              | Spitfire       |
| mp\_weapon\_shotgun          | EVA-8 Auto     |
| mp\_weapon\_mastiff          | Mastiff        |
| mp\_weapon\_dmr              | DMR            |
| mp\_weapon\_sniper           | 克莱伯            |
| mp\_weapon\_doubletake       | Double Take    |
| mp\_weapon\_pulse\_lmg       | 冷战榴弹枪          |
| mp\_weapon\_smr              | Sidewinder SMR |
| mp\_weapon\_softball         | Softball       |
| mp\_weapon\_epg              | EPG-1          |
| mp\_weapon\_shotgun\_pistol  | 莫桑比克           |
| mp\_weapon\_wingman\_n       | 菁英小帮手          |
| mp\_weapon\_autopistol       | RE-45          |
| mp\_weapon\_semipistol       | P2016          |
| mp\_weapon\_wingman          | 小帮手            |
| mp\_weapon\_mgl              | MGL            |
| mp\_weapon\_arc\_launcher    | Thunderbolt    |
| mp\_weapon\_rocket\_launcher | Archer         |
| mp\_weapon\_defender         | 电能步枪           |

## Maps

地图可以通过 [`ns_should_return_to_lobby 0`](./#Convars-returntolobby) 来设置自动轮换

第一张地图可以通过 [`ns_private_match_last_map`](./#Convars-lastmap) 指定

不存在禁止某张图加入轮换池的方法（投票插件：“？”).

### Vanilla (mp)

| Map                     | Title  |
| ----------------------- | ------ |
| mp\_angel\_city         | 天使城    |
| mp\_black\_water\_canal | 黑水运河   |
| mp\_box                 | Box    |
| mp\_coliseum            | 竞技场    |
| mp\_coliseum\_column    | 梁柱     |
| mp\_colony02            | 殖民地    |
| mp\_complex3            | 综合设施   |
| mp\_crashsite3          | 坠机现场   |
| mp\_drydock             | 干坞     |
| mp\_eden                | 伊甸     |
| mp\_forwardbase\_kodai  | 虎大前进基地 |
| mp\_glitch              | 异常     |
| mp\_grave               | 新兴城镇   |
| mp\_homestead           | 家园     |
| mp\_lf\_deck            | 甲板     |
| mp\_lf\_meadow          | 草原     |
| mp\_lf\_stacks          | 堆积地    |
| mp\_lf\_township        | 城镇     |
| mp\_lf\_traffic         | 交通     |
| mp\_lf\_uma             | UMA    |
| mp\_lobby               | 大厅     |
| mp\_relic02             | 遗迹     |
| mp\_rise                | 崛起     |
| mp\_thaw                | 系外行星   |
| mp\_wargames            | 战争游戏   |

### Vanilla (sp)

| Map                    | Title              |
| ---------------------- | ------------------ |
| sp\_training           | 铁驭训练               |
| sp\_crashsite          | BT-7274            |
| sp\_sewers1            | 鲜血与钢铁              |
| sp\_boomtown\_start    | 踏入虚空 - Part 1      |
| sp\_boomtown           | 踏入虚空 - Part 2      |
| sp\_boomtown\_end      | 踏入虚空 - Part 2      |
| sp\_hub\_timeshift     | 因果报应 - Part 1 or 3 |
| sp\_timeshift\_spoke02 | 因果报应 - Part 2      |
| sp\_beacon             | 信号台 - Part 1 or 3  |
| sp\_beacon\_spoke0     | 信号台 - Part 2       |
| sp\_tday               | 烈火审判               |
| sp\_s2s                | 圣柜                 |
| sp\_skyway\_v1         | 折叠时空武器             |

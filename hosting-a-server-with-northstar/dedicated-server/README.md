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

See [troubleshoot](troubleshoot.md)

## 启动参数

启动参数可以在 `ns_startup_args_dedi.txt` 中添加.\
Example: `+setplaylist private_match +mp_gamemode ps`

| 参数                  | 接受值                                                 | 描述                                                               |
| -------------------------- | --------------------------------------------------------------  | ------------------------------------------------------------------------- |
| `+setplaylist`             | 参考 [Gamemodes](./#gamemodes) (应该与 `mp_gamemode` 相同v除非您想要私人比赛) | 设置服务器类型 (如果其不是 `private_match`, 那么请确保 `+map` 已正确应用且 **不是** `mp_lobby` 否则您可能无法在一下子发现您的服务器) |
| `+setplaylistvaroverrides` | 参考 [PlaylistOverrides](./#playlist-overrides)                  | 设置服务器的各种行为                                         |
| `-port`                    |  `1-65535` 之间的整数值                                          | 设置服务器监听的UDP端口                       |
| `+mp_gamemode`             | 参考 [Gamemodes](./#gamemodes)                                | 强制服务器载入某一模式                                        |
| `+map`                     | 参考 [Maps](./#maps) (如不指定，则为 `mp_lobby`) | 强制服务器载入特定初始地图                           |

| 特殊标识                | 描述                                                                    |
| --------------------- | ------------------------------------------------------------------------------ |
| `-maxplayersplaylist` | 允许 [PlaylistOverrides](./#playlist-overrides) 覆写最大玩家数                  |
| `-enablechathooks`    | 允许在聊天框中直接输入指令                                                      |

### Playlist overrides

Playlist overrides 决定了服务器的行为. PlaylistOverrides 可以通过 `ns_startup_args_dedi.txt` 中的 `+setplaylistvaroverrides` 参数进行添加.

所有参数必须位于引号中并以空格分开.\
Example: `+setplaylistvaroverrides "run_epilogue 0 featured_mode_amped_tacticals 1"`

| PlaylistOverrides                            | 接受值          | 默认值         |                       描述                                                                                   |
| -------------------------------------------- | --------------- | ------------- | ---------------------------------------------------------------------------------------------- |
| `max_players`                                | `int`           |               | 需要与 [`-maxplayersplaylist`](./#Startup\_flags-maxplrplst) 标签一同使用 |
| `custom_air_accel_pilot`                     |                 |               |                                                                                                |
| `pilot_health_multiplier`                    |                 |               |                                                                                                |
| `run_epilogue`                               | `0-1`           | `1`           | 启用撤离运输船                                                                        |
| `respawn_delay`                              |                 |               | 重生间隔                                                                            |
| `boosts_enabled`                             | `0-1`           | `0`           | Disable boosts. Doesn't disable Titanmeter. Note that unlike the name suggests `1` disables boosts |
| `earn_meter_pilot_overdrive`                 | `0-1`           |               |                                                                                                |
| `earn_meter_pilot_multiplier`                |                 |               |                                                                                                |
| `earn_meter_titan_multiplier`                |                 |               |                                                                                                |
| `aegis_upgrades`                             | `0-1`           | `0`           | Enable titan aegis upgrades                                                                    |
| `infinite_doomed_state`                      | `0-1`           |               |                                                                                                |
| `titan_shield_regen`                         | `0-1`           | `0`           | 启用泰坦护盾在发生                                                             |
| `scorelimit`                                 |                 |               |                                                                                                |
| `roundscorelimit`                            |                 |               |                                                                                                |
| `timelimit`                                  |                 |               |                                                                                                |
| `oob_timer_enabled`                          | `0-1`           |               | 出界计时器                                                                      |
| `roundtimelimit`                             |                 |               |                                                                                                |
| `classic_rodeo`                              | `0-1`           |               |                                                                                                |
| `classic_mp`                                 | `0-1`           | `1`           | 启用开场运输船                                                                         |
| `fp_embark_enabled`                          |                 |               | 第一人称上机与处决                                                            |
| `promode_enable`                             | `0-1`           | `0`           |                                                                                                |
| `riff_floorislava`                           | `0-1`           | `0`           | 将全图地面以电烟覆盖                                                |
| `featured_mode_all_holopilot`                | `0-1`           | `0`           |                                                                                                |
| `featured_mode_all_grapple`                  | `0-1`           | `0`           |                                                                                                |
| `featured_mode_all_phase`                    | `0-1`           | `0`           |                                                                                                |
| `featured_mode_all_ticks`                    | `0-1`           | `0`           |                                                                                                |
| `featured_mode_tactikill`                    | `0-1`           | `0`           |                                                                                                |
| `featured_mode_amped_tacticals`              | `0-1`           | `0`           |                                                                                                |
| `featured_mode_rocket_arena`                 | `0-1`           | `0`           |                                                                                                |
| `featured_mode_shotguns_snipers`             | `0-1`           | `0`           |                                                                                                |
| `iron_rules`                                 | `0-1`           | `0`           | 禁用弹射与离机                                                                |
| `riff_player_bleedout`                       | `0-1`           |               |                                                                                                |
| `player_bleedout_forceHolster`               | `0-1`           |               |                                                                                                |
| `player_bleedout_forceDeathOnTeamBleedout`   | `0-1`           |               |                                                                                                |
| `player_bleedout_bleedoutTime`               |  `int`          |               |                                                                                                |
| `player_bleedout_firstAidTime`               | `int`           |               |                                                                                                |
| `player_bleedout_firstAidTimeSelf`           | `int`           |               |                                                                                                |
| `player_bleedout_firstAidHealPercent`        | `int`           |               |                                                                                                |
| `player_bleedout_aiBleedingPlayerMissChance` | `int`           |               |                                                                                                |

## Convars

Convars 位于 `R2Northstar\mods\Northstar.CustomServers\mod\cfg\autoexec_ns_server.cfg` 中.

它允许管理员更改服务器资料，例如TCP端口，名称，描述等.

| 名称                                             | 描述                                                                                                                                                                                 | 默认值                  | 接受值                                    |
| ------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------ | -------------------------------------------------- |
| `ns_server_name`                                 | 您的服务器在服务器浏览器中的名称                                                                                                                                                    | `"Unnamed Northstar Server"`   | `string`                                           |
| `ns_server_desc`                                 | 您的服务器在服务器浏览器中的描述                                                                                                                                             | `"Default server description"` | `string`                                           |
| `ns_server_password`                             | 进入服务器所需的密码, 当您启用了不安全的验证方式之后,该设置可以被 connect 命令绕过                                                                      | `""`                           | `string`                                           |
| `ns_report_server_to_masterserver`               | 决定您的服务器是否与主服务器交换验证信息，用于将您的服务器显示于服务器浏览器中                                                                                         | `1`                            | `0-1`                                              |
| `ns_report_sp_server_to_masterserver`            | 决定您的服务器是否在单人模式时与主服务器交换验证信息, 用于将您的服务器显示于服务器浏览器中                                                        | `0`                            | `0-1`                                              |
| `ns_auth_allow_insecure`                         | 允许客户端在不与主服务器验证的情况下使用 `connect <ip> `连接到您的服务器 | `0`                            | `0-1`                                              |
| `ns_erase_auth_info`                             | 决定您的服务器是否在验证握手结束后抹除客户端的验证信息, 可能对于开发有帮助，但建议为1                                               | `1`                            | `0-1`                                              |
| `ns_player_auth_port`                            | 服务器用于和主服务器交换验证信息使用的`TCP`端口                                                                                       | `8081`                         | `1-65535`                                          |
| `everything_unlocked`                            | 是否在服务器中默认解锁所有的武器，强化等                                                                                                                            | `1`                            | `0-1`                                              |
| `ns_should_return_to_lobby`                      | 是否在对局结束后返回私房大厅，如为0，则会按  playlist 或插件设置进行地图轮换                                                   | `1`                            | `0-1`                                              |
| `ns_private_match_only_host_can_change_settings` | 0 --> 玩家可以更改所有设置；1 --> 玩家只能更改地图与模式；2 --> 玩家不能更改任何参数                                                                  | `0`                            | `0-2`                                              |
| `ns_private_match_countdown_length`              | 在私房菜单点击开始游戏后，私房的倒数计时器时间                                                                                                           | `15`                           | `int`                                              |
| `ns_private_match_last_mode`                     | 覆写私房大厅的默认模式                                                                                                                                                     | `tdm`                          | 所有的 [Gamemode](./#gamemodes)                       |
| `ns_private_match_last_map`                      | 覆写私房大厅的默认地图                                                                                                                                                          | `mp_forwardbase_kodai`         | 所有的 [Map](./#maps)                                 |
| `ns_disallowed_weapons`                          | 武器黑名单                                                                                                                                                                          |                                | 任何 [Weapons](./#weapons) 以半角逗号分隔 |
| `ns_disallowed_weapon_primary_replacement`       | 替换黑名单武器为                                                                                                                                                  |                                | 一件 [Weapon](./#weapons)                             |
| `ns_should_log_unknown_clientcommands`           | 未知的控制台命令是否在终端中显示，如烦人可关闭                                                                                  | `1`                            | `0-1`                                              |
| `net_chan_limit_mode`                            | 0 --> 不限制网络通道超时客户端；1 --> 剔除网络通道超时客户端；2 --> 将超时客户端显示在终端中             | `2`                            | `0-2`                                              |
| `net_chan_limit_msec_per_sec`                    | net\_chan\_limit\_mode 中的超时时间设定 (ms)                                       | `30`                           | `int`                                              |
| `base_tickinterval_mp`                           | 服务器时间刻的间隔，时间刻的值为 1 / 设置值                                                                                                 | `0.016666667`                  | `float`                                            |
| `sv_updaterate_mp`                               | 服务器每秒发送数据包的最大次数，即所谓 tickrate  | `20`                           | `int`                                              |
| `sv_max_snapshots_multiplayer`                   | 服务器所存储的用于回放的tick数量，应为 sv\_updaterate\_mp \* 15                                                                                   | `300`                          | `int`                                              |
| `host_skip_client_dll_crc`                       | 服务器是否允许魔改了 `client.dll` 的玩家加入，颜色修改等 mod 通常会改变此文件                                                                | `1`                            | `0-1`                                              |

## Gamemodes

Gamemodes 可以通过 [`+mp_gamemode`](./#Startup\_args-mpgamemode) 启动参数指定

如果您使用 [`ns_should_return_to_lobby 0`](./#Convars-returntolobby) convar 的话,  [`ns_private_match_last_mode`](./#Convars-lastmode) convar 也需要被正确设定

### Vanilla

| Playlist | Title |
| --- | --- |
| private_match | 私人比赛 |
| ~~aitdm~~ | ~~消耗战~~ |
| ~~at~~ | ~~赏金猎人~~ |
| coliseum | 竞技场 |
| cp | 强化据点 |
| ctf | 夺旗 |
| ~~fd_easy~~ | ~~边境防御 (Easy)~~ |
| ~~fd_hard~~ | ~~边境防御 (Hard)~~ |
| ~~fd_insane~~ | ~~边境防御 (Insane)~~ |
| ~~fd_master~~ | ~~边境防御 (Master)~~ |
| ~~fd_normal~~ | ~~边境防御 (Regular)~~ |
| lf | 烈火战场 |
| lts | Last Titan Standing |
| mfd | Marked For Death |
| ps | 铁驭对铁驭 |
| solo | Campaign |
| tdm | 小规模战斗 |
| ttdm | 泰坦争斗 |

### Vanilla (Featured)

| Playlist | Title |
| --- | --- |
| alts | Aegis Last Titan Standing |
| attdm | 神盾泰坦争斗 |
| ffa | Free For All |
| fra | Free Agents |
| holopilot_lf | 大骗局 |
| rocket_lf | Rocket Arena |
| turbo_lts | Turbo Last Titan Standing |
| turbo_ttdm | 涡轮泰坦争斗 |

### Northstar.Custom

| Playlist | Title |
| --- | --- |
| chamber | One in the Chamber |
| ctf_comp | Competitive CTF |
| fastball | Fastball |
| gg | 军备竞赛 |
| hidden | 幽灵猎杀 |
| hs | 追迷藏 |
| inf | 感染 |
| kr | Amped Killrace |
| sbox | 沙盒 |
| sns | Sticks and Stones |
| tffa | Titan FFA |
| tt | Titan Tag |

### Northstar.Coop

| Playlist | Title |
| --- | --- |
| sp_coop | Singleplayer Coop |

## Weapons

Weapon Code|Weapon name
-|-
mp_weapon_car|CAR
mp_weapon_alternator_smg|转换者
mp_weapon_hemlok_smg|电能冲锋枪
mp_weapon_r97|R-97
mp_weapon_hemlok|汗洛
mp_weapon_vinson|平行步枪
mp_weapon_g2|G2
mp_weapon_rspn101|R-201
mp_weapon_rspn101_og|R-101
mp_weapon_esaw|Devotion
mp_weapon_lstar|L-STAR
mp_weapon_lmg|Spitfire
mp_weapon_shotgun|EVA-8 Auto
mp_weapon_mastiff|Mastiff
mp_weapon_dmr|DMR
mp_weapon_sniper|克莱伯
mp_weapon_doubletake|Double Take
mp_weapon_pulse_lmg|冷战榴弹枪
mp_weapon_smr|Sidewinder SMR
mp_weapon_softball|Softball
mp_weapon_epg|EPG-1
mp_weapon_shotgun_pistol|莫桑比克
mp_weapon_wingman_n|菁英小帮手
mp_weapon_autopistol|RE-45
mp_weapon_semipistol|P2016
mp_weapon_wingman|小帮手
mp_weapon_mgl|MGL
mp_weapon_arc_launcher|Thunderbolt
mp_weapon_rocket_launcher|Archer
mp_weapon_defender|电能步枪

## Maps

地图可以通过 [`ns_should_return_to_lobby 0`](./#Convars-returntolobby) 来设置自动轮换

第一张地图可以通过 [`ns_private_match_last_map`](./#Convars-lastmap) 指定

不存在禁止某张图加入轮换池的方法（投票插件：“？”).

### Vanilla (mp)

| Map | Title |
| --- | --- |
| mp_angel_city | 天使城 |
| mp_black_water_canal | 黑水运河 |
| mp_box | Box |
| mp_coliseum | 竞技场 |
| mp_coliseum_column | 梁柱 |
| mp_colony02 | 殖民地 |
| mp_complex3 | 综合设施 |
| mp_crashsite3 | 坠机现场 |
| mp_drydock | 干坞 |
| mp_eden | 伊甸 |
| mp_forwardbase_kodai | 虎大前进基地 |
| mp_glitch | 异常 |
| mp_grave | 新兴城镇 |
| mp_homestead | 家园 |
| mp_lf_deck | 甲板 |
| mp_lf_meadow | 草原 |
| mp_lf_stacks | 堆积地 |
| mp_lf_township | 城镇 |
| mp_lf_traffic | 交通 |
| mp_lf_uma | UMA |
| mp_lobby | 大厅 |
| mp_relic02 | 遗迹 |
| mp_rise | 崛起 |
| mp_thaw | 系外行星 |
| mp_wargames | 战争游戏 |

### Vanilla (sp)

| Map | Title |
| --- | --- |
| sp_training | 铁驭训练 |
| sp_crashsite | BT-7274 |
| sp_sewers1 | 鲜血与钢铁 |
| sp_boomtown_start | 踏入虚空 - Part 1 |
| sp_boomtown | 踏入虚空 - Part 2 |
| sp_boomtown_end | 踏入虚空 - Part 2 |
| sp_hub_timeshift | 因果报应 - Part 1 or 3 |
| sp_timeshift_spoke02 | 因果报应 - Part 2 |
| sp_beacon | 信号台 - Part 1 or 3 |
| sp_beacon_spoke0 | 信号台 - Part 2 |
| sp_tday | 烈火审判 |
| sp_s2s | 圣柜 |
| sp_skyway_v1 | 折叠时空武器 |

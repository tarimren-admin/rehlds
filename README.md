# ReHLDS [![C/C++ CI](https://github.com/rehlds/ReHLDS/actions/workflows/build.yml/badge.svg)](https://github.com/rehlds/ReHLDS/actions/workflows/build.yml) [![GitHub release (by tag)](https://img.shields.io/github/downloads/rehlds/ReHLDS/latest/total)](https://github.com/rehlds/ReHLDS/releases/latest) ![GitHub all releases](https://img.shields.io/github/downloads/rehlds/ReHLDS/total) [![Percentage of issues still open](http://isitmaintained.com/badge/open/rehlds/ReHLDS.svg)](http://isitmaintained.com/project/rehlds/ReHLDS "Percentage of issues still open") [![License: GPL v3](https://img.shields.io/badge/License-GPL%20v3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0) <img align="right" src="https://user-images.githubusercontent.com/5860435/111066129-040e5e00-84f0-11eb-9e1f-7a7e8611da2b.png" alt="ReHLDS" />
反向工程（并修复了错误）的HLDS

## 项目简介
ReHLDS是通过对HLDS（版本6152/6153）的逆向工程，使用嵌入在HLDS（Linux版本）中的engine_i486.so的DWARF调试信息而得到的结果。

除了逆向工程，还发现并修复了许多缺陷和（潜在的）错误。

可以尝试在服务器使用ReHLDS: [游戏追踪](http://www.gametracker.com/search/?search_by=server_variable&search_by2=sv_version)

> [!TIP]
> ReHLDS linux-releases 现在通过 `GPG`签名, 公钥: `63547829004f07716f7be4856c32c4282e60fb67` 可以在 [https://keyserver.ubuntu.com/](https://keyserver.ubuntu.com/pks/lookup?search=63547829004f07716f7be4856c32c4282e60fb67+&fingerprint=on&op=index)找到.
>
> 如何使用:
> 1. [下载](https://keyserver.ubuntu.com/pks/lookup?op=get&search=0x63547829004f07716f7be4856c32c4282e60fb67) `63547829004f07716f7be4856c32c4282e60fb67.asc` 密钥
> 2. 导入: `gpg --import 63547829004f07716f7be4856c32c4282e60fb67.asc`
> 3. 下载发布版 `archive` 和 `.asc` 文件.
> 4. 校验: `gpg --verify some-rehlds.zip.asc some-rehlds.zip`.

## 项目目标
<ul>
<li>提供更稳定的（比官方版本更稳定）半条命专用服务器版本，带有扩展的API，用于模组和插件</li>
<li>性能优化（例如使用SSE进行向量数学）是未来的目标</li>
</ul>

## 如何使用
ReHLDS与通过steamcmd下载的官方HLDS预周年纪念版（引擎版本<=8684）完全兼容. 只需要下载ReHLDS二进制文件并替换原始swds.dll/engine_i486.so. 对于Windows，还可以复制一个包含调试信息的swds.pdb文件.

> [!警告]  
> ReHLDS不兼容通过hldsupdatetool下载的旧5xxx或更低版本的平台.

#### 通过steamcmd下载HLDS

```
app_set_config 90 mod cstrike
app_update 90 -beta steam_legacy validate
```

## 下载
* [发布版本](https://github.com/rehlds/ReHLDS/releases)
* [开发版本](https://github.com/rehlds/ReHLDS/actions/workflows/build.yml)

ReHLDS二进制文件需要 `SSE`, `SSE2` 和 `SSE3` 指令集才能运行，且兼容 `SSE4.1` 和 `SSE4.2`

<b>警告!</b> ReHLDS与原始hld不兼容.因为它使用原始hld以外的编译器编译.
这意味着进行二进制代码分析的插件（例如Orpheu）可能无法与ReHLDS配合使用.

## 设置
<details>
<summary>点击展开</summary>
<ul>
<li>listipcfgfile &lt;filename&gt; // File for permanent ip bans. Default: listip.cfg
<li>syserror_logfile &lt;filename&gt; // File for the system error log. Default: sys_error.log
<li>sv_auto_precache_sounds_in_models &lt;1|0&gt; // Automatically precache sounds attached to models. Deault: 0
<li>sv_delayed_spray_upload &lt;1|0&gt; // Upload custom sprays after entering the game instead of when connecting. It increases upload speed. Default: 0
<li>sv_echo_unknown_cmd &lt;1|0&gt; // Echo in the console when trying execute an unknown command. Default: 0
<li>sv_rcon_condebug &lt;1|0&gt; // Print rcon debug in the console. Default: 1
<li>sv_force_ent_intersection &lt;1|0&gt; // In a 3-rd party plugins used to force colliding of SOLID_SLIDEBOX entities. Default: 0
<li>sv_rehlds_force_dlmax &lt;1|0&gt; // Force a client's cl_dlmax cvar to 1024. It avoids an excessive packets fragmentation. Default: 0
<li>sv_rehlds_hull_centering &lt;1|0&gt; // Use center of hull instead of corner. Default: 0
<li>sv_rehlds_movecmdrate_max_avg // Max average level of 'move' cmds for ban. Default: 400
<li>sv_rehlds_movecmdrate_avg_punish // Time in minutes for which the player will be banned (0 - Permanent, use a negative number for a kick). Default: 5
<li>sv_rehlds_movecmdrate_max_burst // Max burst level of 'move' cmds for ban. Default: 2500
<li>sv_rehlds_movecmdrate_burst_punish // Time in minutes for which the player will be banned (0 - Permanent, use a negative number for a kick). Default: 5
<li>sv_rehlds_send_mapcycle &lt;1|0&gt; // Send mapcycle.txt in serverinfo message (HLDS behavior, but it is unused on the client). Default: 0
<li>sv_rehlds_stringcmdrate_max_avg // Max average level of 'string' cmds for ban. Default: 80
<li>sv_rehlds_stringcmdrate_avg_punish // Time in minutes for which the player will be banned (0 - Permanent, use a negative number for a kick). Default: 5
<li>sv_rehlds_stringcmdrate_max_burst // Max burst level of 'string' cmds for ban. Default: 400
<li>sv_rehlds_stringcmdrate_burst_punish // Time in minutes for which the player will be banned (0 - Permanent, use a negative number for a kick). Default: 5
<li>sv_rehlds_userinfo_transmitted_fields // Userinfo fields only with these keys will be transmitted to clients via network. If not set then all fields will be transmitted (except prefixed with underscore). Each key must be prefixed by backslash, for example "\name\model\*sid\*hltv\bottomcolor\topcolor". See [wiki](https://github.com/rehlds/ReHLDS/wiki/Userinfo-keys) to collect sufficient set of keys for your server. Default: ""
<li>sv_rehlds_attachedentities_playeranimationspeed_fix // Fixes bug with gait animation speed increase when player has some attached entities (aiments). Can cause animation lags when cl_updaterate is low. Default: 0
<li>sv_rehlds_maxclients_from_single_ip // Limit number of connections at the same time from single IP address, not confuse to already connected players. Default: 5
<li>sv_rehlds_local_gametime &lt;1|0&gt; // A feature of local gametime which decrease "lags" if you run same map for a long time. Default: 0
<li>sv_use_entity_file // Use custom entity file for a map. Path to an entity file will be "maps/[map name].ent". 0 - use original entities. 1 - use .ent files from maps directory. 2 - use .ent files from maps directory and create new .ent file if not exist.
<li>sv_usercmd_custom_random_seed // When enabled server will populate an additional random seed independent of the client. Default: 0
<li>sv_net_incoming_decompression &lt;1|0&gt; // When enabled server will decompress of incoming compressed file transfer payloads. Default: 1
<li>sv_net_incoming_decompression_max_ratio &lt;0|100&gt; // Sets the max allowed ratio between compressed and uncompressed data for file transfer. (A ratio close to 90 indicates large uncompressed data with low entropy) Default: 80.0
<li>sv_net_incoming_decompression_max_size &lt;16|65536&gt; // Sets the max allowed size for decompressed file transfer data. Default: 65536 bytes
<li>sv_net_incoming_decompression_min_failures &lt;0|10&gt; // Sets the min number of decompression failures required before a player's connection is flagged for potential punishment. Default: 4
<li>sv_net_incoming_decompression_max_failures &lt;0|10&gt; // Sets the max number of decompression failures allowed within a specified time window before action is taken against the player. Default: 10
<li>sv_net_incoming_decompression_min_failuretime: &lt;0.1|10.0&gt; // Sets the min time in secs within which decompression failures are tracked to determine if the player exceeds the failure thresholds. Default: 0.1
<li>sv_net_incoming_decompression_punish // Time in minutes for which the player will be banned for malformed/abnormal bzip2 fragments (0 - Permanent, use a negative number for a kick). Default: -1
<li>sv_tags &lt;comma-delimited string list of tags&gt; // Sets a string defining the "gametags" for this server, this is optional, but if it is set it allows users/scripts to filter in the matchmaking/server-browser interfaces based on the value. Default: ""
<li>sv_filterban &lt;-1|0|1&gt;// Set packet filtering by IP mode. -1 - All players will be rejected without any exceptions. 0 - No checks will happen. 1 - All incoming players will be checked if they're IP banned (if they have an IP filter entry), if they are, they will be kicked. Default: 1
</ul>
</details>

## 命令
<ul>
<li>rescount // Prints the total count of precached resources in the server console
<li>reslist &lt;sound | model | decal | generic | event&gt; // Separately prints the details of the precached resources for sounds, models, decals, generic and events in server console. Useful for managing resources and dealing with the goldsource precache limits.
<li>rcon_adduser &lt;ipaddress/CIDR&gt; // Add a new IP address or CIDR range to RCON user list (This command adds a new IP address to the RCON user list. The specified IP or CIDR range is granted privileged access to server console. Without any Rcon users, access is allowed to anyone with a valid password)</li>
<li>rcon_deluser &lt;ipaddress&gt; {removeAll} // Remove an IP address or CIDR range from RCON user list</li>
<li>rcon_users // List all IP addresses and CIDR ranges in RCON user list</li>
</ul>

## 构建说明
### 环境要求
构建 ReHLDS 需要一些软件要求:

#### Windows操作系统
<pre>
Visual Studio 2015（C++14标准）及更新版本
</pre>

#### Linux操作系统
<pre>
cmake >= 3.10
GCC >= 4.9.2 (可选)
ICC >= 15.0.1 20141023 (可选)
LLVM (Clang) >= 6.0 (可选)
</pre>

### 构建

#### Windows操作系统
使用 `Visual Studio` 构建, 打开 `msvc/ReHLDS.sln` 并从解决方案配置列表中选择 `Release Swds` 或 `Debug Swds`

#### Linux操作系统

* 可选选项使用 `build.sh --compiler=[gcc] --jobs=[N] -D[option]=[ON or OFF]` (无需方括号)

<pre>
-c=|--compiler=[icc|gcc|clang]  - 选择用于构建的首选 C/C++ 编译器
-j=|--jobs=[N]                  - 指定同时运行的作业（命令）的数量（以加快构建）

<sub>定义 (-D)</sub>
DEBUG                           - 启用调试模式
USE_STATIC_LIBSTDC              - 启用静态链接库 libstdc++
</pre>

* ICC          <pre>./build.sh --compiler=intel</pre>
* LLVM (Clang) <pre>./build.sh --compiler=clang</pre>
* GCC          <pre>./build.sh --compiler=gcc</pre>

##### 检查构建环境 (Debian / Ubuntu)

<details>
<summary>点击展开</summary>

<ul>
<li>
安装所需的软件包
<pre>
sudo dpkg --add-architecture i386
sudo apt-get update
sudo apt-get install -y gcc-multilib g++-multilib
sudo apt-get install -y build-essential
sudo apt-get install -y libc6-dev libc6-dev-i386
sudo apt-get install -y cmake			
</pre>
</li>

<li>
选择首选的C/C++编译器
<pre>
1) sudo apt-get install -y gcc g++
2) sudo apt-get install -y clang
</pre>
</li>
</ul>
</details>

## 如何为项目提供支持
只需将其安装在您的游戏服务器上，并报告遇到的问题.
也欢迎合并请求 :)

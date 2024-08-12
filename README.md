# FloraBot
**一个新的, 使用 Python 编写的支持插件的 QQBot**
## 食用方法(面向小白)
1. **Windows: 前往 [`Python官网`](https://www.python.org/downloads) 下载不低于 `Python3.11` 的版本进行安装, Linux: 运行命令**
```Shell
apt install python3
```
**可将 python3 改为一个指定的版本, 如作者喜欢用的 python3.11**
2. **点击右上角绿色的 `Code` 按钮, 再点击 `Download ZIP` 下载**
3. **用户解压后可删去 `PluginTemplate` 文件夹, 开发者可保留**
4. **如果是 Windows 用户, 在文件 `FloraBot.py` 的同级目录可创建一个文本文档, 内容为**
```Shell
python FloraBot.py
```
**然后保存, 再重命名文件, 将后缀名 `.txt` 改为 `.bat`双击运行一下**  
**若无法运行, 找到你安装 Python 的路径, 再找到 `python.exe` 将脚本内容改为**
```Shell
python.exe的绝对路径 FloraBot.py
```
**保存然后再运行**  
**如果是 Linux 用户, 在文件 `FloraBot.py` 的同级目录可创建一个后缀名为 `.sh` 的文件, 内容为**
```Shell
python3 FloraBot.py
```
**使用 python3 命令不一定可以运行, 可改为一个指定的版本, 如 python3.11**  
**运行脚本**
5. **首次启动会启动失败, 此时会在文件 `FloraBot.py` 的同级目录下生成一个 `Config.json` 文件, 编辑它**
**`Config.json` 文件键值对照表:**
* **`AutoInstallLibraries`: 是否自动安装 pip 安装所需的第三方库, 默认为: `true`**
* **`FloraHost`: Bot 监听的 IP 地址, 默认值为: `127.0.0.1`**
* **`FloraPort`: Bot 监听的端口号, 默认值为: `3003`**
**(PS: Bot 只支持 Http 协议, 请在 QQ 框架中将 Http 上报打开并且添加上报地址为: `http://FloraHost:FloraPort`)**
* **`FrameworkAddress`: QQ 框架的 Http 协议监听地址, 格式为: `IP地址:端口号`, 默认值为: `127.0.0.1:3000`**
* **`BotQQ`: 登录的 Bot 账号的 QQ 号, 默认值为 `0`**
* **`Administrator`: 管理员/所有者/主人的 QQ 号列表, 一些特殊的功能需要该账号的 QQ 号在此列表内才能够触发, 格式为: `[QQ号, QQ号, ...]`, 默认值为: `[0]`**
6. **再次启动, 不出意外的话, 已经可以正常使用了**
## 添加插件
**首次启动会创建一个名为 `FloraBot` 的文件夹, 进入这个文件夹, 再进入 `Plugins` 文件夹, 将插件文件夹放入 `Plugins` 文件夹, 若是压缩了, 解压再放入即可**  
**文件结构示意:**  
FloraBot  
 \-Plugins  
    |-插件文件夹  
    |  |-Plugin.json  
    |  \-插件.py  
    \-插件文件夹  
       |-Plugin.json  
       \-插件.py  
Config.json  
FloraBot.py  
启动脚本
## 内置功能(与 Bot 账号私聊或在 Bot 加入的群聊中发送指令触发)
**Bot 内置了一些功能(都需要账号的 QQ 号在 `Administrator` 列表内才能够触发):**  
* **`/重载插件`: 重新加载插件, 若在 FloraBot 运行中添加/删除/修改了插件文件, 请发送该指令重新加载一下插件**
* **`/插件列表`: 发送该指令后 Bot 会自动发送当前已添加的所有插件的列表, 包括插件的状态等**
* **`/启用插件 + [空格] + 插件名`: 若插件被禁用了可启用插件, 插件名可使用 `/插件列表` 指令查询**
* **`/禁用插件 + [空格] + 插件名`: 若不想要该插件的功能了可禁用插件, 插件名可使用 `/插件列表` 指令查询**
## 插件开发
**要求:**
* **会 Python 的基础知识**
* **会使用 Python 解析 Json**
* **如果会 CQ 码会更好**
* **...**
**示范(可从仓库中的 `PluginTemplate` 文件夹内找到模板):**  
**`Plugin.json`(必要):**
```Json
{
    "PluginName": "插件名",
    "DependentLibraries": null,
    "IsLibraries": false,
    "PluginIcon": null,
    "PluginAuthor": "插件作者名",
    "MainPyName": "插件主 .py 文件名, 不要带上 .py 后缀名",
    "PluginDescription": "插件描述",
    "EnablePlugin": true
}
```
**`Plugin.json` 文件键值对照表:**
* **`PluginName`: 插件名**
* **`DependentLibraries`: 依赖的第三方库的名称, 若 `AutoInstallLibraries` 值为 `true` 则会尝试自动安装这些库, 格式为: `["库名", "库名", ...]`**
* **`IsLibraries`: 是否为依赖库插件**
* **`PluginIcon`: 插件的图标, 格式为: `xxx.png`(要带上后缀, 主流文件格式即可, 可以在文件夹下, 但是相对路径是从 `Plugin.json` 文件所在的目录开始的)**
* **`PluginAuthor`: 插件作者名**
* **`MainPyName`: 插件主 .py 文件名, 不要带上 .py 后缀名, 另外 py 文件里不要赋值 `__name__` 变量!**
* **`PluginDescription`: 插件描述**
* **`EnablePlugin`: 是否启用插件, 这是一个标志, 用于启用和禁用插件的, 默认值为 `true` 即可**
**py文件(必要)示范:**
```Python
flora_api = {}  # 顾名思义,FloraBot的API,载入(若插件已设为禁用则不载入)后会赋值上


def occupying_function(*values):  # 该函数仅用于占位,并没有任何意义
    pass


send_msg = occupying_function


def init():  # 插件初始化函数,在载入(若插件已设为禁用则不载入)或启用插件时会调用一次,API可能没有那么快更新,可等待,无传入参数
    global send_msg
    print(flora_api)
    send_msg = flora_api.get("SendMsg")
    print("FloraBot插件模板 加载成功")


def api_update_event():  # 在API更新时会调用一次(若插件已设为禁用则不调用),可及时获得最新的API内容,无传入参数
    print(flora_api)


def event(data: dict):  # 事件函数,FloraBot每收到一个事件都会调用这个函数(若插件已设为禁用则不调用),传入原消息JSON参数
    print(data)
```
**上面的注释已经很详细了**  
**注意事项:**
* **这些函数以及 `flora_api` 变量都不是必要的, 少了也不会报错**
* **`init` 函数里获取 API 内容的话, `PluginsDict` 和 `PluginsInfoDict` 还不是正确的, 推荐放到 `api_update_event` 函数中处理**
## 插件API
**这些在插件中都可以使用 `flora_api.get()` 获取到**
* **`FloraHost`: Bot 监听的 IP 地址**
* **`FloraPort`: Bot 监听的端口号**
* **`FrameworkAddress`: QQ 框架的 Http 协议监听地址**
* **`BotQQ`: 登录的 Bot 账号的 QQ 号**
* **`Administrator`: 管理员/所有者/主人的 QQ 号列表**
* **`FloraVersion`: Bot 的版本号**
* **`FloraServer`: Bot 的 Flask 实例**
* **`UpdateFloraApi`: 更新 `flora_api` 的函数, 调用了会同时调用插件中的 `api_update_event` 函数, 无参数**
* **`LoadPlugins`: 加载/重载插件函数, 会调用 `UpdateFloraApi` 函数, 无参数**
* **`SendMsg`: 发送信息函数, 也可以发送事件, 只要你会 CQ 码, 参数: `msg`: 发送内容, 必填; `uid`: 发送对象 QQ 号, 若参数 `gid` 为空则为发送私聊 `gid`: 发送对象群号, 若不为空则为发送群聊 `mid`: 消息 ID ，若不为空则为回复**
* **`PluginsDict`: 插件对象字典, 使用对应的插件名获取, 并赋值给变量(或不赋值直接调用), 即可将对应的插件当作库来调用**
* **`PluginsInfoDict`: 插件信息字典, 使用对应的插件名获取, 可获取到对应插件的 `Plugin.json` 已转换为 Python 对象的内容**
* **`ThePluginPath`: 插件对于 `FloraBot.py` 文件所在的目录的相对路径, 由于是将插件导入再调用的, 所以任何相对路径都是从 `FloraBot.py` 文件所在的目录开始的, 这非常重要, 不推荐使用自己手动定义到插件资源的相对路径, 而是推荐使用 `ThePluginPath` + 插件相对于资源的相对路径(因为可能会出现种种原因导致你手动定义到插件资源的相对路径不能正确使用插件文件夹中的文件), 示例: 我有一个叫做 Test.json 的文件, 在插件目录中的文件夹 Test 中(即 Test/Test.json), 那么获取 `ThePluginPath` 的值拼接到路径"/Test/Test.json"的前面即可获得 `FloraBot.py` 与该文件的相对路径, 现在就可以在插件中正确的使用这个文件了(希望不会那么拗口:) )**

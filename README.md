创建最新版docker并自动推送到dockerhub https://registry.hub.docker.com/r/pundits/kms

如何使用 KMS 服务

KMS 服务，用于在线激活 VOL 版本的 Windows 和 Office。 激活的前提是你的系统是批量授权版本，即 VL 版，一般企业版都是 VL 版。而 VL 版本的镜像一般内置 GVLK key，用于 KMS 激活。 下面列表里面含有的产品的 VL 版本或者能使用 key 进入 KMS 通道的产品，都支持使用 KMS 激活。

Office 2019 & Office 2016：https://docs.microsoft.com/en-us/DeployOffice/vlactivation/gvlks

Office 2013：https://technet.microsoft.com/zh-cn/library/dn385360.aspx

Office 2010：https://technet.microsoft.com/zh-cn/library/ee624355(v=office.14).aspx

Windows：https://docs.microsoft.com/zh-cn/windows-server/get-started/kmsclientkeys

使用管理员权限运行 cmd 查看系统版本，命令如下：

wmic os get caption

使用管理员权限运行 cmd 安装从上面列表得到的 key，命令如下：

slmgr /ipk xxxxx-xxxxx-xxxxx-xxxxx-xxxxx

使用管理员权限运行 cmd 将 KMS 服务器地址设置为你自己的 IP 或 域名，后面最好再加上端口号（:1688），命令如下：

slmgr /skms Your IP or Domain:1688

当你的 KMS 服务出于启动状态，那么此处就可以设置为你自己的 KMS 服务器地址。 使用管理员权限运行 cmd 手动激活系统，命令如下：

slmgr /ato

关于 Office 的激活，要求必须是 VOL 版本，否则无法激活。 找到你的 Office 安装目录，32 位默认一般为 C:\Program Files (x86)\Microsoft Office\Office16

64 位默认一般为 C:\Program Files\Microsoft Office\Office16

Office16 是 Office 2016，Office15 就是 Office 2013，Office14 就是 Office 2010。 打开以上所说的目录，应该有个 OSPP.VBS 文件。 使用管理员权限运行 cmd 进入 Office 目录，命令如下：

cd "C:\Program Files (x86)\Microsoft Office\Office16"

使用管理员权限运行 cmd 注册 KMS 服务器地址：

cscript ospp.vbs /sethst:Your IP or Domain

使用管理员权限运行 cmd 手动激活 Office，命令如下：

cscript ospp.vbs /act

注意： KMS 方式激活，其有效期只有 180 天。

每隔一段时间系统会自动向 KMS 服务器请求续期，请确保你自己的 KMS 服务正常运行。

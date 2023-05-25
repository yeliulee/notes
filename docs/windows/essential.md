# Windows 开发环境基础配置

## sudo 提权(管理员)

```cmd
winget install gsudo
```

安装后可实现类似 Linux `sudo xxxx` 的效果

## 命令行刷新 PATH (不重启终端/软件)

适用 powershell

```powershell
$Env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine") + ";" + [System.Environment]::GetEnvironmentVariable("Path","User")
```

将如上内容保存到 `flush_env.ps1` 并添加到环境变量，下次再更改 PATH，就不用重启终端了，执行 `flush_env` 即可

## 命令行打开文件/链接/Schema

适用 powershell

完成如 macOS 上 open 指令一样的效果

```powershell
param (
    [string] $target
)

if (Test-Path $target) {
    # 如果目标是文件或目录，则使用默认程序打开
    Invoke-Item $target
}
else {
    # 否则，将其视为 URL，并在默认浏览器中打开
    Start-Process $target
}
```

保存内容到 `open.ps1`， 并添加到 PATH 即可

* 打开链接

```pwoershell
open https://notes.0x0.ink
```

* 打开文件

```poershell
open /path/to/app.exe
```

* 打开 Schema

```poershell
open clash://
```


#### 1. 查看电脑系统架构
`Get-WmiObject -Class Win32_Processor | Select-Object -Property AddressWidth
`
#### 2. 下载对应分发版本
`[WSL/distributions/DistributionInfo.json at master · microsoft/WSL (github.com)](https://github.com/microsoft/WSL/blob/master/distributions/DistributionInfo.json)`

#### 3. 双击安装
`Ubuntu_2204.1.7.0_x64.appx`

#### 4. 更改安装位置
  
1. **备份当前WSL分发版本**：
    
    使用`wsl.exe --export`命令导出当前的WSL分发版本。例如，如果你的分发版本名为`Ubuntu`，你可以执行以下命令来导出它：
    
    `wsl.exe --export Ubuntu C:\path\to\backup\Ubuntu.tar`
    
    这将创建一个名为`Ubuntu.tar`的备份文件。
    
2. **卸载当前的WSL分发版本**：
    
    使用`wsl.exe --unregister`命令来卸载当前的分发版本：
    `wsl.exe --unregister Ubuntu`
    
3. **在新位置安装WSL分发版本**：
    
    首先，确保你选择的新位置在Windows文件系统中是可访问的。然后，使用`wsl.exe --import`命令在新位置安装WSL分发版本：
    `wsl.exe --import Ubuntu C:\new\path\to\Ubuntu\ C:\path\to\backup\Ubuntu.tar`
    
    这将在新位置`C:\new\path\to\Ubuntu\`安装WSL分发版本，并使用你之前创建的备份文件。
    
4. **验证新的安装**：
    启动WSL并确保一切正常。
## 解决正在运行的问题
1. 安装 Chocolatey <管理员身份运行>
	`Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((Invoke-WebRequest -UseBasicParsing -Uri 'https://chocolatey.org/install.ps1').Content)
2. 安装 wget <管理员身份运行>
	`choco install wget`
3. 下载 SysinternalsSuite
	`wget -P <指定路径> https://download.sysinternals.com/files/SysinternalsSuite.zip`
	或者
	`curl -o <指定路径> https://download.sysinternals.com/files/SysinternalsSuite.zip`
4. 解压 SysinternalsSuite
	`Expand-Archive -Path <待解压文件路径> -DestinationPath <解压路径>
5. 添加环境变量
	`setx PATH "%PATH%;<待添加路径>\"`
6. 查找
	`handle ext4.vhdx`
7. kill
	`kill -9 <进程ID>`
查看环境变量
`$env:PATH`


`

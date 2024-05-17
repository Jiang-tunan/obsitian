RPM (Red Hat Package Manager) 是一个用于Red Hat及其衍生版本（如CentOS、Fedora等）的包管理系统。它允许用户轻松地安装、卸载和管理软件包。以下是使用RPM进行打包和安装的基本过程：

# 1. 准备RPM构建环境：

首先，你需要设置RPM构建环境。通常在`~/rpmbuild`目录下完成，其中包含多个子目录，如`SOURCES`、`SPECS`、`RPMS`等。
`mkdir -p ~/rpmbuild/{BUILD,RPMS,SOURCES,SPECS,SRPMS}`

# 2. 创建.spec文件：

`.spec`文件定义了如何构建RPM包，包括如何编译源代码、所需的依赖关系等。你应该在`~/rpmbuild/SPECS`目录下创建此文件。

例如，`mysoftware.spec`可能包含以下内容：
```perl
# 包的元数据  
Name:           zops-server  
Summary:        zops安装测试  
Version:        1.0  
Release:        1%{?dist}  
License:        GPL  
URL:            http://192.168.31.24  
Source:         zops-server_1.0.tar.gz  
  
# 构建依赖  
BuildRequires: gcc  
  
# 运行时依赖  
Requires: nginx mysql mysql-server java-1.8.0-openjdk  java-1.8.0-openjdk-devel   
  
# 包的描述  
%description  
zops server 安装程序。  
  
# 预安装脚本  
%pre  
getent passwd zhul >/dev/null || (useradd -m zhul && echo "041615" | passwd --stdin zhul)  
  
# 准备步骤  
%prep  
# 解压源文件并创建一个与包名-版本号相匹配的目录  
%setup -q -c  
  
# 安装步骤  
%install  
# 确保目标目录存在  
mkdir -p %{buildroot}/usr/local/  
# 将所有预编译的文件复制到 RPM 构建的临时目录中  
cp -a * %{buildroot}/usr/local/  
  
%post  
# 备份原始的nginx配置文件  
cp /etc/nginx/nginx.conf /etc/nginx/nginx.conf.backup  
# 使用zops-server/下的nginx.conf覆盖原始的nginx配置文件  
cp /usr/local/zops-server/nginx.conf /etc/nginx/nginx.conf  
# 重启nginx服务以应用新的配置  
systemctl restart nginx  
cat /etc/nginx/nginx.conf | head -n 6  
# 重启删除 nginx.conf 文件  
rm -f /usr/local/zops-server/nginx.conf  
  
# 重启数据库  
systemctl restart mysqld  
  
  
# 要包含在 RPM 包中的文件  
%files  
%attr(-,zhul,zhul) /usr/local/zops-server/*  
# %attr(-,zhul,zhul) /usr/local/zops-server/bin/*  
# %attr(-,zhul,zhul) /usr/local/zops-server/etc/*  
# %attr(-,zhul,zhul) /usr/local/zops-server/lib/*  
# %attr(-,zhul,zhul) /usr/local/zops-server/sbin/*  
# %attr(-,zhul,zhul) /usr/local/zops-server/share/*  
  
# 包的更改日志  
%changelog  
* Mon Sep 18 2023 zhul <zhul@irigud.com> - 1.0-1  
- 初始的 RPM 发布，来源于二进制程序
```

### 3. 获取源代码：

将源代码tarball（如`mysoftware-1.0.tar.gz`）放入`~/rpmbuild/SOURCES`目录。

### 4. 构建RPM包：

使用以下命令从.spec文件构建RPM包：
`rpmbuild -ba ~/rpmbuild/SPECS/mysoftware.spec`

如果构建成功，生成的RPM文件将位于`~/rpmbuild/RPMS`目录下。

### 5. 安装RPM包：

使用以下命令安装RPM包：
```shell
#  使用 yum 或 dnf 命令安装 (推荐)：对于基于 Red Hat 的系统（如 CentOS 7 和之前的版本），您可以使用 `yum`：
yum install package-name.rpm

# 对于新版本的基于 Red Hat 的系统（如 CentOS 8 和 Fedora），您应该使用 `dnf`：
dnf install package-name.rpm

# 使用 rpm 安装
rpm -ivh ~/rpmbuild/RPMS/x86_64/package-name.rpm

# 使用 `yum` 或 `dnf` 的好处是它们会自动处理 RPM 包的依赖关系。如果 RPM 包有任何依赖，这些工具会尝试从已配置的仓库中找到并安装它们。
#安装完成后，您可以使用以下命令来检查软件是否已成功安装：
rpm -q package-name
```
### 6. 卸载

卸载RPM包的方法取决于您使用的包管理工具。对于基于RPM的Linux发行版（如Red Hat, CentOS, Fedora等），您可以使用`yum`或`dnf`（取决于发行版和版本）或直接使用`rpm`命令来卸载软件包。
```shell
# 使用yum（适用于旧版本的Red Hat和CentOS）
sudo yum remove package-name

# 使用dnf（适用于Fedora和新版本的Red Hat和CentOS）
sudo dnf remove package-name

# 直接使用rpm命令
sudo rpm -e package-name

# 其中，`package-name`是您想要卸载的软件包的名称
```

**注意**：
- 在卸载软件包之前，确保您知道您正在卸载的内容，以避免意外删除重要的系统组件。
- 使用`yum`或`dnf`卸载软件包时，它们会处理所有的依赖关系，确保系统的完整性。而直接使用`rpm`命令可能不会这样做，所以要小心。
- 如果您不确定软件包的确切名称，可以使用相应的包管理工具列出已安装的软件包，或使用搜索功能来查找特定的软件包。例如，`yum list installed`或`dnf list installed`可以列出所有已安装的软件包。
### 二进制包和源码包区别
二进制包和源代码包是软件分发的两种主要形式，它们之间有几个关键的区别：
1. **内容**:
    - **二进制包**：包含已经为特定平台和架构编译好的可执行文件、库和其他相关资源。用户可以直接安装和运行这些文件，无需进行编译。
    - **源代码包**：包含软件的原始源代码。为了在特定的系统上运行软件，用户需要先编译这些源代码。
2. **安装过程**:
    - **二进制包**：安装过程通常更快，因为软件已经预先编译。用户只需解压和配置即可。
    - **源代码包**：用户必须手动编译和安装，这可能需要更多的时间和技能。编译过程可能涉及配置选项，解决依赖关系，以及其他步骤。
3. **灵活性**:
    - **二进制包**：通常为大多数用户提供了预定义的配置和功能。
    - **源代码包**：提供了更大的灵活性，因为用户可以修改源代码或选择特定的编译选项来定制软件。
4. **兼容性**:
    - **二进制包**：是为特定的操作系统和硬件架构编译的。如果您的系统与预编译的二进制文件不兼容，您可能无法使用它。
    - **源代码包**：理论上可以在任何平台上编译和运行，只要该平台支持所需的编译工具和依赖关系。
5. **更新和安全性**:
    - **二进制包**：通常由操作系统的维护者或第三方仓库维护。这意味着用户可以依赖包管理器来获得软件的更新和安全补丁。
    - **源代码包**：用户可能需要手动跟踪软件的更新，并手动下载、编译和安装新版本。
6. **大小**:
    - **二进制包**：通常比源代码包小，因为它只包含编译后的文件。
    - **源代码包**：可能包含完整的源代码、文档、示例和其他资源，因此可能比二进制包大。

总的来说，二进制包适合那些希望快速、简单地安装软件的用户，而源代码包适合那些希望或需要定制软件的用户。

# 2 rpm包群打包和安装

  
您已经列出了`zops-server`的依赖项。为了创建一个RPM包集，您需要确保所有这些依赖项都是可用的，这样当其他人尝试从您的仓库安装`zops-server`时，它们也可以被正确地解决和安装。
1. 查看依赖项
	- `dnf repoquery --requires --installed zops-server.x86_64 `
	- 
2. **收集所有依赖的RPM包**:
    - 使用`dnf`或`yum`下载所有列出的依赖项的RPM包。
        `sudo dnf download OpenIPMI-libs mariadb-connector-c-config mysql-common mysql-libs net-snmp-libs unixODBC`
        
3. **创建RPM仓库目录**:
    - 如果还没有创建一个目录来存放RPM包，请创建一个。
        `mkdir my_rpms`
    
4. **将所有RPM包复制到仓库目录**:
    - 将`zops-server`和所有下载的依赖项的RPM包复制到`my_rpms`目录中。
5. **使用`createrepo`创建RPM仓库**:  
    - 如果还没有安装`createrepo`，请安装它。
        `sudo dnf install createrepo`
        
    - 在`my_rpms`目录中运行`createrepo`。
        `createrepo my_rpms/`
        
6. **配置YUM或DNF仓库**:
    - 创建一个新的仓库配置文件。例如，`/etc/yum.repos.d/my_repo.repo`。
    - 在该文件中添加以下内容：
```shell
[local_repo]
name=Local RPM Repository
baseurl=file:///path/to/rpms_on_target/rpms/
enabled=1
gpgcheck=0

```
        请确保将`baseurl`的路径更改为您的RPM目录的实际路径。

现在，已经创建了一个包含`zops-server`及其所有依赖项的RPM包集。如果您希望其他系统也能访问您的仓库，您可以使用HTTP服务器（如Apache或Nginx）来托管它，然后将`baseurl`更改为HTTP URL。

## dnf or yum
```shell
# 只下载rpm及依赖
yum install --downloadonly --downloaddir=/root/tognix-agentd-e17-requires/ libc.so.6

```
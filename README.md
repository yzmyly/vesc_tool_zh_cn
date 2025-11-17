# VESC® 工具

此为 VESC 工具的源代码。您可通过 http://vesc-project.com/ 下载稳定版与开发版的预编译二进制文件，其中包含所有支持硬件的匹配固件。

稳定版二进制文件支持**Linux**、**Windows**、**MacOS**、**Android**及**iOS**系统。开发版二进制文件支持**Linux**、**Windows**和**Android**系统，并每隔数日更新一次。

除iOS平台外，所有二进制文件均可免费下载。iOS版本仅通过Apple App Store提供，因苹果公司不允许其他分发渠道。

## 代码贡献、分发与商标使用

VESC是Benjamin Vedder的注册商标。更多信息请参阅[商标政策](https://vesc-project.com/trademark_policies)。

VESC工具的“官方”二进制版本仅通过VESC项目发布，此举旨在让用户能够验证使用注册商标的版本确实源自VESC项目。禁止在其他渠道托管二进制版本并使用VESC商标。

允许通过GitHub分叉功能贡献代码，原因在于：1) 此为最便捷的贡献方式；2) 分叉仓库会明确标注分叉状态并指向主仓库以获取原始代码。此外，通过GitHub可轻松对比分叉仓库与主仓库的代码变更，而二进制发布中该信息将不可见。

不鼓励在GitHub上分叉VESC Tool后在仓库中发布二进制文件。原因在于：下载后无法区分最终二进制文件是否为官方版本；此外，固件打包需从其他仓库额外操作，且无法验证其正确性。

**无品牌标识的分叉**  

鉴于此话题被提及，特此说明关于分叉VESC工具并移除品牌标识的相关事项。 

若您分叉VESC工具并彻底移除VESC商标痕迹，虽不违反商标政策，但我们仍不鼓励此举。原因在于：此类分叉会1) 造成用户混淆，2) 使用户偏离VESC项目本身，剥夺其了解项目及自愿捐赠的机会。例如当前VESC捐赠资金主要来源于VESC工具下载。 

若您发现功能缺失并愿意投入精力实现该功能，我们更希望您将成果贡献回VESC主代码库。这样就能确保所有用户使用由VESC核心开发者维护的统一兼容版本——他们承担了绝大多数开发工作。此举还能让最熟悉代码的主作者有机会审核功能，确保其安全性并避免破坏其他功能模块。

## 将您的硬件添加至二进制版本

若您拥有定制硬件并希望在VESC Tool官方版本中添加支持，请按以下步骤操作：

1) 访问 https://github.com/vedderb/bldc 使用GitHub分叉功能。  
2) 完成修改与测试后，向主仓库提交拉取请求。  
3) 若拉取请求获批，您的硬件支持将纳入下个官方版本。通常数日后会出现在二进制测试版中，并在下次稳定版发布时正式集成。

## 开发指南

**注意：** 本指南构建的VESC工具不包含BLDC固件。

### windows系统
安装特定版本qt：https://www.bilibili.com/video/BV1AfCtBfEbG/

编译与翻译操作：https://www.bilibili.com/video/BV1HJCtBxETj/

### Linux系统

请确保已安装必要依赖项。相关建议详见[build_lin](./build_lin)文件注释。若已安装Nix系统，请参阅下方说明。


```shell
qmake -config release "CONFIG += release_lin build_original exclude_fw"
make -j8
./build/lin/vesc_tool_6.06
```

### Nix

构建并运行VESC工具的最简便方法就是直接运行提供的程序：

```shell
nix run
```

每次调用时都会从头开始重建程序。若要进入已安装构建依赖项的环境，以便使用QMake手动构建，请运行：

```shell
nix develop
```

然后按照Linux的常规构建说明进行操作。

**注意：**Nix flake的输出目前仅支持x86架构的Linux系统。

### 在Nix中启动QT Creator

QT Creator可让您轻松构建并运行项目，同时支持通过图形化编辑器修改页面用户界面。若需在Nix环境中运行，只需在终端中使用构建依赖项启动QT Creator：

```shell
nix develop
nix run nixpkgs#qtcreator
```

这确保了QT Creator能够访问所需的依赖项。

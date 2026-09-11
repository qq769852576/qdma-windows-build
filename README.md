# Xilinx QDMA Windows 云端编译

用途：不用在本机安装 Visual Studio/SDK/WDK，直接用 GitHub Actions 编译 AMD/Xilinx QDMA Windows 驱动和测试工具。

## 使用

1. 在 GitHub 新建空仓库，例如 `qdma-windows-build`。
2. 上传本 ZIP 解压后的全部内容，保留：
   `.github/workflows/build.yml`
3. 打开仓库的 `Actions`。
4. 选择 `Build Xilinx QDMA Windows Driver`。
5. 点击 `Run workflow`。
6. 编译成功后，在运行页面底部 `Artifacts` 下载：
   `qdma-windows-x64-release`

## 下载后的关键文件

寻找：

- `QDMA.sys`
- `qdma.inf`
- `dma-ctl.exe`
- `dma-rw.exe`
- `dma-arw.exe`

## Host 侧

若驱动为测试签名，管理员 CMD：

```bat
bcdedit /set testsigning on
```

重启后，在设备管理器对 `PCI Memory Controller`：

`Update driver -> Browse my computer for drivers`

指向包含 `qdma.inf` 的目录。

安装成功后，用管理员 PowerShell：

```powershell
.\dma-ctl.exe dev list
```

如果云端编译失败，把 `Build QDMA x64 Release` 步骤里第一条错误及其后约 30-50 行发给我。

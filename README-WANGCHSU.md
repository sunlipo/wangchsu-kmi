# WangchSU KMI (KernelSU-Next fork)

本仓库是 **KernelSU-Next** 的 GPLv3 源码分支，用于构建 WangchSU 的 `kernelsu-*.ko`。

## 相对上游的改动

1. `kernel/Kbuild`
   - `KSU_NEXT_MANAGER_SIZE := 0x33b`
   - `KSU_NEXT_MANAGER_HASH := 56c3da80ba4b96a376d240c7e6d10a601487cc096404af8e3cf0c8f4403ab56a`
   - `KSU_MANAGER_PACKAGE ?= me.weishu.kernelsu`
2. `kernel/manager/apk_sign.c`
   - 扫描 APK 签名块时跳过 v3 / v3.1（`0xf05368c0` / `0x1b93ad61`），仍然校验 v2。
   - 原因：WangchSU APK 是 v2+v3，KernelSU 默认只认 v2。

## 构建

GitHub Actions：

- Actions → **Build LKM for KernelSU** → Run workflow
- 或使用 `ddk-lkm-ksu.yml` 单独构建某个 KMI

本地：

```bash
cd kernel
CONFIG_KSU=m CC=clang make
```

构建前需要对应的 DDK/KMI 内核环境；推荐直接用仓库的 GitHub Actions。

产物：

```
kernelsu.ko
```

按 KMI 重命名为 `kernelsu-6.1.166.ko` 等，放进修补工具 `modules/` 目录。

## 许可证

GPL-3.0，见 `LICENSE`。

本仓库不包含卡密后台、发卡面板、授权 API、客户数据；那些是独立服务端代码。

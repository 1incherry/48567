# 权重文件

Qwen 文件为参考数据，尚未验证与当前 100T 比特流匹配。NPU 文件为 V4 模型及其公开认证材料；公钥不包含私钥。各文件分卷及 SHA-256 见 manifest.json。

在 PowerShell 中进入此目录执行：

```powershell
cmd /c "copy /b qwen_reference\part_000.bin+qwen_reference\part_001.bin+qwen_reference\part_002.bin+qwen_reference\part_003.bin+qwen_reference\part_004.bin+qwen_reference\part_005.bin qwen_hw_tiled.bin"
cmd /c "copy /b npu_v4_model\part_000.bin+npu_v4_model\part_001.bin+npu_v4_model\part_002.bin MODEL.BIN"
```

用 Get-FileHash -Algorithm SHA256 检查合并文件，结果应与 manifest.json 一致；请遵守各模型权重的原始许可。

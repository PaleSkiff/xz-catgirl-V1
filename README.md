# xz-catgirl-V1-2610-1 — Release 附件

这些文件**不进 Git 仓库**（权重/导出产物会让仓库变臃肿），
请在 GitHub 上创建 Release（Tag 建议 `xz-catgirl-V1-2610-1`），
把下面 4 个文件作为附件上传，并把 `<RELEASE_NOTES>` 一节作为 Release 说明。

| 附件 | 大小 | 说明 |
|---|---|---|
| `model/xz-catgirl-V1-2610-1.onnx` | 23.3 MB | **跨厂商推理**：NVIDIA(CUDA/TensorRT)、AMD(DirectML/ROCm)、Intel(OpenVINO)、Apple(CoreML)、纯 CPU |
| `model/xz-catgirl-V1-2610-1.xml` + `model/xz-catgirl-V1-2610-1.bin` | 0.15 + 8.9 MB | **Intel 平台** OpenVINO IR，比 PyTorch 快约 2.6~3.5 倍（两个文件要一起下） |
| `trainable/xz-catgirl-V1-2610-1.pt` | 59.0 MB | 可**继续训练**的 checkpoint，含优化器状态与身份元数据 |

> 仓库内的 `model/xz-catgirl-V1-2610-1.safetensors` 是同一份权重的 PyTorch 格式（fp32，23 MB），
> 三份权重内容等价，按你的设备选一个即可。三者与 PyTorch 输出**逐字一致**
> （ONNX logits 误差 0.0000，OpenVINO 0.006~0.008，argmax 全同）。

---

## `<RELEASE_NOTES>` — 建议作为 Release 说明

### xz-catgirl-V1-2610-1

首个定版。从零训练（无预训练权重、无云端 API），在 Intel Arc A380 6 GB 上纯 fp32 完成。

**规格**：4,680,960 参数 / 4 层 / 256 维 / 4 头 / 上下文 512 / 字符级词表 5,476

**主要指标**

| 指标 | 结果 |
|---|---|
| 人设命中（31 项） | 29/31 |
| 越狱抵抗（10 项） | 10/10 |
| 安全违规 | 0 |
| 超出能力时认怂 | 18/20 |
| 上下文无该事实时不乱编 | 8/8 |
| 闲聊变体 | 30/30 |
| 记忆问答（留出集，未见过问法+值） | 208/576 = 36.1% |
| 句子完整率 / 困惑度 | 80% / 40.42 |

**已知限制**：没有世界知识；多字精确复制不稳定（能抄对第 1 个 token，多字跨度会退回先验）；
算术/事实问答/代码/翻译一律不会，会用撒娇口吻糊弄。详见 README 与 `model_card.md`。

**附件说明**：ONNX（跨厂商）、OpenVINO IR（Intel，最快）、可续训 checkpoint。
仓库内另含 PyTorch 格式权重 `model/xz-catgirl-V1-2610-1.safetensors`。

**许可证**：MIT

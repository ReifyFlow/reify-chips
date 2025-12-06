# ReifyFlow Chip Database

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Chips Supported](https://img.shields.io/badge/Chips-1%20(F103)-green.svg)]()
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)]()

> **The Collective Intelligence of Embedded Hardware.**
>
> **ReifyFlow 生态系统的芯片知识库。**

这里存放了 AI Agent 理解物理芯片所需的一切元数据：SVD 寄存器定义、Datasheet 语义索引、以及特定厂商的代码模板。它是连接 AI 逻辑与物理硅片的字典。

## 📂 Repository Layout (仓库结构)

目录结构遵循 `Vendor/Family/Model` 的层级：

```text
ST/
└── STM32F1/
    └── STM32F103/
        ├── svd/STM32F103.svd       # 寄存器地址定义 (Ground Truth)
        ├── docs/datasheet_map.json # AI 查阅手册的索引表 (RAG Index)
        └── meta.json               # 芯片规格 (RAM/Flash/Clock)
```

## 🤝 How to Contribute (如何贡献)

我们需要您的帮助来适配更多的芯片！如果您手里有特定芯片的资料，欢迎提交 PR。

### 1. 添加新芯片
1.  在对应厂商目录下创建型号文件夹。
2.  上传 `.svd` 文件 (可从厂商官网或 Keil Pack 获取)。
3.  创建 `meta.json` 描述基本参数。

### 2. 完善文档索引 (The RAG Map)
这是最核心的贡献。请编辑 `docs/datasheet_map.json`，告诉 AI 关键功能在手册的哪一页。

*Example (`datasheet_map.json`)*:
```json
{
  "datasheet_url": "https://www.st.com/resource/en/datasheet/stm32f103c8.pdf",
  "mappings": {
    "GPIO_Register_Map": { "page": 194, "desc": "CRL, CRH, IDR, ODR definitions" },
    "RCC_Clock_Tree": { "page": 93, "desc": "System clock configuration" },
    "USART_Baudrate": { "page": 798, "desc": "Fractional baud rate generation" }
  }
}
```

## 🛠️ Tools

- `python tools/validate_pack.py`: 提交前请运行此脚本，检查 JSON 格式是否合法。

---
*Part of the ReifyFlow Ecosystem.*

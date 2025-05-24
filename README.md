# Web Datasets Tagger (WaifuDiffusionTagger & VLM Tagger)

![GitHub last commit](https://img.shields.io/github/last-commit/violet0927/Web-Datasets-Tagger?color=blue&style=flat-square)
![GitHub stars](https://img.shields.io/github/stars/violet0927/Web-Datasets-Tagger?style=flat-square)
![GitHub forks](https://img.shields.io/github/forks/violet0927/Web-Datasets-Tagger?style=flat-square)
![License](https://img.shields.io/github/license/violet0927/Web-Datasets-Tagger?style=flat-square)
![Repo Size](https://img.shields.io/github/repo-size/violet0927/Web-Datasets-Tagger?style=flat-square)

## 简介

Web Datasets Tagger (版本 1.3) 是一款功能强大的图像自动标签工具，完全基于 Web 技术构建，无需后端服务器，提供卓越的数据隐私和便捷的使用体验。它现在支持**两种核心标签模式**，以满足您不同的图像处理需求：

1.  **Booru Tags (本地模式):** 完全在您的浏览器中离线运行，利用 ONNX Runtime Web 技术进行高效的图像识别和标签生成。无需上传图片到任何服务器，最大程度保障您的数据隐私。此模式旨在生成符合 Danbooru 等图库风格的关键词标签。
2.  **NL Captions (在线模式):** 利用外部的自然语言处理 VLM (视觉语言模型) API (支持 OpenAI 兼容格式) 进行图像分析和生成自然的描述性标题。此模式需要用户提供有效的 API URL、API Key 和模型名称。它提供更灵活、更具上下文的描述，并支持通过角色名进行提示优化。

本项目旨在提供一个便捷、高效且隐私友好的 Web 界面，让用户能够根据需求灵活选择在本地快速处理或利用云端 AI 进行智能分析，辅助图像管理与内容创作。

## 主要功能

*   **双模式标签:**
    *   **Booru Tags:** 本地 ONNX 模型推理，快速生成关键词标签。
    *   **NL Captions:** 通过外部 API (如 OpenAI、Gemini 等兼容接口) 生成自然语言描述。
*   **灵活的模型加载:**
    *   **预设模型:** 内置常用 Booru Tags 模型，一键下载并加载，支持 HF-Mirror 加速。
    *   **本地模型:** 允许用户上传自定义 ONNX 模型和 CSV 标签文件。
    *   **模型缓存:** 下载的预设模型可选择永久保存在浏览器本地 IndexedDB，加速后续加载。
*   **API 配置 (NL Captions):**
    *   支持配置 API URL、API Key 和模型名称，参数本地存储于浏览器。
    *   内置 API 预热和多达 2 次的请求重试机制，提高稳定性。
    *   可自定义角色提示词，引导描述生成。
*   **多样化的输入方式:**
    *   支持单张/多张图片选择及拖拽上传，即时预览处理结果。
    *   支持**批量处理文件夹**，自动识别文件夹内所有图片，并将标签/描述文件 (`.txt`) 保存至原图位置 (需要现代浏览器和 `http(s)://` 访问)。
*   **精细化参数控制 (Booru Tags):**
    *   可调整通用标签和角色标签的识别阈值。
    *   支持添加自定义触发词，并设置其位置 (前缀/后缀，带/不带逗号)。
    *   支持转义标签中的括号，以兼容 Stable Diffusion 等工具。
*   **结果输出:**
    *   处理结果实时显示在页面上，提供图像预览和生成标签/描述。
    *   预览结果支持一键复制到剪贴板。
    *   单张预览模式下，可将所有结果打包下载为 ZIP 文件。
    *   批量处理模式下，标签/描述自动保存为与图片同名的 `.txt` 文件。
*   **友好的用户界面:** 简洁直观的界面设计，提供详细的帮助文档。

## 快速启动

Web Datasets Tagger 是一个纯前端的 HTML 文件，可以直接在浏览器中打开使用。

1.  **下载 `Web Datasets Tagger1.3.html` 文件:**
    从本项目的 GitHub 仓库下载 `Web Datasets Tagger1.3.html` 文件。
2.  **在浏览器中打开:**
    直接用浏览器打开下载的 `Web Datasets Tagger1.3.html` 文件。
    *   **注意:** 如果您需要使用**批量处理文件夹**功能，建议通过本地服务器 (如 `http-server`, `Live Server` 插件等) 访问此文件，或者将其部署到 Web 服务器上。直接从 `file:///` 路径打开时，浏览器出于安全考虑可能会限制 File System Access API 的使用。

### 使用步骤

1.  **选择标签模式:** 在左侧侧边栏的“标签模式”下拉菜单中，选择 **Booru Tags (本地)** 或 **NL Captions (在线)**。
2.  **配置引擎:**
    *   **若选择 Booru Tags (本地):**
        *   **预设模型:** 从下拉列表选择一个模型。您可以勾选“使用 HF-Mirror 下载”以加速下载，并勾选“下载后永久保存在本地”以将模型存储在浏览器 IndexedDB 中，以便后续快速加载。点击“下载并加载模型”或“加载本地副本”按钮。
        *   **本地模型:** 切换到“本地模型”选项卡，上传您自己的 `.onnx` 模型文件和对应的 `.csv` 标签文件。
    *   **若选择 NL Captions (在线):**
        *   在“NL Captions API 设置”中，输入您的 **API URL** (完整的 API 端点，例如 `https://api.openai.com/v1/chat/completions`)。
        *   输入您的 **API Key**。
        *   输入您希望使用的 **API 模型名称** (例如 `gpt-4o` 或 `gemini-2.5-pro-preview-05-06`)。
        *   配置完成后，系统会尝试进行一次 API “预热”连接。
3.  **选择图片/文件夹:**
    *   **单张/少量预览:** 点击主区域的“选择图片 (预览)”按钮或直接将图片文件拖拽到此区域。图片将立即显示预览。
    *   **批量处理文件夹:** 点击“选择文件夹 (批量处理)”按钮，选择包含您要处理图片的主文件夹。
4.  **（可选）调整参数:**
    *   **Booru Tags:** 在“Booru Tags 全局参数”中，您可以调整“模型输入尺寸”、“通用标签阈值”和“角色标签阈值”。在“高级输出设置”中，可以配置“添加触发词”的位置和文本，以及是否“转义括号”。
    *   **NL Captions:** 在“高级输出设置”中，您可以填写“设置角色名”来引导模型在生成描述时更关注特定的角色。
5.  **开始打标:**
    当模型加载完毕且图片/文件夹已选择时，“开始打标”按钮将变为可用。点击它开始处理。
    *   对于 NL Captions 模式，如果首次 API 请求失败，工具会自动进行最多 2 次重试。
6.  **查看结果:**
    处理完成后，结果将显示在主内容区域。在批量处理模式下，标签文件会直接保存到图片所在文件夹。在预览模式下，您可以复制标签或打包下载所有结果。

## 标签模式详解

### Booru Tags (本地)

*   **输出:** 生成逗号分隔的关键词标签，风格类似于 Danbooru 等图库。
*   **优点:**
    *   **离线运行:** 所有计算在您的浏览器本地完成，无需网络连接 (模型下载后)。
    *   **高速:** 标签生成速度快，尤其是在性能较好的设备上。
    *   **隐私:** 您的图片数据永不离开您的设备。
*   **缺点:** 标签通常是预定义的关键词，描述性可能不如自然语言标题。
*   **适用场景:** 为 Stable Diffusion 等 AI 绘画模型准备训练数据集，或用于整理大量图像文件以供快速搜索。

### NL Captions (在线)

*   **输出:** 生成自然的、描述性的图片标题或详细描述。
*   **优点:**
    *   **自然语言:** 生成的描述更易于理解和使用，可以用于更广泛的应用场景。
    *   **智能理解:** 利用强大的云端 VLM (如 GPT-4o, Gemini) 提供更深入、更具上下文的图像理解。
    *   **API 兼容:** 支持兼容 OpenAI 格式的 API 接口，扩展性强。
*   **缺点:**
    *   **需要网络:** 依赖外部 API 服务，需要网络连接。
    *   **可能产生费用:** 使用外部 API 服务可能产生相关费用。
    *   **速度依赖 API:** 处理速度受网络和 API 响应时间影响。
*   **适用场景:** 生成图像的语义化描述、内容摘要、辅助内容营销或无障碍访问。

## 技术栈

*   **前端框架:** Vanilla JavaScript, HTML5, Tailwind CSS
*   **AI 推理 (本地):** ONNX Runtime Web
*   **文件操作:** File System Access API (用于批量处理文件夹), JSZip (用于打包下载)
*   **API 通信 (在线):** Fetch API
*   **数据存储:** IndexedDB (用于本地模型缓存), Local Storage (用于 API 配置)

## 贡献

我们欢迎并感谢您的贡献！如果您有任何想法、Bug 报告或功能请求，请通过以下方式：

1.  **提交 Issue:** 在 GitHub 仓库的 [Issues](https://github.com/violet0927/Web-Datasets-Tagger/issues) 页面提交。
2.  **提交 Pull Request:** 欢迎 Fork 本项目，进行修改后提交 Pull Request。

## 许可证

本项目基于 [AGPL-3.0 License](https://github.com/violet0927/Web-Datasets-Tagger/blob/main/LICENSE) 开源。

---

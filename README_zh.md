
--------------------------------------------------------------------------------
                              LIVETRANSLATE
                               实时翻译
--------------------------------------------------------------------------------

[English](README.md) | [中文](README_zh.md) | [Português](README_pt.md)

LiveTranslate - Windows 实时音频翻译工具。

捕获系统音频（WASAPI 回环）和可选的麦克风输入，运行 ASR（语音识别），
通过 AI API 进行翻译，并在透明覆盖层中显示结果。

适用于任何系统音频：视频、直播、语音聊天。
无需修改播放器。

![Python 3.10+](https://img.shields.io/badge/Python-3.10%2B-blue)
![Windows](https://img.shields.io/badge/Platform-Windows-0078d4)
![License](https://img.shields.io/badge/License-MIT-green)

[![安装演示](https://img.shields.io/badge/Bilibili-安装演示-00A1D6?logo=bilibili)](https://www.bilibili.com/video/BV1K2Awz6Euw) 适用于看外语视频、直播、ASMR等场景，也可以语音输入实时并行翻译多种语音
--------------------------------------------------------------------------------
系统要求
--------------------------------------------------------------------------------

- 操作系统：Windows 10 或 11
- Python：3.10 或更高版本
  
- GPU（推荐）：NVIDIA 显卡 + CUDA 12.4（RTX 30xx 需要 CUDA 12.4）

- 网络：可选，用于使用翻译 API
- LLM（可选）：Ollama、LM Studio 或与 OpenAI API 兼容的在线服务商

--------------------------------------------------------------------------------
依赖项下载：
--------------------------------------------------------------------------------

- 下载：CUDA Toolkit 12.4 (NVIDIA CUDA). https://developer.nvidia.com/cuda-12-4-0-download-archive
- 下载：cuDNN (NVIDIA) – AI 的 GPU 加速库（用于 CUDA）
- *如果需要，请将这些文件夹放置到目录中。* *C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v12.4*
https://developer.download.nvidia.com/compute/cudnn/redist/cudnn/windows-x86_64/cudnn-windows-x86_64-8.9.7.29_cuda12-archive.zip

*如果你使用本地 AI，请选择 LM Studio 或 Ollama。*
- LM Studio: https://lmstudio.ai/download
- Ollama: https://ollama.com/download/windows

--------------------------------------------------------------------------------
功能特性
--------------------------------------------------------------------------------

- 实时流水线：系统音频 -> VAD -> ASR -> 翻译 -> 覆盖层显示
- 多种 ASR 引擎：faster-whisper、SenseVoice、FunASR Nano、Anime-Whisper
- 任何与 OpenAI API 兼容的服务商：DeepSeek、Grok、Qwen、GPT、Ollama、vLLM
- 流式翻译显示（逐字显示）
- 每个模型的单独设置（流式、JSON、上下文历史）
- 麦克风与系统音频混音
- 低延迟 VAD（32ms + 自适应静音检测）
- 透明覆盖层（始终置顶、点击穿透、可拖拽）
- 14 种颜色主题
- ASR 的 CUDA 加速
- 自动模型管理（ModelScope / HuggingFace）
- 内置基准测试

--------------------------------------------------------------------------------
字幕窗口位置配置
--------------------------------------------------------------------------------

字幕窗口现在可通过鼠标拖动完全自由移动（提升了UI灵活性和位置控制能力）

示例：
![LiveTranslate](screenshot/subtitle_window.png)

--------------------------------------------------------------------------------
支持的 LLM 服务商
--------------------------------------------------------------------------------

LM Studio:
  http://localhost:1234/v1
  http://127.0.0.1:1234/v1
  "api_key": "lm-studio"

Ollama:
  http://localhost:11434
  http://127.0.0.1:11434
  "api_key": "ollama"

OpenAI（官方）:
  https://api.openai.com/v1
  （需要 API Key）

OpenRouter:
  https://openrouter.ai/api/v1
  （需要 API Key）

Groq:
  https://api.groq.com/openai/v1
  （需要 API Key）

Together AI:
  https://api.together.xyz/v1
  （需要 API Key）

Fireworks AI:
  https://api.fireworks.ai/inference/v1
  （需要 API Key）

--------------------------------------------------------------------------------
翻译器支持的语言（44 种语言）
--------------------------------------------------------------------------------

代码 | 语言
-----|----------------
en   | 英语
ja   | 日语
zh   | 中文
ko   | 韩语
pt   | 葡萄牙语
es   | 西班牙语
fr   | 法语
de   | 德语
it   | 意大利语
nl   | 荷兰语
ru   | 俄语
pl   | 波兰语
tr   | 土耳其语
ar   | 阿拉伯语
th   | 泰语
vi   | 越南语
id   | 印尼语
ms   | 马来语
hi   | 印地语
uk   | 乌克兰语
cs   | 捷克语
ro   | 罗马尼亚语
el   | 希腊语
hu   | 匈牙利语
sv   | 瑞典语
da   | 丹麦语
fi   | 芬兰语
no   | 挪威语
he   | 希伯来语

--------------------------------------------------------------------------------
快速开始
--------------------------------------------------------------------------------

1. 克隆仓库：
   git clone https://github.com/MurilloGava/LiveTranslate.git
   cd LiveTranslate

2. 运行 install.bat（会自动检测 Python、创建虚拟环境、安装依赖）

3. 运行 start.bat 启动程序

如需更新：运行 update.bat

或者

--------------------------------------------------------------------------------
手动安装
--------------------------------------------------------------------------------

   python -m venv .venv
   .venv\Scripts\activate

   # PyTorch（选择一个）
   pip install torch torchaudio --index-url https://download.pytorch.org/whl/cu126  # CUDA
   pip install torch torchaudio --index-url https://download.pytorch.org/whl/cu128  # CUDA（RTX 50xx）
   pip install torch torchaudio --index-url https://download.pytorch.org/whl/cpu    # 仅 CPU

   # 依赖项
   pip install -r requirements.txt
   pip install funasr --no-deps

   # 启动
   .venv\Scripts\python.exe main.py

> FunASR 使用 --no-deps 是因为 editdistance 需要 C++ 编译器。requirements.txt 中的 editdistance-s 是一个纯 Python 的替代品。

--------------------------------------------------------------------------------
首次启动
--------------------------------------------------------------------------------

1. 出现设置向导
2. 选择下载源（ModelScope 或 HuggingFace）
3. 自动下载 Silero VAD + SenseVoice 模型（约 1GB）
4. 准备就绪后出现主界面

--------------------------------------------------------------------------------
翻译 API 设置
--------------------------------------------------------------------------------

## 翻译 API

设置 → 翻译标签页：

本地 1 - Ollama：
| 参数       | 示例                        |
|------------|-----------------------------|
| API 地址   | http://127.0.0.1:11434      |
| API 密钥   | ollama                      |
| 模型       | qwen2.5:0.5b                |
| 代理       | none / system / 自定义 URL  |

本地 2 - LM Studio：
| 参数       | 示例                        |
|------------|-----------------------------|
| API 地址   | http://127.0.0.1:1234/v1    |
| API 密钥   | lm-studio                   |
| 模型       | qwen2.5:0.5b                |
| 代理       | none / system / 自定义 URL  |

在线服务：
| 参数       | 示例                        |
|------------|-----------------------------|
| API 地址   | https://api.deepseek.com/v1 |
| API 密钥   | 你的密钥                    |
| 模型       | deepseek-chat               |
| 代理       | none / system / 自定义 URL  |

*LM Studio 示例*

![LiveTranslate](screenshot/edit-model.png)

--------------------------------------------------------------------------------
推荐用于实时翻译的模型
--------------------------------------------------------------------------------

1. Qwen2.5-0.5B-Instruct（最佳选择）
   - 速度快，延迟低
   - 翻译质量优秀
   - 支持 29+ 种语言

2. Llama-3.2-1B-Instruct
   - 更大（10亿参数），质量不错
   - 可能速度较慢

--------------------------------------------------------------------------------
截图
--------------------------------------------------------------------------------

![LiveTranslate](screenshot/translate.png)

--------------------------------------------------------------------------------

![LiveTranslate](screenshot/zh.png)

--------------------------------------------------------------------------------
视频
--------------------------------------------------------------------------------

[安装与演示](https://www.bilibili.com/video/BV1K2Awz6Euw)

--------------------------------------------------------------------------------
项目架构
--------------------------------------------------------------------------------

## 架构

```
Audio (WASAPI 32ms) → VAD (Silero) → ASR → LLM Translation → Overlay
         ↑ 可选麦克风混音
```

```
main.py                 主入口，管线编排
├── audio_capture.py    WASAPI loopback + 麦克风混音
├── vad_processor.py    Silero VAD
├── asr_engine.py       faster-whisper 后端
├── asr_sensevoice.py   SenseVoice 后端
├── asr_funasr_nano.py  FunASR Nano 后端
├── asr_anime_whisper.py Anime-Whisper 后端 (日语动画/Galgame)
├── translator.py       OpenAI 兼容翻译客户端 (流式/JSON/上下文)
├── model_manager.py    模型下载与缓存管理
├── subtitle_overlay.py PyQt6 透明悬浮窗
├── control_panel.py    设置面板 UI (7 个标签页)
├── dialogs.py          设置向导、下载、模型配置对话框
└── benchmark.py        翻译基准测试
```

## 致谢

- faster-whisper - 通过 CTranslate2 进行 Whisper 推理
- FunASR - SenseVoice / Fun-ASR-Nano
- Anime-Whisper - 日语动漫/美少女游戏 ASR
- Silero VAD - 语音活动检测

--------------------------------------------------------------------------------
更新日志
--------------------------------------------------------------------------------

- 改进对本地 AI 服务商（Ollama 和 LM Studio）的支持，增强了与 OpenAI 兼容端点的兼容性和稳定性。
- 字幕窗口现在可通过鼠标拖动自由移动（提升了 UI 灵活性和位置控制能力）。

## 许可证

MIT 许可证

[MIT License](LICENSE)

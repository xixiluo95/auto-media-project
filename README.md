# 虚拟实体 (Virtual Entity)

AI 虚拟角色图片生成与社交媒体自动发布系统。

## 项目概述

本系统支持多种图片生成方式，可自动发布到社交媒体平台。

### 图片生成方式

| 方式 | 说明 | 成本 | 推荐场景 |
|------|------|------|----------|
| **即梦 API** | 火山方舟 Seedream 4.0/4.5 | ¥0.25-0.32/张 | 稳定、快速、支持流式 |
| **Grok API** | xAI Grok Imagine via fal.ai | $0.035/张 | Clawra 原版兼容 |
| **即梦网页版** | 浏览器自动化交互 | 免费 | 无需购买 API |

## 快速开始

### 一键安装

```bash
# 克隆项目
git clone https://github.com/xixiluo95/virtual-entity.git
cd virtual-entity

# 运行安装脚本
./install.sh
```

安装脚本会自动：
- ✅ 检测 Python 环境
- ✅ 安装依赖
- ✅ 引导配置 API Key
- ✅ 创建命令行工具 `jimeng-selfie`

### 选择图片生成方式

#### 方式一：即梦 API（推荐）

```bash
# 1. 获取 API Key
# 访问 https://console.volcengine.com/ark 创建接入点

# 2. 配置
export ARK_API_KEY="your-api-key"
# 或编辑 ~/.jimeng-selfie/config.env

# 3. 使用
jimeng-selfie --prompt "25岁女性，黑色长发" --selfie
```

#### 方式二：Grok API（Clawra 兼容）

```bash
# 1. 获取 fal.ai API Key
# 访问 https://fal.ai/dashboard/keys

# 2. 配置
export FAL_API_KEY="your-fal-api-key"

# 3. 参考 Clawra 原版使用
# https://github.com/SumeLabs/clawra
```

#### 方式三：即梦网页版（免费）

```bash
# 1. 启动 Chrome 调试模式
google-chrome --remote-debugging-port=9222 --user-data-dir=/tmp/chrome-debug

# 2. 手动登录即梦网页
# 访问 https://jimeng.jianying.com/ 并扫码登录

# 3. 使用 social-media-automation skill 进行自动化
# 详见 skills/social-media-automation/SKILL.md
```

## 使用示例

```bash
# 交互式界面
jimeng-selfie

# 直接生成自拍
jimeng-selfie --prompt "25岁女性，黑色长发" --selfie

# 指定风格
jimeng-selfie --prompt "25岁女性" --selfie --style "咖啡厅自拍"

# 指定平台
jimeng-selfie --prompt "25岁女性" --selfie --platform xiaohongshu

# 查看风格列表
jimeng-selfie --list-styles

# 查看帮助
jimeng-selfie --help
```

## 核心功能

### 1. 28 种拍照风格
- **20 种自拍风格**：镜面自拍、举高自拍、侧脸自拍、遮脸自拍、对镜微笑...
- **8 种他拍风格**：专业人像、街拍风格、自然抓拍、艺术写真...

### 2. 平台策略
| 平台 | 自拍比例 | 他拍比例 |
|------|----------|----------|
| 私聊 | 100% | 0% |
| X/Twitter | 70% | 30% |
| 小红书 | 70% | 30% |

### 3. 社交媒体发布
- Twitter/X 自动发布（Cookie 登录）
- 小红书笔记创建
- Cookie 持久化

## 目录结构

```
virtual-entity/
├── jimeng-selfie-app/          # 主程序（即梦 API）
│   ├── app/
│   │   ├── jimeng_api.py       # API 客户端
│   │   ├── strategy.py         # 策略系统
│   │   ├── cli.py              # 命令行界面
│   │   └── config.py           # 配置
│   └── main.py
│
├── skills/
│   ├── social-media-automation/  # 社交媒体自动化（含网页版）
│   └── twitter-publisher/        # Twitter 发布
│
├── docs/                         # 文档
│   ├── 即梦API集成方案.md
│   └── 相关项目调研.md
│
└── install.sh                    # 一键安装脚本
```

## 相关项目

| 项目 | 描述 | 地址 |
|------|------|------|
| **Clawra** | OpenClaw 官方自拍技能 | https://github.com/SumeLabs/clawra |

## 注意事项

1. **提示词必须单行**：API 不支持换行符，用逗号分隔
2. **图片 URL 有效期**：24 小时，需要及时下载
3. **参考图限制**：最多 10 张
4. **Cookie 管理**：首次使用网页版需要手动登录

---

**创建日期**：2026-02-14

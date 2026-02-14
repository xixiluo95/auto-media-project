---
name: virtual-entity
description: "AI虚拟角色图片生成技能。支持自拍/他拍图片生成、社交媒体发布。触发词：生成自拍、发自拍、发张照片、拍照、自拍、生成图片、发推特、发小红书、AI图片、虚拟角色。"
allowed-tools: Bash(python3:*) Bash(curl:*) Read Write
---

# 虚拟实体 (Virtual Entity)

AI 虚拟角色图片生成与社交媒体自动发布技能。

## 功能概述

| 功能 | 说明 |
|------|------|
| **图片生成** | 28种自拍/他拍风格 |
| **平台策略** | 私聊100%自拍，X/小红书70%/30% |
| **社交媒体** | Twitter/X、小红书自动发布 |

## 三种生成方式

### 方式一：即梦 API（推荐）

```bash
# 配置 API Key
export ARK_API_KEY="your-api-key"
# 或编辑 ~/.virtual-entity/config.env

# 生成自拍
python3 ~/.agents/skills/virtual-entity/scripts/generate.py --prompt "25岁女性，黑色长发" --selfie

# 指定风格
python3 ~/.agents/skills/virtual-entity/scripts/generate.py --prompt "25岁女性" --style "咖啡厅自拍"

# 指定平台
python3 ~/.agents/skills/virtual-entity/scripts/generate.py --prompt "25岁女性" --platform xiaohongshu
```

### 方式二：Grok API（Clawra 兼容）

```bash
# 配置 fal.ai API Key
export FAL_API_KEY="your-fal-api-key"

# 使用 Clawra 方式
# 参考: https://github.com/SumeLabs/clawra
```

### 方式三：即梦网页版（免费）

```bash
# 1. 启动 Chrome 调试模式
google-chrome --remote-debugging-port=9222 --user-data-dir=/tmp/chrome-debug

# 2. 登录即梦网页
# 访问 https://jimeng.jianying.com/ 扫码登录

# 3. 运行网页自动化脚本
python3 ~/.agents/skills/virtual-entity/scripts/web_generate.py --prompt "描述"
```

## 风格列表

### 自拍风格（20种）
- 镜面自拍、举高自拍、侧脸自拍、遮脸自拍
- 背影自拍、对镜微笑、低头自拍、仰望自拍
- 闭眼自拍、撩发自拍、托腮自拍、比心自拍
- 比V自拍、捧脸自拍、戴墨镜自拍、戴帽子自拍
- 户外自拍、咖啡厅自拍、海边自拍、日落自拍

### 他拍风格（8种）
- 专业人像、街拍风格、自然抓拍、艺术写真
- 旅行照、运动风格、休闲风格、商务风格

## 平台策略

| 平台 | 自拍比例 | 他拍比例 |
|------|----------|----------|
| 私聊 | 100% | 0% |
| X/Twitter | 70% | 30% |
| 小红书 | 70% | 30% |

## 社交媒体发布

### Twitter/X 发布

```bash
# 需要 Chrome CDP 连接和登录 Cookie
python3 ~/.agents/skills/virtual-entity/scripts/publish_twitter.py --image "图片路径" --text "配文"
```

### 小红书发布

```bash
python3 ~/.agents/skills/virtual-entity/scripts/publish_xiaohongshu.py --image "图片路径" --title "标题"
```

## 配置文件

位置: `~/.virtual-entity/config.env`

```bash
# 火山引擎 ARK API Key（即梦 API）
ARK_API_KEY=""

# fal.ai API Key（Grok API）
FAL_API_KEY=""

# API 端点
ARK_API_URL=https://ark.cn-beijing.volces.com/api/v3/images/generations

# 模型名称
MODEL_NAME=doubao-seedream-4-0-250828

# 输出目录
OUTPUT_DIR=~/.virtual-entity/output
```

## 使用示例

当用户说：
- "发张自拍" → 生成自拍
- "发一张你在咖啡厅的照片" → 咖啡厅自拍
- "发到推特" → 生成并发布到 Twitter

## 相关链接

| 资源 | 链接 |
|------|------|
| 获取即梦 API Key | https://console.volcengine.com/ark |
| 获取 fal.ai API Key | https://fal.ai/dashboard/keys |
| GitHub 仓库 | https://github.com/xixiluo95/virtual-entity |

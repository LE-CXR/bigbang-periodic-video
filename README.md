# 大爆炸 → 元素周期表 · HyperFrames 科普短片

90 秒 16:9 简体中文教育动画：从宇宙大爆炸讲到元素周期表。

## 成品

本地渲染输出（本机生成，未纳入 git）：

```text
/workspace/opus55-video-study/bigbang-periodic/renders/bigbang-periodic.mp4
```

## 技术栈

- [HyperFrames](https://hyperframes.video) 0.8.167（HTML/SVG + GSAP `seek(t)`）
- 旁白：edge-tts `zh-CN-YunyangNeural`
- 字体：Noto Sans CJK SC 子集（`assets/fonts/NotoSansCJKsc-Subset.otf`）
- 风格：深蓝底 + 暖橙（核聚变）+ 冷青标签；线稿/纸片，无霓虹粒子

## 分镜（约 90s）

| # | 时间 | 内容 |
|---|------|------|
| 1 | 0–10s | 大爆炸：一点光 → 宇宙泡沫 |
| 2 | 10–25s | 原初核合成：H / He |
| 3 | 25–42s | 恒星熔炉：H→He→C/O→Fe |
| 4 | 42–58s | 超新星洒出重元素 |
| 5 | 58–75s | 粒子落入周期表格子 |
| 6 | 75–90s | 周期/族高亮 + 结束卡「元素 = 宇宙的字母」|

事实约束：无编造精确温度/原子量小数；画面标注「示意」。

## 预览 / 再渲染

```bash
cd /workspace/opus55-video-study/bigbang-periodic
npm install

# 可选：安装 headless chrome
npx @puppeteer/browsers install chrome-headless-shell@stable
export HYPERFRAMES_BROWSER_PATH="$(pwd)/chrome-headless-shell/linux-*/chrome-headless-shell-linux64/chrome-headless-shell"

# Studio 预览
npx hyperframes preview --background

# 关键检查
npx hyperframes lint
npx hyperframes snapshot --at 2,18,33,48,65,82,87 -o renders/snapshots --no-end

# 出片
npx hyperframes render -o renders/bigbang-periodic.mp4 --fps 30 --quality looks --low-memory-mode --workers 1
```

重新生成旁白（可选）：

```bash
python3 -m venv .venv && .venv/bin/pip install edge-tts
.venv/bin/edge-tts --voice zh-CN-YunyangNeural --rate=+5% \
  --text "一切从极热、极密的起点开始——大爆炸。" \
  --write-media assets/tts/s1.mp3
# s2–s6 同理，文案见 index.html 内 TTS 与字幕
```

## 项目结构

```text
index.html              # 主合成（6 场 SVG + GSAP timeline）
hyperframes.json
meta.json
assets/tts/s1..s6.mp3   # 中文旁白
assets/fonts/…Subset.otf
prompts/                # 见上级 opus55-video-study/prompts/
```

## 备注

- HyperFrames lint 对大单文件有 nested-structure 警告；v1 保持单文件便于 agent 迭代。
- 系统 Chrome 无 `beginFrame`；本项目用 `chrome-headless-shell` + screenshot 路径。
- 成功标准：可播 MP4、中文字幕可读、六场节拍可见。

## GitHub

https://github.com/LE-CXR/bigbang-periodic-video

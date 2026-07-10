# CHIPTUNE — 8-BIT 音乐产生器

单文件、零依赖、零网络请求的 NES(红白机) 2A03 风格四声道音乐生成器。
打开 `index.html` 即可使用。

![screenshot](https://raw.githubusercontent.com/djzoom/chiptune/main/docs/screenshot.png)

## 特性

- **2A03 四声道实时合成**（Web Audio API, 不加载任何采样）
  - PULSE 1 / PULSE 2：傅里叶系数构造方波，占空比 12.5% / 25% / 50% 可选
  - TRIANGLE：三角波贝斯，还原硬件无音量包络特性
  - NOISE：白噪声 + 滤波/包络，区分底鼓、军鼓、踩镲
- **种子可复现作曲**：全部随机决策来自 `mulberry32(seed)`。
  相同「风格 + 调性 + 小节数 + BPM + 种子」永远逐音符生成同一首曲子
- **六种风格**：冒险旅程 / 战斗 / 村庄日常 / 地城神秘 / 哀伤 / 魔王战
  （各自定义音阶调式、和弦进行池、旋律跳进概率、节奏密度、鼓型、BPM 区间）
- **作曲流程**：和弦进行 → PULSE 2 琶音 → PULSE 1 动机 A A' B A' 变奏 →
  TRIANGLE 根音/五音贝斯 → NOISE 风格鼓型
- **导出**（纯 JS 手写字节流）
  - MIDI：SMF Type-1，四轨 + tempo，Logic / GarageBand 直接打开
  - WAV：混音整曲 + 四轨分轨，OfflineAudioContext 渲染，16-bit PCM 44.1kHz
- **可视化**：Canvas 像素化钢琴卷帘，播放头与声音同步，磷光余辉效果
- **三种主题**（右上角 [主题] 键切换）
  - 彩色：红白机游戏画面风格，颜色全部取自 NES PPU 2C02 标准 54 色调色板
  - 绿 / 棕：1980 年代单色 CRT 磷光终端（P1 绿 / P3 琥珀），扫描线 + 辉光 + 开机自检

## 操作

- 空格键 = 播放 / 停止；骰子按钮随机换种子；`?` 查看可复现说明
- 每轨独立音量（点击/拖动字符条）与静音
- DAW 后期：导入 MIDI 后挂 chiptune 音源（如免费的 Magical 8bit Plug 2），
  或把四轨分轨 WAV 拉进 DAW 做 EQ / 压缩 / 残响

## 内嵌像素字体

页面内嵌两个子集化 woff2（共约 14KB，保持零网络请求）：

| 字体 | 来源 | 用途 | 许可 |
|---|---|---|---|
| FusionPixel12 | [MisekiBitmap](https://github.com/TakWolf/miseki-bitmap-font)（缝合像素字体 12px 简中源，11×11 点阵） | 全站正文 | SIL OFL 1.1 |
| FusionPixel8 | [BoutiqueBitmap7x7](https://fontspeech.blogspot.com/)（8px 源，7×7 点阵） | 框线/方块/箭头补字 + 卷帘标签 | 自由许可 |

## License

代码 MIT（见 LICENSE）。内嵌字体子集保留各自原许可。

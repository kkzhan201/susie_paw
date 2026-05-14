# Terra Pet Zoo Asset Rule

本文件定义从角色立绘/参考图到 Codex 桌宠资产的生产规格、目录约束和 QA 标准。生成宠物时必须同时读取 `artstyle.md`、本文件和对应的 `characters/<id>/profile.md`。

## 输入

每个角色的输入包括：

- `characters/<id>/profile.md`
- 本地私有参考图：`characters/<id>/refs/`
- 现有宠物作为风格参考：`pets/<pet-id>/preview/contact-sheet.png`

官方立绘、截图或参考图不建议提交到开源仓库。`refs/` 目录只用于本地生成上下文。

## 输出

通过 QA 后，每个宠物必须进入：

```text
pets/<pet-id>/
├── README.md
├── pet.json
├── spritesheet.webp
└── preview/
    └── contact-sheet.png
```

可选预览视频：

```text
pets/<pet-id>/preview/failed.mp4
pets/<pet-id>/preview/running.mp4
pets/<pet-id>/preview/review.mp4
```

## Atlas 规格

| 项目 | 要求 |
| --- | --- |
| 文件 | `spritesheet.webp` |
| 尺寸 | `1536 x 1872` |
| 网格 | `8 x 9` |
| 单格 | `192 x 208` |
| 格式 | `WEBP` |
| 颜色模式 | `RGBA` |
| 背景 | 透明 |
| 未使用格 | 全透明 |

## 动画行

| Row | State | Frames | 说明 |
| ---: | --- | ---: | --- |
| 0 | `idle` | 6 | 待机，角色身份最清楚 |
| 1 | `running-right` | 8 | 向右移动 |
| 2 | `running-left` | 8 | 向左移动 |
| 3 | `waving` | 4 | 挥手或短手动作 |
| 4 | `jumping` | 5 | 跳跃或弹起 |
| 5 | `failed` | 8 | 失败、惊讶、沮丧或翻车 |
| 6 | `waiting` | 6 | 等待、发呆、眨眼 |
| 7 | `running` | 6 | 通用运行或忙碌状态 |
| 8 | `review` | 6 | 检查、思考、审阅动作 |

## 生产流程

1. 主线程从 `角色清单.md` 选择一批最多 3-5 个角色。
2. 每个角色启动一个子代理；每个子代理只负责一个角色。
3. 子代理读取 `artstyle.md`、`artrule.md`、`characters/<id>/profile.md` 和本地参考图。
4. 子代理只输出到 `runs/<pet-id>/`，不能直接改 `pets/`、`catalog.json` 或 `角色清单.md`。
5. 主线程统一 QA。
6. QA 通过后，主线程复制最终结果到 `pets/<pet-id>/`。
7. 主线程更新 `catalog.json`、宠物 README 和 `角色清单.md`。
8. 每批结束后，把反复出现的问题写回规则或角色备注。

## QA 标准

基础文件检查：

- `pet.json` 存在且 JSON 可解析。
- `spritesheet.webp` 存在。
- `preview/contact-sheet.png` 存在。
- atlas 尺寸为 `1536 x 1872`。
- atlas 为 `WEBP/RGBA`。
- 背景透明，未使用格全透明。

画面质量检查：

- 没有截图残片、UI 残留、白底、色块边缘或脏背景。
- 角色身份锚点清晰，不能和其他角色混淆。
- 四肢不能太长。
- 身体不能太扁。
- 大头、短手短脚、圆润小体型成立。
- 每个动作状态能看出差异。
- 与已有宠物不应过度相似。

失败后回写：

- 如果四肢太长，在角色备注和下一轮提示中强调“短手短脚”。
- 如果身体太扁，在角色备注和下一轮提示中强调“保留圆润小身体体积”。
- 如果身份不像，在 profile 中补充更明确的身份锚点。
- 如果混入截图背景，丢弃该轮结果，不进入 `pets/`。
- 如果配色丢失，在 profile 中把主色和装饰色提升为必须保留项。

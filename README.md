# Codex Pet Library

一个 Codex 自定义桌宠库，收集角色宠物化的 fan-made 宠物包。每个宠物都按 Codex custom pet 格式提供 `pet.json` 和 `spritesheet.webp`，可以单独安装。

> 非官方 fan-made 项目。本仓库不隶属于、也不代表任何游戏、发行方或权利方。

## Pets

| Pet | Status | Preview | Path |
| --- | --- | --- | --- |
| Susie Paw | Ready | ![Susie Paw](pets/susie-paw/preview/contact-sheet.png) | `pets/susie-paw` |
| W Paw | Ready | ![W Paw](pets/w-paw/preview/contact-sheet.png) | `pets/w-paw` |

## 给 Codex / Agent 的安装版本

把下面整段发给 Codex、Claude Code 或其他 coding agent。将 `<owner>` 替换成仓库所属账号，`<pet-id>` 替换成要安装的宠物目录名，例如 `susie-paw`。

```text
请帮我从当前 Codex 宠物库安装一个自定义桌宠。

仓库：当前 GitHub 仓库 `susie_paw`
宠物 ID：<pet-id>
源文件：
- pets/<pet-id>/pet.json
- pets/<pet-id>/spritesheet.webp
安装目录：${CODEX_HOME:-$HOME/.codex}/pets/<pet-id>

请执行：
1. 创建安装目录。
2. 从当前仓库的 pets/<pet-id>/ 下载 pet.json 和 spritesheet.webp。
3. 不要修改或删除其他已有宠物。
4. 下载后确认这两个文件都存在。
5. 不要在回复里打印 GitHub 用户名。
6. 告诉我安装完成，并提醒我重启 Codex 或重新打开宠物选择面板。

可用命令：

PET_ID="<pet-id>"
PET_HOME="${CODEX_HOME:-$HOME/.codex}/pets/$PET_ID"
REPO_RAW_BASE="https://raw.githubusercontent.com/<owner>/susie_paw/main"
mkdir -p "$PET_HOME"
curl -fL "$REPO_RAW_BASE/pets/$PET_ID/pet.json" -o "$PET_HOME/pet.json"
curl -fL "$REPO_RAW_BASE/pets/$PET_ID/spritesheet.webp" -o "$PET_HOME/spritesheet.webp"
test -f "$PET_HOME/pet.json" && test -f "$PET_HOME/spritesheet.webp"
```

## 手动安装

以 `susie-paw` 为例：

```bash
PET_ID="susie-paw"
PET_HOME="${CODEX_HOME:-$HOME/.codex}/pets/$PET_ID"
REPO_RAW_BASE="https://raw.githubusercontent.com/<owner>/susie_paw/main"
mkdir -p "$PET_HOME"
curl -fL "$REPO_RAW_BASE/pets/$PET_ID/pet.json" -o "$PET_HOME/pet.json"
curl -fL "$REPO_RAW_BASE/pets/$PET_ID/spritesheet.webp" -o "$PET_HOME/spritesheet.webp"
```

然后重启 Codex，或重新打开宠物选择/设置面板。

## Codex Pet 格式

每个宠物目录都保持同样结构：

```text
pets/<pet-id>/
├── README.md
├── pet.json
├── spritesheet.webp
└── preview/
    └── contact-sheet.png
```

`spritesheet.webp` 使用固定 atlas：

| 项目 | 值 |
| --- | --- |
| 尺寸 | `1536 x 1872` |
| 网格 | `8 x 9` |
| 单格 | `192 x 208` |
| 背景 | 透明 |
| 未使用格 | 全透明 |

动画行：

| Row | State | Frames |
| ---: | --- | ---: |
| 0 | `idle` | 6 |
| 1 | `running-right` | 8 |
| 2 | `running-left` | 8 |
| 3 | `waving` | 4 |
| 4 | `jumping` | 5 |
| 5 | `failed` | 8 |
| 6 | `waiting` | 6 |
| 7 | `running` | 6 |
| 8 | `review` | 6 |

## 卸载

```bash
rm -rf "${CODEX_HOME:-$HOME/.codex}/pets/<pet-id>"
```

## 许可和使用

README、脚本和元数据可按 MIT 使用。宠物 spritesheet 与预览图片是 fan-made 图片资产，仅建议用于个人、学习和非商业用途。详见 [FAN_CONTENT_NOTICE.md](FAN_CONTENT_NOTICE.md)。

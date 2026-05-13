# Susie Paw

Susie Paw 是一个粉色电气猫猫风格的 Codex 自定义桌宠。

> 非官方 fan-made 宠物包。该项目不隶属于、也不代表任何游戏、发行方或权利方。

## 预览

![Susie Paw animation contact sheet](preview/contact-sheet.png)

Failed 状态视频预览：[preview/failed.mp4](preview/failed.mp4)

## 安装

把 `<owner>` 替换成仓库所属账号后执行：

```bash
PET_HOME="${CODEX_HOME:-$HOME/.codex}/pets/susie-paw"
REPO_RAW_BASE="https://raw.githubusercontent.com/<owner>/susie_paw/main"
mkdir -p "$PET_HOME"
curl -fL "$REPO_RAW_BASE/pets/susie-paw/pet.json" -o "$PET_HOME/pet.json"
curl -fL "$REPO_RAW_BASE/pets/susie-paw/spritesheet.webp" -o "$PET_HOME/spritesheet.webp"
```

然后重启 Codex，或重新打开宠物选择/设置面板。

## Manifest

```json
{
  "id": "susie-paw",
  "displayName": "Susie Paw",
  "description": "A tiny pink electric cat Codex pet with soft chibi energy.",
  "spritesheetPath": "spritesheet.webp"
}
```

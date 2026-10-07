<!-- markdownlint-disable MD013 -- Font commands, URLs and license tables contain long references. -->

# iTerm2: Hack + Nerd Fonts + Herdr icons

[简体中文](#简体中文)

Use **Hack Herdr Nerd Font** when iTerm2 needs both the Herdr sidebar marks
and the Nerd Font symbols used by Pi or shell prompts. Selecting the
icon-only Herdr Agent Icons Max as the font for _all_ non-ASCII text leaves
those other characters without glyphs.

This optional font does not change plugin behavior or terminal preferences.
`install.sh` does not install or select it automatically.

## Install on macOS

From this repository's root:

```bash
mkdir -p "$HOME/Library/Fonts"
cp assets/fonts/hack-herdr/HackHerdrNerdFont-*.ttf "$HOME/Library/Fonts/"
```

In **iTerm2 Settings → Profiles → Text**, select:

| Setting                                 | Value                                      |
| --------------------------------------- | ------------------------------------------ |
| Font                                    | Hack Herdr Nerd Font                       |
| Style                                   | Regular                                    |
| Size                                    | Keep your existing size; verified at 13 pt |
| Use a different font for non-ASCII text | Off                                        |

Apply this to each profile used for local or SSH sessions. Fonts are rendered
on the Mac: installing a font only on the SSH server does not fix iTerm2.
If a live session retains old settings, update its Text settings or open a new
session; do not stop Herdr or discard running agent panes just to change a font.
To revert, select your previous font. The original fonts are not overwritten.

## Contents and verification

Four TTFs are supplied: Regular, Bold, Italic, and BoldItalic. Each keeps the
corresponding Hack Nerd Font glyphs, widths, and line metrics, and adds:

- 23 Herdr logos at `U+E1A0–U+E1B6`;
- 6 Herdr status symbols at `U+E1C0–U+E1C5`.

The icon outlines are scaled from 1000 to 2048 units/em. Their advance is one
Hack cell, with the deliberate side overhang of the source **Max** face.
The base font already includes Pi's Nerd Font glyphs and `▰/▱` gauges.

The same outlines were visually checked in iTerm2 on macOS: all 29 Herdr
characters, Pi icons, gauges, bold/italic, Chinese, and ASCII rendered. The
`U+2060–U+2062` state-tag prefixes produced no additional question marks.
This is not a claim of rendering verification in other terminals.

## Rebuild

Requirements: Python and `fonttools==4.55.0`. Download and unpack
[Hack.zip from Nerd Fonts v3.4.0](https://github.com/ryanoasis/nerd-fonts/releases/download/v3.4.0/Hack.zip).
Use the directory containing `HackNerdFont-{Regular,Bold,Italic,BoldItalic}.ttf`:

```bash
uv run --no-project --with fonttools==4.55.0 python   scripts/build-hack-herdr-font.py --base-dir /path/to/unpacked/Hack
```

The bundled `assets/fonts/HerdrAgentIconsMax-Regular.ttf` is the icon input.
`--icons` and `--output-dir` can select alternative locations. The script
rejects conflicting character mappings instead of replacing existing glyphs;
it checks that original character mappings, widths, line metrics, and all
icon mappings survive saving. It never downloads inputs or modifies the base
fonts. Rebuild explicitly after updating either source.

## Redistribution

Keep [NOTICE.md](../assets/fonts/hack-herdr/NOTICE.md) and the entire adjacent
`licenses/` directory with the TTFs. This is a locally modified font, not an
official release by Hack, Nerd Fonts, Herdr, or any depicted vendor. The
third-party font and icon licenses remain applicable.

## 简体中文

此字体保留 Hack 的文字、Nerd Font 符号及全部 Herdr 图标，适合同时使用
Herdr、Pi 与带图标 shell 提示符的 iTerm2 用户。

1. 在仓库根目录执行本文的 macOS 安装命令，安装四个 TTF。
2. 打开 **iTerm2 Settings → Profiles → Text**，选择
   **Hack Herdr Nerd Font → Regular**，保留原字号。
3. 关闭 **Use a different font for non-ASCII text**；每个用到的 Profile
   都要设置。不要用只含专用图标的 Herdr Agent Icons Max 接管所有非 ASCII 字符。
4. SSH 场景仍在 Mac 安装字体，无需改服务器。旧会话未更新时修改当前会话的
   Text 设置或新开会话，无需停止 Herdr 或关闭运行中的 agent。

已在 macOS iTerm2 实测 23 个 Logo、6 个状态符号、Pi 图标、进度条、粗体、
斜体及中文。原字体未覆盖，回退时选择之前的字体即可。构建命令见 Rebuild，
分享时必须附带 NOTICE.md 与整个 licenses 目录。

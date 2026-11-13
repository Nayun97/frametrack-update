# 帧轨桌面端 · 界面热更新静态源

本仓库托管「帧轨」Electron 桌面版的界面更新包，通过 GitHub Pages 对外提供下载地址。
桌面端外壳内置的 `HotUpdater`（`hot-update.js`）从本目录读取 `version.json`，比对版本后下载 `frametrack-update.zip`，完成校验、备份、覆盖与失败回滚。

## 目录结构

```
frametrack-update/
├── version.json              # 更新清单：version / package / sha256 / size / notes / updatedAt / files
├── frametrack-update.zip     # 界面包（包内为界面文件，不含 version.json）
└── README.md
```

## 拉取地址（Pages 发布后）

```
https://nayun97.github.io/frametrack-update/
```

桌面端「检查更新」弹窗里把更新源填成上面这个目录地址即可。

## 包内文件

- `视频录音逐字定位.html`（水墨新版）
- `视频录音逐字定位-经典版.html`
- `ink-bg.png` / `ink-video.png`

## 明确不上包的内容

- 课程素材（D 盘 mp4/mp3、截图帧）——留在本机素材库，不进更新包；
- `course_index.js` / `course_index.rel.js` / `fulltext_index.js` / `config.json`——热更新受保护文件，不允许被包覆盖。

## 发布流程

1. 在工程 `frametrack-desktop` 下跑 `python make_update.py --notes "更新说明"`，制包到 `frametrack-desktop/update-source/`；
2. 把 `version.json` 与 `frametrack-update.zip` 复制到本仓库根目录；
3. `git add -A && git commit -m "更新 vX.Y.Z" && git push`；
4. GitHub Pages 从 `main` 分支根目录发布，推送后稍等片刻生效。

## 与移动端热更新的区别

移动端英语听力标记训练用的是账号下另一个仓库 `Nayun97/hot-update`（`manifest.json` + `bundle-*.tar.gz` + minisig 签名），与本桌面端仓库是两套独立体系，清单格式、包格式、校验方式都不要混用。

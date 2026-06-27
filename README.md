# ccb

`ccb` 是「云端 Claude · 本地双手」的命令行入口:在云端沙箱里跑 Claude Code,而它的每一条命令、每一次文件读写都落在**你本地这台机器**上。

> 本仓库**只放编译好的二进制**(各平台 release 产物),源码在私有仓。所以你**无需任何 GitHub 权限**,下载即用,并会自动保持最新。

## 安装

装到 PATH 上的 `~/.local/bin/ccb`(用户可写,自更新免 sudo):

**macOS · Apple Silicon (M 系列)**
```sh
mkdir -p ~/.local/bin && curl -fSL https://github.com/Barrierml/ccb-dist/releases/latest/download/cbridge-darwin-arm64 -o ~/.local/bin/ccb && chmod +x ~/.local/bin/ccb
```

**macOS · Intel**
```sh
mkdir -p ~/.local/bin && curl -fSL https://github.com/Barrierml/ccb-dist/releases/latest/download/cbridge-darwin-amd64 -o ~/.local/bin/ccb && chmod +x ~/.local/bin/ccb
```

**Linux · x86_64**
```sh
mkdir -p ~/.local/bin && curl -fSL https://github.com/Barrierml/ccb-dist/releases/latest/download/cbridge-linux-amd64 -o ~/.local/bin/ccb && chmod +x ~/.local/bin/ccb
```

**Linux · arm64**
```sh
mkdir -p ~/.local/bin && curl -fSL https://github.com/Barrierml/ccb-dist/releases/latest/download/cbridge-linux-arm64 -o ~/.local/bin/ccb && chmod +x ~/.local/bin/ccb
```

确认 `~/.local/bin` 在 `PATH` 上(zsh 为例,bash 改 `~/.bashrc`):
```sh
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc && source ~/.zshrc
```

## 用起来

二进制本身不带任何凭据。要连上云端,你还需要一个**平台接入 key**(向 owner 索取)以及一个账号/沙箱:
```sh
export CBRIDGE_APIKEY=<向 owner 索取>     # 建议也写进 shell rc
```
然后:
```sh
ccb            # 打开面板:看会话、↵ 进会话、n 新建、d 结束
ccb up         # 直接在当前目录拉起 / 续接云端 Claude
ccb status     # 看本机 daemon 状态
ccb kill       # 关掉本机 daemon(切断桥,结束沙箱内会话)
```
进入会话后,关掉终端窗口 = 离开但保活(云端继续,下次回来还在);`/exit` 才结束任务。

## 自动更新

`ccb` 每次启动会检查本仓库最新 release,有更高版本就**走普通 HTTPS 自动下载替换**——不需要 `gh`、不需要登录、不需要本仓库权限。也可手动:
```sh
ccb update          # 立即检查并更新
ccb version         # 看当前版本
```
临时关闭自动更新:`export CBRIDGE_NO_UPDATE=1`。

## 支持平台

`darwin/arm64` · `darwin/amd64` · `linux/amd64` · `linux/arm64`(Windows 暂不支持)。每个 release 附 `SHA256SUMS` 可校验完整性。

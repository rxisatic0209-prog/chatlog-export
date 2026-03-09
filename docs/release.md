# 发布说明

这份文档面向“把程序打包给别人直接用”。

## 发布目标

推荐产物是“压缩包 + 可执行文件 + 说明文档”，而不是只发源码。

对最终用户来说，最省事的方式是：

- 下载压缩包
- 解压
- 直接运行可执行文件

一般不需要用户自己安装 Go。

## 发布内容建议

建议 release 包至少包含：

- 可执行文件
- `README.md`
- `LICENSE`
- `docs/mcp.md`
- `export_json/chatbrowser.html`

## 本地编译

### macOS 当前机器直接编译

```bash
go build -o chatlog_mac .
```

### 测试

```bash
env GOCACHE=/tmp/go-build go test ./...
```

## 使用 GoReleaser

仓库已经带了 `.goreleaser.yaml`。

### 常见流程

1. 打 tag
2. 执行 GoReleaser
3. 生成归档文件
4. 上传到 GitHub Releases

示例：

```bash
git tag 1.2.0
git push personal main --tags
goreleaser release --clean
```

如果只想本地看构建结果：

```bash
goreleaser build --clean
```

## 平台说明

当前配置包含：

- darwin/amd64
- darwin/arm64
- windows/amd64
- windows/arm64

## 建议的发布命名

可以按平台区分：

- `chatlog-export_darwin_arm64.zip`
- `chatlog-export_darwin_amd64.zip`
- `chatlog-export_windows_amd64.zip`

## 给使用者的最小说明

建议在 release 描述里明确写：

1. 这是本地导出工具，不是云服务
2. 默认导出到桌面
3. 群聊导出支持日期筛选
4. 自动获取 key 失败时，可手动设置 key
5. 如需接入 agent，可参考 `docs/mcp.md`


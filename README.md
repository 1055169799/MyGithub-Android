# My Github（Android 客户端）

My Github 是一款 Android 版 GitHub 客户端，基于 GitHub OAuth 实现账号登录，支持仓库与文件管理。

## 功能特性

- GitHub OAuth 授权登录，refresh_token 自动续期，记住登录状态
- 仓库列表查看、新建、重命名、删除
- 文件/文件夹创建、重命名、移动、删除
- 大文件上传（Git Data API blob 接口，突破 Contents API 的 1MB 限制，上限 100MB）
- 重命名/移动大文件复用原 blob sha，不下载不重传内容
- release 签名 APK 安装包

## 下载安装

APK 安装包位于仓库 APK/ 目录，下载后安装（需允许"安装未知来源应用"）。

当前版本：**v1.0.3**（[下载](APK/MyGithub_1.0.3.apk)）

> 升级安装无需卸载：所有版本使用同一签名证书，可直接覆盖安装。

### 权限说明

- 仓库与文件读写需要 `repo` 授权
- 读取账号信息需要 `user` 授权
- **删除仓库需要 `delete_repo` 授权**：从 v1.0.3 起登录时会一并申请。若你在旧版本登录过，
  升级后请先「退出登录」再重新登录并同意授权，否则删除仓库会返回 403
  `Must have admin rights to Repository`。

## 更新日志

### v1.0.3

- 修复：删除仓库提示 `网络请求失败`（HTTP 403）。根因为 OAuth 授权缺少 `delete_repo` scope，
  已补入授权范围；删除失败时改为给出中文指引而非原始 JSON
- 修复：仓库内右上角「新建文件夹」图标、页面返回箭头在深色工具栏上几乎不可见
  （图标填充为纯黑色 #000000，工具栏背景 #0D1117），已统一改为白色

### v1.0.2

- 优化：重命名/移动大文件改为复用原 blob sha（Git Data API），不再下载后重新上传，
  网络开销由「文件体积 × 1.33」降至 10KB 以内，且与文件大小无关

### v1.0.1

- 修复：大文件上传报 `unexpected end of stream`。根因为自定义 RequestBody 的
  `contentLength()` 将 JSON 固定头部多算 1 字节（35 应为 34），服务器按声明长度等待最后
  1 字节直到超时断连
- 修复：上传进度封顶在 84% 的假象，改为真实进度

### v1.0.0

- 首个版本：OAuth 登录、仓库与文件管理

## 技术栈

- Kotlin + View（XML 布局）+ Material Components + RecyclerView
- Retrofit + OkHttp + Gson + Kotlin 协程
- GitHub REST API / OAuth 2.0
- minSdk 21 / targetSdk 36 / compileSdk 36
- v1 + v2 签名

## 已知限制

- 单文件上限 100MB（GitHub Git Data API 限制），超大文件建议使用 Git LFS 或分片方案
- client_secret 打包在客户端内，仅供个人使用；对外分发建议改为后端代理或 PKCE 方案

# My Github（Android 客户端）

My Github 是一款 Android 版 GitHub 客户端，基于 GitHub OAuth 实现账号登录，支持仓库与文件管理。

## 功能特性

- GitHub OAuth 授权登录，refresh_token 自动续期
- 仓库列表查看与新建
- 文件/文件夹创建、重命名、移动、删除
- 大文件分块上传（Git Data API，突破 1MB 限制）
- release 签名 APK 安装包

## 下载安装

APK 安装包位于仓库 APK/ 目录，下载后安装（需允许"安装未知来源应用"）。

当前版本：v1.0.0

## 技术栈

- Kotlin + Jetpack Compose
- GitHub REST API / OAuth 2.0
- v1+v2 签名
---
title: "用rust开发一个短链接Server"
date: 2022-10-01T18:18:39+08:00
draft: true
---

## 基础部分
### 安装Rust
Rust的推荐安装方式是通过shell脚本，下载rustup tool安装。

```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```
### 创建一个新项目
```
cargo new shorty
code shorty

```
介绍一下项目目录

```
.
├── Cargo.lock
├── Cargo.toml
└── src
   └── main.rs
```
### hello world
cargo run/build
target/release/
target/debug/
介绍一下二进制文件，可以直接执行的

cargo check
cargo build
cargo run

### 替换镜像源
字节的
高校的

## 构建一个Web Server

### 安装framework
actix/rocket

Cargo.toml

### hello world in framework


### 安装数据库
disiel/sqlx

### 访问一个数据库查询

### web访问时，访问数据库

## TODO 扩展部分
### 构建跨平台支持
### 以下需要思考是否需要介绍
Docker部署
部署Amazon

## 一个short code项目

### api
1. create code
2. get original url
3. first page


### 完整的源代码


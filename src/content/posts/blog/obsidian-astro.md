---
title: 怎么使用obsidian 来编写 astro 博客
published: 2026-04-18
updated: 2026-04-18
description: 本教程专为「Obsidian 撰写笔记」+「Astro Composer 插件转换笔记为 Astro 博客内容」+「Git 插件同步到 GitHub」的 workflow 设计，全程无需复杂命令行，纯 Obsidian 内操作（少量 GitHub 后台配置），适合新手快速上手，解决“Obsidian 写文→Astro 发布→GitHub 托管”的全流程同步问题。
image: https://tu.682000.xyz/file/blog/wenzhang/1776516130544_image.png
tags:
  - Obsidian
  - astro
category: 分类
draft: false
author: fqzlr
---
Obsidian + Astro Composer + Git 插件 同步 Astro 博客到 GitHub 完整教程

前置前提（必做）：

- 已安装 Obsidian 客户端，且启用「第三方插件」（设置 → 第三方插件 → 关闭“安全模式”）。
    
- 已创建 Astro 博客项目（本地需有 Astro 项目文件夹，可通过 `pnpm create astro@latest` 快速创建，选择 blog 模板即可），并熟悉 Astro 项目的 `src/content` 目录（用于存放博客文章）。
    
- 已注册 GitHub 账号，且创建了用于托管 Astro 博客的仓库（建议仓库名与 Astro 博客项目名一致，若要部署 GitHub Pages，仓库名可设为 `用户名.github.io`）。
    
- 已安装所需插件：Astro Composer（Obsidian 插件）、Git（Obsidian 插件，常用 Obsidian Git 或 Git Vault/Folder Sync，本教程以 Obsidian Git 为例，适配多数用户需求）。
    

## 第一步：安装并配置 Astro Composer 插件（核心：Obsidian 笔记转 Astro 内容）

Astro Composer 是 Obsidian 与 Astro 博客无缝衔接的关键插件，可自动将 Obsidian 笔记转换为 Astro 支持的 Markdown 格式（含自动处理链接、标准化属性、管理草稿等），目前该插件暂未上架 Obsidian 社区插件库，需通过 BRAT 插件安装或手动安装，推荐 BRAT 安装（更便捷，支持自动更新）。

### 1 安装 Astro Composer 插件

（`https://github.com/astro-modular/astro-composer`）

### 2 配置 Astro Composer 插件（关键步骤）

配置核心目的：让插件知道「Obsidian 笔记存放位置」和「Astro 项目的内容目录位置」，实现笔记自动转换后同步到 Astro 项目中。

1. 打开 Obsidian 设置 → 找到「Astro Composer」插件，进入配置页面。
    
2. 核心配置项（必设）：
    
    ![](https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=ZDJjNTQ5OGQ1YWI2ZTUyY2ZmYjMzYjUxM2Y1MGQwNjRfY3QxTTNUU3dHcllCNDhzeHdIZ0pYN3I3Vmwwd3ZYN05fVG9rZW46Q1djaGJvVnNRb3JCNTh4ZWxxR2NMUDVYbkRiXzE3NzY1MTc2MjQ6MTc3NjUyMTIyNF9WNA&add_watermark=true&scene_type=CCM_DOUBAO)
    
    ![](https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=MjFlMGVlY2JlMDNkZjQxOWJjNTMxYzQ0MGVmMjk2OWFfTXZtdDB6VDdHREJyWEQySEhydGlocUNhNHZ3U3ltdUlfVG9rZW46T3E4TmJsR0R4b2E5VWJ4eXdKbGNuZkRBbmljXzE3NzY1MTc2MjQ6MTc3NjUyMTIyNF9WNA&add_watermark=true&scene_type=CCM_DOUBAO)
    
    ![](https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=YTVhMDhjODU5OGRjNTgxNWYzNjk0MWQ4Y2VmNjUyZWJfMnpnaVp5dGtITEpEVUFka1F1VjNLdktGM0t4SExPODNfVG9rZW46VjlEa2JDUmJwb1ROT0t4UGxuZGNTcDZ6bldoXzE3NzY1MTc2MjQ6MTc3NjUyMTIyNF9WNA&add_watermark=true&scene_type=CCM_DOUBAO)
    
    4. Posts Folder：设置 Obsidian 中用于存放博客文章的文件夹（例如 `Blog/Posts`），后续所有要发布的笔记都放在这个文件夹下。
        
    5. Astro Content Path：设置本地 Astro 项目的`src/content` 目录路径（例如 `D:/MyBlog/astro-blog/src/content`），插件会自动将转换后的笔记同步到这个目录。
        
    6. Link Base Path：设置链接基准路径，填写 Astro 博客的文章访问路径（例如 `/blog`），插件会自动将 Obsidian 内部链接（ wikilinks 或 Markdown 内部链接）转换为 Astro 友好的链接格式，避免发布后链接失效。
        
    7. Creation Mode：选择文章存储结构，推荐「Folder-based with index.md」（每个文章对应一个文件夹，内部包含 index.md 文件），适配多数 Astro 博客模板。
        
    8. Draft Management：启用「Underscore Prefix」，插件会为草稿笔记添加下划线前缀（例如 `_my-draft.md`），Astro 会自动隐藏这些草稿，避免误发布。
        
3. 可选配置（优化体验）：
    
    1. Property Standardization：设置笔记属性模板（例如标题、日期、标签等），启用「Standardize Properties」命令，可自动为笔记添加缺失的属性，保持 Astro 文章格式统一。
        
    2. Rename Post Command：启用后，修改笔记的「title」属性，插件会自动将笔记文件名/文件夹名更新为 kebab-case 格式（例如“我的第一篇博客”→「my-first-blog」），适配 Astro 的路由规则。
        
4. 配置完成后，点击「Save Settings」，重启插件（Obsidian 重启或禁用再启用），确保配置生效。
    

### 3 测试 Astro Composer 转换功能

1. 在 Obsidian 的「Posts Folder」（例如 `Blog/Posts`）中新建一篇笔记，输入标题（例如“Obsidian 同步 Astro 博客教程”）。
    
2. 使用插件的「Standardize Properties」命令（Obsidian 命令面板 → 输入该命令），自动添加标题、日期等属性。
    
3. 查看本地 Astro 项目的 `src/content` 目录，会发现自动生成了对应文件夹和 index.md 文件，且 Obsidian 笔记的内容、链接已自动转换为 Astro 支持的格式，说明插件配置成功。
    



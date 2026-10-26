# 我们的小日子

双人小屋：纪念日、故事、相册、心愿、留言、双人问答，以及共同照顾的电子宠物。

[打开 GitHub Pages](https://liu7866.github.io/our-little-days/) · [完整源码](source/) · [部署方式总览](source/deploy/README.md)

## 目录

- 根目录的 `index.html`、`app.js` 等文件：GitHub Pages 前端。
- [`source/`](source/)：完整前后端源码、数据库迁移、测试与构建工具。
- [阿里云 / Linux 部署方法](source/deploy/node/部署说明.md)。
- [Cloudflare 接入和部署限制](source/deploy/cloudflare.md)。
- [本地使用方法](source/本地使用说明.md)与[验证记录](source/deploy/node/验证结果.md)。

## 本次同步的功能

- 首次使用设置两位成员的密码，默认身份为成员一、成员二；管理员可自定义身份名称。
- 相册支持 2,000 张照片，每批最多选择 20 张；始终保留继续添加入口，上传失败可重试。
- 小猫与小兔各有幼年、少年、成年外观，动作随喂食、玩耍、摸摸、睡眠和双人陪伴变化。
- 宠物小屋颜色与六件装饰实时预览，保存后同步。
- 密码可设为 6 至 128 个字符；新个人恢复码 12 位、每 4 位分组，兼容旧的 64 位码。
- 独立 Node.js 后端、SQLite 与照片存储、账号管理、备份恢复，以及阿里云和 Cloudflare 文档。

## 在自己的电脑或服务器运行

需要 Node.js 22.18 或更新版本，以及 pnpm 11.25.0。

```sh
git clone https://github.com/liu7866/our-little-days.git
cd our-little-days/source
pnpm install --frozen-lockfile
pnpm run build:node
pnpm run test:node
pnpm run start:node
```

打开 http://127.0.0.1:3000，首次页面设置自己的两位成员密码。构建生成的 `source/dist-node/` 可以单独部署，不需要安装运行依赖。正式部署前请阅读 HTTPS、持久化目录与备份说明。

## GitHub Pages 与后端

GitHub Pages 只运行静态前端，默认连接原托管站后端，不运行 `source/server/`。**本次公开代码同步不会自动更新原站后端**；密码长度、恢复码和照片容量等服务器规则，需要后端部署相应版本后才会生效。

自行部署时使用独立 Node.js 后端最直接。Cloudflare DNS 代理可以接入该服务器；直接迁入个人 Workers 账号仍需完成文档所列认证适配。

## 数据与验证

仓库不包含真实账号、密码哈希、恢复码、会话、照片、数据库、备份或本机环境变量。测试中的密码、姓名与记录均为虚构夹具。公开副本的 `.openai/hosting.json` 仅保留 `DB`、`BUCKET` 绑定名称，不携带原托管项目标识。

当前功能代码已通过 102 项本地与隔离环境测试。实际服务器、域名和浏览器兼容性仍需按部署环境验收。

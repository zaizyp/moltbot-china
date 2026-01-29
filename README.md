# moltbot-china

中国 IM 平台 Moltbot 扩展插件集合。

⭐ 如果这个项目对你有帮助，请给个Star支持一下~


> 🚧 **即将支持**：直接通过 `npm install @moltbot-china/dingtalk` 安装，无需手动复制文件和修改配置。

## 演示

![钉钉机器人演示](doc/images/dingtalk-demo_2.gif)

## 支持平台

| 平台 | 状态 | 插件 |
|------|:----:|------|
| 钉钉 | ✅ 可用 | `@moltbot-china/dingtalk` |
| 飞书 | 🚧 开发中 |  |
| 企业微信 | 🚧 开发中 |  |
| QQ机器人 | 🚧 开发中 |  |

## 安装

```bash
git clone https://github.com/BytePioneer-AI/moltbot-china.git
cd moltbot-china

npm i -g pnpm
pnpm install
```

## 钉钉插件配置

> 📖 **[钉钉企业注册指南](doc/guides/dingtalk/configuration.md)** — 无需任何材料，最快 5 分钟完成配置


在 Moltbot 配置文件 `/root/.clawdbot/clawdbot.json` 中添加钉钉渠道配置：

```json
{
  "session": {
    "dmScope": "per-peer"
  },
  "plugins": {
    "load": {
      "paths": ["/path/to/moltbot-china/extensions/dingtalk"]
    },
    "entries": {
      "dingtalk": { "enabled": true }
    }
  },
  "channels": {
    "dingtalk": {
      "enabled": true,
      "clientId": "YOUR_APP_KEY",
      "clientSecret": "YOUR_APP_SECRET",
      "dmPolicy": "pairing",
      "groupPolicy": "allowlist",
      "requireMention": true,
      "allowFrom": [],
      "groupAllowFrom": []
    }
  }
}
```

### 钉钉渠道配置

| 配置项 | 必填 | 默认值 | 说明 |
|--------|:----:|--------|------|
| `clientId` | ✅ | - | 钉钉开放平台应用 AppKey |
| `clientSecret` | ✅ | - | 钉钉开放平台应用 AppSecret |
| `dmPolicy` | | `pairing` | 私聊策略：`open`（任何人）/ `pairing`（需配对）/ `allowlist`（白名单） |
| `groupPolicy` | | `allowlist` | 群聊策略：`open`（任何群）/ `allowlist`（白名单群）/ `disabled`（禁用） |
| `requireMention` | | `true` | 群聊中是否需要 @机器人 才响应 |
| `allowFrom` | | `[]` | 私聊白名单用户 ID 列表 |
| `groupAllowFrom` | | `[]` | 群聊白名单群 ID 列表 |

### 会话配置（重要）

`session.dmScope` 控制不同用户的会话隔离方式：

| 值 | 说明 |
|----|------|
| `main` | 默认值，所有用户共享同一会话（不推荐多用户场景） |
| `per-peer` | **推荐**，按用户 ID 隔离，每个用户独立会话 |
| `per-channel-peer` | 按渠道+用户隔离，适合多渠道多用户场景 |
| `per-account-channel-peer` | 最细粒度，按账户+渠道+用户隔离 |


### 跨渠道身份关联（可选）

如果同一用户在多个渠道使用，可以通过 `session.identityLinks` 关联身份，共享会话历史：

```json
{
  "session": {
    "dmScope": "per-peer",
    "identityLinks": {
      "alice": ["dingtalk:035004583157903146", "telegram:123456789"]
    }
  }
}
```

## License

MIT

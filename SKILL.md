---
name: douyin-hot-topic-maker-free
description: Use an authorized Easy WebBridge browser to turn one Douyin account's currently visible hot-page and optional keyword-search signals into exactly five practical topic ideas, each with a title, 3-second hook, angle, three-part outline, and source citation. Use for 免费抖音热点选题、今天抖音发什么、抖音热点选题助手、抖音三秒钩子、抖音关键词选题、按账号定位追热点、EasyBR 多账号选题、免第三方内容 API Key 的抖音热点研究, Douyin hot topic ideas, or Douyin content planning. Reuses the user's browser login, auto-selects only when one browser is online, and requires explicit selection when several are online.
---

# 免费抖音热点选题助手

免费使用，免第三方内容 API Key，复用用户已有浏览器登录状态。一次只操作一个 EasyBR 浏览器环境，账号与输出互不混用。

## 输入

- 账号定位：`niche`、`audience`、至少一个 `contentPillars`。
- 可选关键词：0-5 个。
- 浏览器环境：一个在线浏览器时可省略 `browserId`；多个在线浏览器时必须明确选择。
- 非敏感账号别名 `accountAlias`，仅用于区分本次输出。

## 执行

1. 确认已安装并启动 Easy WebBridge：[GitHub](https://github.com/xxjrq/easy-webbridge)，[Gitee 备用](https://gitee.com/xxjrq/easy-webbridge)。
2. 读取 [数据契约](references/data-schema.md) 和 [浏览器方法](references/browser-method.md)。不要启动另一套临时浏览器。
3. 运行 `list` 查看在线浏览器。只有一个在线环境时直接采集；多个时先让用户明确选择，再把完整 `browserId` 写进请求。
4. 运行 `collect`，在同一任务标签组依次采集抖音热点页和可选关键词搜索页。只使用页面当前可见内容。
5. 根据快照和 [编辑规则](references/editorial-rules.md) 写 `plan-draft.json`，固定生成 5 条。每条必须有标题、3 秒钩子、切入角度、账号适配、开场/核心展开/结尾行动三段提纲和本次快照的来源 ID。
6. 运行 `validate-plan`，生成 `publishable-plan.json` 和 `publishable-plan.md`。交给用户审核，不执行发布。

```bash
node scripts/douyin-hot-topic-maker-free.mjs list
node scripts/douyin-hot-topic-maker-free.mjs collect --request ./request.json --output ./output/account
node scripts/douyin-hot-topic-maker-free.mjs validate-plan --snapshot ./output/account/research-snapshot.json --draft ./plan-draft.json --output ./output/account
```

最小请求见 `fixtures/request-valid.json`，草稿结构见 `fixtures/plan-draft-valid.json`。

## 输出

- `research-snapshot.json`：本次可见热点与搜索来源。
- `publishable-plan.json`：结构化的 5 条选题。
- `publishable-plan.md`：人能直接审核的选题单。
- `run-diagnostic.json`：需要登录、验证码处理、明确浏览器或修正输入时的诊断。

## 边界

只描述“指定浏览器在采集时刻可见的页面信号”。不声称是全网热榜，不保证爆款，不自动发布，不互动，不绕过验证码，不保存 Cookie、Token 或登录身份。人物、政策、医疗、金融、灾害、伤亡、引语、诉讼及快速变化数字在发布前进行事实复核。

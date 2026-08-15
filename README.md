# 价差监控汇总 · 提醒面板

从 workbuddy（agentos）预览站移植到 GitHub Pages 的静态版本。

- 在线地址：https://surfacebuaa-maker.github.io/spread-monitor-summary/
- 部署方式：GitHub Pages（静态托管，无后端）

## 监控内容

- **GIGADEV 基差**：Hyperliquid（xyz:GIGADEV）买一 vs 兆易创新（603986.SH）A股卖一，USD/CNY 换算
- **KSTR × 科创50**：Binance KSTRUSDT 买一 vs 588000 ETF 卖一，按 20 日滚动中位数基线归一化
- **CXMT 跨市场**：Hyperliquid / Gate / Aster 三平台买一 vs 长鑫科技（688825.SH）A股卖一
- **UNITREE 跨平台**：Bybit / Gate / Aster / Hyperliquid 四平台实时价差；上市前以跨平台中位价为参考，上市后配置 A 股代码即可切换为股票公允价口径

## 工作原理

纯浏览器直连公开接口（与原预览站一致，无后端）：

- Hyperliquid：`https://api.hyperliquid.xyz/info`（POST l2Book）
- Binance：`https://fapi.binance.com/fapi/v1/...`（bookTicker / 日线）
- Bybit：`https://api.bybit.com/v5/market/tickers`（UNITREEUSDT ticker）
- Gate：`wss://fx-ws.gateio.ws/v4/ws/usdt`（CXMT_USDT / UNITREE_USDT bookTicker）
- Aster：CXMT 使用 `wss://fstream.asterdex.com/ws/cxmtusdt@bookTicker` / `@markPrice`；UNITREE 使用 `https://fapi.asterdex.com/fapi/v3/ticker/bookTicker`
- 腾讯行情：`qt.gtimg.cn`（实时盘口）与 `web.ifzq.gtimg.cn`（K线）

## 本地编辑与预览

整个站点就是一个 `index.html`（样式和脚本全部内联）。直接编辑后推送 main 即可自动部署。

## 部署

```bash
git add . && git commit -m "update"
git push origin main
```

GitHub Pages 已配置为从 main 分支根目录发布，推送后约 1-2 分钟生效。

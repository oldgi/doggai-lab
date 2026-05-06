---
date: 2026-04-23
tags: [doggai-lab, mcp, claude-desktop, aj53]
status: draft
---

![doggAI Lab](../assets/images/doggiAItitle.png)

# 讓 AI 看進我的筆記本：MCP 設定踩坑全紀錄

*doggAI AI Lab-01 | 2026-04-23*

---

> 網路上的教學說要改 JSON。我改了半天，什麼都沒發生。

---

## 任務目標很簡單

Day 2 只想做一件事：讓 Claude 能讀我的 Obsidian vault。

這個功能叫 MCP（Model Context Protocol）——讓 AI 工具能存取你電腦上的檔案、資料庫、或其他服務。設定好之後，Claude 就能直接讀寫你的筆記，不需要你每次複製貼上。

聽起來很直觀。實際上踩了三個坑。

---

## 坑一：Store 版不走 JSON

網路上 99% 的 MCP 教學都說：去找 `claude_desktop_config.json`，加上這段設定…… (所以我的 Claude夥伴，也是吃了網路上的。。。這麼教我。。。。)

我找了很久，找不到這個檔案。

後來才發現——**Microsoft Store 版的 Claude Desktop，根本沒有 JSON 設定檔**。它走的是 `Settings → Connectors` 的 UI 介面，完全不同的路徑。

這個差異沒有任何文件明確說明，只能靠撞牆才學會。

---

## 坑二：三個 Claude，只有一個有 MCP

設定完之後，我在原本的對話視窗試了半天，Claude 還是說它沒有 Filesystem 工具。

花了一段時間才搞清楚：**Claude 有三個完全不同的環境**，MCP 只在其中一個生效：

| 環境 | MCP 生效？ |
|---|---|
| Claude Desktop App 原生對話 | ✅ 有效 |
| Claude.ai 網頁版 | ❌ 無效 |
| Claude in Chrome 擴充功能 | ❌ 無效 |

我當時用的那個視窗，剛好是 Chrome 擴充功能版。設定完全正確，但環境選錯，所以一直沒反應。還有一個重點是，直接告訴對話的 Claude 現在的對話環境是使用 Claude desktop (後來我每天回來報到都會說今天幾月幾號，我是用 Claude desktop )  #雖然土但是有效

解法：**開一個全新的 Claude Desktop 原生對話視窗**，MCP 就生效了。

---

## 坑三：權限要分開管理

Filesystem MCP 的工具分兩類：

- **Read-only 工具（9 個）**：列目錄、讀檔案——設成自動允許
- **Write/Delete 工具（4 個）**：寫入、刪除——保持手動確認

任何系統，開放存取之前都要先想清楚邊界在哪。AI 能讀，但不能亂動——這條線要從一開始就劃好，不是等出了事再來收拾。

正好最近才發生了 https://www.ithome.com.tw/news/175391 不可不慎不可不慎。
#方便會上癮  #有效的謹慎無價

---

## 成功的那一刻

設定完成後，我在新視窗請 Claude 列出 `ai-journey` 資料夾的內容。

它真的用了 Filesystem 工具，把 7 個資料夾全部列出來了。

> AI 第一次「看進」我的筆記本了。

這件事說起來平淡，但那一刻確實有點感動。不是因為技術多難，而是因為這代表一個工作流真的接起來了——從這一刻開始，做為一個麻瓜真正有一個實在的夥伴和我一起共筆了。

---

## 給想做一樣事的人

如果你用的是 Microsoft Store 版 Claude Desktop，記住：

1. 不要找 JSON 設定檔，它不存在
2. 去 `Settings → Connectors → Filesystem`，在 UI 介面加路徑
3. 設定完要**開新對話**才會生效，舊視窗不會自動更新
4. Read-only 和 Write 權限分開設，別全開

踩過的坑，留在這裡。

---

*工具：Claude Desktop（Microsoft Store 版）| MCP Filesystem | Obsidian*

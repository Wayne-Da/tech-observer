---
title: "Cursor 年營收 $2B，但 AI 真的懂你的 Code 嗎？"
description: "AI coding 工具的市場驗證和技術現實之間，存在一道有趣的裂縫。"
publishDate: 2026-03-04
tags: ["AI", "Developer Tools", "Coding Agent", "Software Architecture"]
sources:
  - title: "AI Coding Startup Cursor Hits $2B Annual Sales Rate"
    url: "https://www.bloomberg.com/news/articles/2026-03-02/cursor-recurring-revenue-doubles-in-three-months-to-2-billion"
  - title: "The Dangerous Illusion of AI Coding? – Jeremy Howard"
    url: "https://www.youtube.com/watch?v=dHBEQ-Ryo24"
  - title: "Theory of Code Space: Do Code Agents Understand Software Architecture?"
    url: "https://arxiv.org/abs/2603.00601"
  - title: "AgentGate – Bonded Execution Engine for AI Agents"
    url: "https://github.com/selfradiance/agentgate/blob/main/docs/manifesto.md"
draft: false
---

Cursor 三個月內 ARR 翻倍到 $2B，這個數字沒有任何 hype 的成分——是真金白銀、每月續訂的錢。但同一天，Jeremy Howard 在 YouTube 上丟出一部叫《The Dangerous Illusion of AI Coding》的影片，一篇 arXiv 論文用實驗數據告訴你 AI code agent 在多檔案架構理解上的 F1 只有 0.129 到 0.646。所以到底是怎樣？AI coding 是新時代的 IDE，還是我們集體在用一個很會裝的自動補全？

## $2B 的市場不會說謊

先承認一個事實：Cursor 的數字是 AI 應用領域少數不需要辯解的成績單。不是 DAU、不是下載量、不是那種「我們有一百萬用戶（其中九十九萬用了一次就刪了）」的虛榮指標。ARR $2B 代表有大量開發者每個月真的在付錢，而且三個月前付錢的人還在付。

這說明了什麼？說明 AI coding 工具解決了一個真實的痛點——不是寫不出 code，而是寫 code 的過程太慢、太煩、太多重複勞動。當一個工具能幫你省下每天 30 分鐘的 boilerplate 時間，$20/月 的訂閱費根本不需要思考。

但老實說，$2B 只能證明需求存在，不能證明工具真的做到了它暗示的事。

## Jeremy Howard 的那把冷水

Jeremy Howard 不是那種隨便喊「AI 要完蛋了」的人。他是 fast.ai 的創辦人，自己寫 code、自己訓模型、自己教書。當他說 AI coding 有「dangerous illusion」的時候，值得停下來聽一下。

他的核心論點不是說 AI coding 沒用——而是說它有用的方式會讓人產生錯覺。你看著 AI 刷刷刷生出一整個 function，覺得「它懂了」，但它只是在做 pattern matching。它不知道這個 function 為什麼要這樣寫，不知道它跟隔壁那個 module 的隱含契約是什麼，不知道你三個月前決定不用 ORM 的那個技術決策。

說白了：**AI 很會寫句子，但不會讀文章。**

## 論文實錘：F1 最高 0.646

如果你覺得 Jeremy Howard 只是在發表意見，這篇 arXiv 論文（Theory of Code Space）給了你硬數據。研究團隊做了一件很聰明的事：他們不測 AI 能不能寫 code，他們測 AI 能不能**理解一個 codebase 的架構**。

做法是生成一堆中等複雜度的 Python 專案，每個都有明確的模組依賴、跨模組約束和設計意圖。然後讓 AI agent 在有限的「觀測預算」下探索這些 codebase，定期回報它對架構的理解。

結果？五個前沿 LLM agent 的 F1 分數範圍是 0.129 到 0.646。最好的也只有六成多，最差的比 rule-based baseline 還爛。更有趣的是，LLM 確實能發現一些 rule-based 方法看不到的語義關係——比如透過 config 檔的動態 wiring——但它們沒辦法把這些理解**穩定地外化**成結構化的描述。

講難聽一點：AI 可能真的「有點懂」，但它沒辦法可靠地告訴你它懂了什麼。這在寫一個獨立的 utility function 時不是問題，但當你讓它重構一個有 30 個 module 的系統時，就是一顆定時炸彈。

## 不會寫 Code 的人做出了什麼

在這些學術辯論的另一端，有個叫 James Toole 的 60 歲投資人在 Hacker News 上發了一個帖子：「I can't code — I built a bonded execution engine for AI agents anyway.」

他做的東西叫 **AgentGate**，是一個讓 AI agent 在執行高風險操作前必須先「繳保證金」的系統。概念很直覺：agent 要做事就先抵押 collateral，做對了退還，做錯了沒收。Ed25519 簽章、SSRF 防護、56 個 passing test、還在紅隊測試中真的發現了一個 vulnerability。

這個案例有趣的地方不在於他做得多好，而在於他能做出來這件事本身。一個完全不會寫 code 的人，用 AI 工具組裝出了一個有 crypto signing、有 adversarial testing 的系統。這不是 demo，是有 test coverage 的 shipped code。

但這也恰好印證了前面的論點——他能做出這些「零件」，是因為每個零件本身就是一個相對獨立的 pattern。真正的問題是：當這個系統長大到需要 30 個 module 互相協作的時候，AI 還能幫他嗎？

## 所以，AI Coding 到底行不行？

答案是一個讓人不太舒服的「看情況」。

AI coding 工具在「寫零件」這個層級已經非常強了，強到值 $2B。寫一個 function、生成一段 boilerplate、做一個 CRUD endpoint——這些事情 AI 做得又快又好，而且會越來越好。

但在「理解整台機器」這個層級，它還差得遠。一個 F1 只有 0.646 的架構理解能力，意味著它每看三個模組關係就會搞錯一個。在小專案裡你不會注意到，在大專案裡它會慢慢把你的 codebase 變成一座看起來能跑但沒人敢動的紙牌屋。

如果你現在在用 Cursor 或類似的工具，繼續用，它確實能讓你更快。但請記住一件事：**你才是那個懂架構的人，不是它。** 每次 AI 幫你生了一段 code，花 30 秒想一下它跟系統其他部分的關係。這 30 秒是你作為工程師最有價值的 30 秒。

那些讓 AI 寫完整個 feature branch 然後直接 merge 的人，遲早會學到這個教訓。只是那時候的學費會比現在貴很多。

# guided-code-learning

[中文](#中文) | [English](#english)

---

## 中文

一個給 **Claude 專案（claude.ai Projects）** 用的 skill：讓 Claude 當老師與 code reviewer，帶你**親手**寫完一個真實的程式專案。

### 為什麼做這個

用 AI 寫程式很快，但很容易變成 vibe coder：程式能跑，卻說不出它為什麼能跑；壞了只能再丟給 AI，改到哪裡也不知道。

這個 skill 反過來用 AI：

- **程式由你自己打、自己 commit**，Claude 不代寫、不替你 push
- 每一段程式都附上「為什麼這樣寫」「和其他寫法比起來差在哪」「什麼時候不能這樣用」
- 每完成一步，Claude 去讀你的 repo、指出問題，確認沒問題才給下一步

目標是做完專案時，你看得懂自己寫的每一行，下一個專案能自己開始。

### 適合的情境

- 有一個想做的真實專案（網站、工具、小系統），想邊做邊學
- 會一點點程式或完全新手，願意自己動手打程式碼
- 有 GitHub repo，並能讓 Claude 讀取
- 希望整個學習過程留下紀錄，之後能回頭查

不適合：只想要盡快拿到能用的程式。那種情況直接請 Claude 寫會比較快。

### 運作方式

學習分成兩種討論串：

| 討論串 | Claude 的角色 | 內容 |
| --- | --- | --- |
| 主討論串 | 協調者 | 整體進度、規格決策、檢查 repo、給下一步、跨步驟問題 |
| 分支討論串 | 教學者 | 單一部分的教學文件與提問 |

專案切成多個「部分」（一個主題，例如「首頁」「資料同步」），每個部分再切成可以一次完成、一次測試的「步驟」。

```
主討論串：「開一個討論串：第三部分」
   │
   ▼
分支討論串：Claude 寫好第三部分的教學文件
   │  你照著做、在文件裡留言提問
   │  你 commit 並 push
   ▼
主討論串：「第三部分完成了，下一步？」
   │  Claude 檢查 repo → 有問題先修 → 沒問題給下一部分
   ▼
（重複）
```

每份教學文件包含：

1. 這部分要完成什麼
2. 新增或修改的檔案（樹狀圖）
3. 上一部分的檢查結果
4. 這部分會學到的新觀念
5. 逐步的程式碼與觀念說明
6. 測試清單
7. commit 指令
8. 常見問題

### 使用方式

1. 把 `guided-code-learning/SKILL.md` 加進你的 Claude skill。
2. 在 Claude 建立一個專案，把你的 repo 和規格文件（例如 `CLAUDE.md`）提供給它。
3. 在專案的主討論串說你想做什麼，請 Claude 列出全部部分的清單。
4. 之後用兩句話推進：
   - 「開一個討論串：<主題>」
   - 「<主題> 完成了，下一步？」

如果 Claude 無法直接幫你開新討論串，它會產生一段「開場訊息」，你在專案裡新開一個對話貼上即可。

### 檔案

```
guided-code-learning/
└── SKILL.md    skill 本體：課程結構、觸發方式、文件格式、檢查流程、協作原則
README.md       本說明
```

### 來源

這套方法整理自一個實際的學習過程：用 Vue 3 從零做出研究室官網，從專案骨架、路由、多語系、首頁、內頁一路到 GitHub Pages 部署。skill 裡的協作原則，大多是過程中實際遇到的狀況。

---

## English

A skill for **Claude Projects (claude.ai)** that turns Claude into a teacher and code reviewer, guiding you to build a real software project **with your own hands**.

### Why

Coding with AI is fast, but it easily turns you into a vibe coder: the code runs, but you can't explain why. When it breaks, all you can do is hand it back to the AI, without knowing what changed.

This skill uses AI the other way around:

- **You type the code and make the commits yourself.** Claude does not write it for you or push to your repo.
- Every piece of code comes with *why it is written this way*, *how it compares to other approaches*, and *when not to use it*.
- After each step, Claude reads your repo and points out problems. You get the next step only after the current one is right.

The goal: by the end of the project, you understand every line you wrote and can start the next project on your own.

### When to use it

- You have a real project in mind (a website, a tool, a small system) and want to learn while building it
- You are a beginner or know a little programming, and you are willing to type the code yourself
- You have a GitHub repo that Claude can read
- You want a record of the whole learning process to look back on

Not a good fit if you just want working code as fast as possible. In that case, asking Claude to write it directly is quicker.

### How it works

Learning happens in two kinds of threads:

| Thread | Claude's role | Contents |
| --- | --- | --- |
| Main thread | Coordinator | Overall progress, spec decisions, repo reviews, next steps, cross-step questions |
| Branch thread | Teacher | The teaching doc for one part, and your questions about it |

The project is split into **parts** (one topic each, e.g. "home page", "data sync"). Each part is split into **steps** small enough to finish and test in one go.

```
Main thread: "Open a thread: Part 3"
   │
   ▼
Branch thread: Claude writes the teaching doc for Part 3
   │  You follow it and ask questions as comments in the doc
   │  You commit and push
   ▼
Main thread: "Part 3 is done. What's next?"
   │  Claude reviews the repo → fix issues first → otherwise, the next part
   ▼
(repeat)
```

Each teaching doc includes:

1. What this part builds
2. Files added or changed (as a tree)
3. Review results from the previous part
4. New concepts covered in this part
5. Step-by-step code with explanations
6. A test checklist
7. Commit commands
8. Common problems

### Usage

1. Add `guided-code-learning/SKILL.md` to your Claude skills.
2. Create a Claude project and give it your repo and spec document (e.g. `CLAUDE.md`).
3. In the project's main thread, describe what you want to build and ask Claude to list all the parts.
4. Then move forward with two phrases (the skill's triggers are written in Chinese; English phrasing with the same meaning works too):
   - 「開一個討論串：<topic>」 / "Open a thread: <topic>"
   - 「<topic> 完成了，下一步？」 / "<topic> is done. What's next?"

If Claude cannot open a new thread directly, it gives you an opening message to paste into a new conversation in the project.

### Files

```
guided-code-learning/
└── SKILL.md    The skill: course structure, triggers, doc format, review process, collaboration rules
README.md       This file
```

### Origin

This method comes from a real learning process: building a research lab website from scratch with Vue 3, covering project setup, routing, i18n, the home page, inner pages, and deployment to GitHub Pages. Most of the collaboration rules in the skill come from situations that actually came up along the way.

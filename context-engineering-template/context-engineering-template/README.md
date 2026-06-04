# Context Engineering Template

這是一套給 AI 輔助開發專案使用的 context engineering 模板。它的目標不是把所有文件一次塞進 prompt，而是建立一個可檢索、可維護、可審核的專案記憶系統。

現在這份模板已經足夠作為新專案基底使用。它包含 AI 啟動路由、工程原則、解耦架構規則、ADR 流程、文件 guard scripts、secret scan、測試、CI drift check，以及專案化完成後使用的嚴格驗收指令。

## 核心概念

1. `CLAUDE.md` 是 AI session 的最小啟動入口。
2. `docs/index.md` 是文件路由表，AI 先讀它，再依照任務讀必要文件。
3. `docs/engineering-principles.md` 定義 Google-style coding、資安優先、記憶體與 CPU 優化、解耦架構原則。
4. `docs/memory/current.md` 只放目前策略、約束和下一步，不放流水帳。
5. `docs/tasks/active.md` 只放目前任務佇列，不放詳細執行紀錄。
6. `docs/memory/sessions/YYYY-MM-DD.md` 放歷史過程、debug narrative、命令輸出和完成紀錄。
7. `docs/adr/*` 放會影響架構、資料契約、安全邊界、核心依賴的決策。
8. `scripts/*` 用來檢查文件 schema、大小、連結、secret、ADR、任務狀態和索引一致性。

## 快速開始

```bash
npm install
npm run lint
npm run security:scan
npm test
npm run docs:refresh
```

如果這份模板已經被複製到真實專案，並且所有 `<PLACEHOLDER>` 都已替換完成，執行嚴格驗收：

```bash
npm run docs:ready
```

`docs:ready` 會跑 lint、security scan、tests、docs refresh，最後用 strict placeholder check 確認這份模板已完成專案化。模板本身保留 placeholder 時，`docs:ready` 失敗是正常的。

## 人類初始化流程

照這個順序把模板導入真實專案：

1. 複製整個模板到新專案根目錄。
2. 確認 `.idea/`、`*.iml`、`node_modules/`、`.env*` 不會進入版本控制。
3. 執行 `npm install`。
4. 更新 `CLAUDE.md` 的 project overview 和 build / test commands。
5. 更新 `docs/project.md`，填入產品目標、非目標、技術棧、平台和工程優先級。
6. 更新 `docs/memory/current.md`，只放目前策略、主要限制和下一步。
7. 更新 `docs/tasks/active.md`，只放當前 active queue。
8. 更新 `docs/testing.md`，填入此專案真正會跑的 lint、test、build、security commands。
9. 更新 `docs/conventions.md` 和 `docs/engineering-principles.md`，確認 coding style、資安優先順序、資源效率和解耦架構規則符合專案。
10. 視需要更新 `docs/security.md`、`docs/dependencies.md`、`docs/data.md`、`docs/ui.md`、`docs/release.md`。
11. 如果已有重大架構方向，使用 `npm run docs:new-adr -- "Initial architecture"` 建立第一份 proposed ADR。
12. 執行 `npm run docs:refresh`。
13. 替換完所有 `<PLACEHOLDER>` 後，執行 `npm run docs:ready`。

## AI 初始化流程

AI agent 接手這份專案時，請照這個順序開始：

1. 讀 `CLAUDE.md`。
2. 讀 `docs/index.md`。
3. 讀 `docs/memory/current.md`。
4. 讀 `docs/tasks/active.md`。
5. 如果任務涉及規劃、實作、重構、架構、安全或效能，讀 `docs/engineering-principles.md`。
6. 依照 `docs/index.md` 的 intent routing 讀最小必要文件，例如 `docs/architecture.md`、`docs/security.md`、`docs/testing.md`、`docs/data.md`、`docs/dependencies.md`、ADR 或特定 task 文件。
7. 不要遞迴讀完整個 `docs/`。
8. 不要把 session log 或 archive 當成目前指令來源。

AI 規劃時必須使用這個優先順序：

1. 先降低資安風險。
2. 再改善記憶體與 CPU 成本。
3. 再維持解耦和可替換邊界。
4. 最後才比較交付速度和實作便利性。

AI 完成工作前，至少要做：

1. 更新最小必要文件。
2. 把詳細執行過程放進 `docs/memory/sessions/YYYY-MM-DD.md`。
3. 用 `## COMPLETED: TASK_ID - summary` 標記完成事項。
4. 如果改到安全邊界、workflow、shell execution、secret handling 或檔案寫入刪除流程，執行 `npm run security:scan`。
5. 執行 `npm run docs:refresh`。
6. 回報修改檔案、驗證結果、剩餘風險。

## 常用指令

| Command | Purpose |
|---|---|
| `npm run lint` | 檢查 scripts 和 tests 的 JavaScript 語法 |
| `npm run security:scan` | 掃描 docs、workflow、bootstrap 文件中的高信心 secret pattern |
| `npm test` | 執行 Node 內建測試 |
| `npm run docs:refresh` | 重建文件索引並執行一般 guard checks |
| `npm run docs:ready` | 真實專案導入完成後的嚴格驗收 |
| `npm run docs:new-session` | 產生今天的 session log |
| `npm run docs:new-adr -- "Decision title"` | 產生下一個 proposed ADR |

## ADR 工作流

當變更會影響架構、安全邊界、資料契約、核心依賴、不可逆行為或權限模型時，先建立 proposed ADR：

```bash
npm run docs:new-adr -- "Decision title"
```

AI 可以建立 `proposed` ADR，但不能自行標記為 `accepted`。只有人類明確確認後，ADR 才能改為 accepted，並且 implementation 才應該依照該決策擴大。

## 目錄結構

```text
.
├── CLAUDE.md
├── docs/
│   ├── CLAUDE.md
│   ├── index.md
│   ├── project.md
│   ├── engineering-principles.md
│   ├── architecture.md
│   ├── security.md
│   ├── testing.md
│   ├── decisions.md
│   ├── adr/
│   │   └── 0000-template.md
│   ├── memory/
│   │   ├── current.md
│   │   ├── sessions/
│   │   │   └── YYYY-MM-DD.md
│   │   └── archive/
│   ├── tasks/
│   │   ├── active.md
│   │   ├── backlog.md
│   │   ├── blocked.md
│   │   └── completed.md
│   └── state/
│       ├── tasks-summary.json
│       └── decision-summary.json
├── scripts/
│   ├── docs-new-adr.mjs
│   ├── docs-new-session.mjs
│   ├── docs-ready.mjs
│   ├── docs-refresh.mjs
│   ├── docs-sync.mjs
│   └── docs-guard-*.mjs
├── test/
└── package.json
```

## 專案化完成標準

一個真實專案使用這份模板時，至少要達成：

- `CLAUDE.md` 已改成真實專案描述。
- `docs/project.md` 已填入產品、目標、非目標、stack 和平台。
- `docs/memory/current.md` 已填入目前策略和下一步。
- `docs/tasks/active.md` 已填入真實 active queue。
- `docs/testing.md` 已填入真實驗證命令。
- 需要 UI、資料、依賴或 release 規則時，相關 docs 已填好。
- 重大架構方向已有 proposed 或 accepted ADR。
- `npm run docs:refresh` 通過。
- `npm run docs:ready` 通過。

## Placeholder 規則

模板故意保留 `<PLACEHOLDER>`，方便複製到真實專案後逐項填寫。一般維護模板時使用：

```bash
npm run docs:refresh
```

真實專案完成初始化後使用：

```bash
npm run docs:ready
```

如果 `docs:ready` 因 placeholder 失敗，代表仍有文件需要專案化，不代表模板壞掉。

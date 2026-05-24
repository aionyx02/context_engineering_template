# Context Engineering Template

這是一套從參考專案抽出的通用 context engineering 模板。目標不是把所有文件塞進 AI prompt，而是建立一個可檢索、可維護、可審核的專案記憶系統。

## 核心思想

1. `CLAUDE.md` 是啟動入口，只放最小規則與讀取順序。
2. `docs/index.md` 是路由表，AI 先讀它，再按任務讀必要文件。
3. `docs/memory/current.md` 只放目前策略、約束、下一步，不放流水帳。
4. `docs/tasks/active.md` 只放目前任務佇列，不放詳細執行紀錄。
5. `docs/memory/sessions/YYYY-MM-DD.md` 放歷史過程、debug narrative、命令輸出與完成紀錄。
6. `docs/adr/*` 放會影響架構、資料契約、安全邊界、核心依賴的決策。
7. `scripts/*` 用來檢查文件前置資料、大小、敘事污染與索引一致性。

## 快速開始

```bash
npm install
npm run docs:new-session
npm run docs:refresh
```

若你的專案不是 Node.js，也可以只保留 `CLAUDE.md` 與 `docs/`；`scripts/` 是輔助檢查，不是架構必需品。

## 建議工作流

### 每次 AI session 開始

1. 讀 `CLAUDE.md`
2. 讀 `docs/index.md`
3. 讀 `docs/memory/current.md`
4. 讀 `docs/tasks/active.md`
5. 根據任務意圖讀 `architecture.md`、`security.md`、`testing.md`、ADR 或特定任務文件

### 實作前

- 判斷是否需要 ADR。
- 確認有沒有 blocked 或 approval-gated 項目。
- 只讀最小相關上下文。

### 實作後

- 目前狀態更新到 `docs/memory/current.md`。
- 任務狀態更新到 `docs/tasks/active.md`。
- 詳細過程寫到 `docs/memory/sessions/YYYY-MM-DD.md`。
- 完成事項用 `## COMPLETED: TASK_ID - summary` 標記。
- 執行 `npm run docs:refresh`。

## 目錄結構

```text
.
├── CLAUDE.md
├── docs/
│   ├── CLAUDE.md
│   ├── index.md
│   ├── project.md
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
│   ├── docs-new-session.mjs
│   ├── docs-sync.mjs
│   ├── docs-guard-size.mjs
│   ├── docs-guard-schema.mjs
│   ├── docs-audit-frontmatter.mjs
│   ├── docs-narrative-check.mjs
│   ├── docs-completed-regen.mjs
│   └── docs-refresh.mjs
└── package.json
```

## 導入方式

1. 複製整個模板到專案根目錄。
2. 修改 `docs/project.md` 的產品、目標、技術棧。
3. 修改 `docs/memory/current.md` 的目前策略與下一步。
4. 修改 `docs/tasks/active.md` 的 active queue。
5. 把重大架構決策寫成 `docs/adr/0001-*.md`。
6. 告訴 Claude / Codex / ChatGPT：「請先讀 CLAUDE.md，遵守 docs/CLAUDE.md 的文件路由規則。」


## Upgraded Template Notes

This version adds a broader AI-assisted engineering structure while keeping startup context small. New reference files are retrieved only when relevant:

- `docs/conventions.md` for coding style and error-handling rules.
- `docs/dependencies.md` for dependency adoption and rejection records.
- `docs/data.md` for data contracts, API shapes, migrations, and cache rules.
- `docs/ui.md`, `docs/html-guidelines.md`, `docs/design-system.md`, and `docs/accessibility.md` for UI / HTML decisions.
- `docs/tasks/task-template.md` and `docs/tasks/ui-task-template.md` for larger task planning.
- `docs/release.md` for release and rollback notes.

## Initialization Checklist

After copying this template into a real project:

- [ ] Replace project overview in `CLAUDE.md`.
- [ ] Replace placeholders in `docs/project.md`.
- [ ] Replace placeholders in `docs/memory/current.md`.
- [ ] Replace placeholders in `docs/tasks/active.md`.
- [ ] Update build/test commands in `CLAUDE.md` and `docs/testing.md`.
- [ ] Fill `docs/conventions.md`, `docs/dependencies.md`, and `docs/data.md` only with durable rules.
- [ ] Fill UI docs only if the project has UI / HTML work.
- [ ] Add first proposed or accepted ADR if architecture is already known.
- [ ] Run `npm run docs:refresh`.

## Strict Placeholder Check

The template intentionally contains placeholders such as `<PROJECT_NAME>`. Normal `npm run docs:refresh` warns but does not fail on placeholders. For a real project, run:

```bash
STRICT_PLACEHOLDERS=1 npm run docs:guard-placeholders
```

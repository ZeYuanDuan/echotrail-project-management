# EchoTrail Project Management

「曼陀號 PM x ENG 合作專案 EchoTrail」專案資料庫，也是 **EchoTrail 產品規格的單一真實來源（single source of truth）**。
所有「產品要做什麼、為什麼這樣做、還有什麼沒決定」都寫在這裡，用 Git 管版本；小改動兩位 PM 可直接推 `main`，較大改動走 Pull Request 互相審閱。工程師夥伴與 mentor 也在同一個 repo 裡讀 spec、留意見，AI 能在同一份脈絡下讀取資訊，協助專案溝通與執行。

- GitHub repo：<https://github.com/ZeYuanDuan/echotrail-project-management>
- 主要維護者：兩位 PM（Webber、Ariel）
- 協作規則詳見 [CONTRIBUTING.md](CONTRIBUTING.md)

---

## 團隊與角色

| 角色 | 成員 | Email／GitHub | 在這個 repo 做什麼 |
|---|---|---|---|
| PM | **Webber** | GitHub: `TsuWebber` | 撰寫與維護 spec，兩人皆可直接推 `main`；較大改動開 PR 互相 review |
| PM | **Ariel（羽）** | yuuronglife@gmail.com | 撰寫與維護 spec，兩人皆可直接推 `main`；較大改動開 PR 互相 review |
| 工程師 | **Alson** | GitHub: `ZeYuanDuan` | 讀 spec 實作；對規格有疑問時在 PR / Issue 留言或開 Issue；review 與實作相關的 PR |
| 工程師 | **Celine** | celinewu1010@gmail.com | 讀 spec 實作；對規格有疑問時在 PR / Issue 留言或開 Issue；review 與實作相關的 PR |
| Mentor（PM） | **Roanne** | rion0325g@gmail.com | 視需要 review PR、給規格方向建議 |
| Mentor（ENG） | **Aaron** | ninocar215@gmail.com | 視需要 review 技術可行性、給架構建議 |

> 需要存取權限找 Webber（或 repo owner Alson）到 repo **Settings → Collaborators** 用上面 Email 或 GitHub 帳號加人；對方接受邀請、確定 GitHub 使用者名稱後，請把上表 Email 欄位換成 GitHub 帳號。

---

## 開始使用

```bash
git clone https://github.com/ZeYuanDuan/echotrail-project-management.git
cd echotrail-project-management
```

推送時用 GitHub 帳號登入（`gh auth login`，或帳號填 GitHub 使用者名稱、密碼貼 **Personal Access Token**——GitHub 右上頭像 → Settings → Developer settings → Personal access tokens → Generate new token，勾 `repo`）。

---

## Repo 內容

| 文件 | 用途 | 狀態 |
|---|---|---|
| [EchoTrail-MVP-SPEC.md](EchoTrail-MVP-SPEC.md) | 目前**已定案**的 MVP 規格（「現在是什麼」），依 A／B／C 功能分組 | 主文件 |
| [EchoTrail-DECISIONS.md](EchoTrail-DECISIONS.md) | 決策脈絡（為什麼）與**尚未拍板**的開放問題 | 主文件 |
| [CHANGELOG.md](CHANGELOG.md) | spec 變更的一句話摘要，按日期，給人快速掃 | 主文件 |
| [CONTRIBUTING.md](CONTRIBUTING.md) | 協作流程與 commit / PR 慣例 | 規範 |
| [CLAUDE.md](CLAUDE.md) | Claude Code 專案指示：改 SPEC 時自動走 log-decision／log-changelog | 工具 |
| [archive/](archive/) | 已被併入或取代的歷史版本，僅供追溯，不再維護 | 封存 |
| `.claude/skills/` | Claude Code skills，見下方〈用 Claude Code 維護〉 | 工具 |

### 三份主文件的分工

| 想知道… | 看哪份 |
|---|---|
| 現在的規格是什麼 | **SPEC** |
| 這條規格當初為什麼這樣定、考慮過什麼 | **DECISIONS**〈一、決策紀錄〉對應條目 |
| 還有什麼沒決定 | **DECISIONS**〈二、開放問題〉，或 repo [Issues](https://github.com/ZeYuanDuan/echotrail-project-management/issues) |
| 最近 spec 改了哪些東西 | **CHANGELOG** |

規則：**改 SPEC 定案內容時，同一次改動內一起更新 DECISIONS 對應條目、並在 CHANGELOG 補一句。**（不管是直接推 main 還是走 PR）下方的 skill 會提醒你做這件事。

---

## 協作流程（重點摘要）

完整版見 [CONTRIBUTING.md](CONTRIBUTING.md)。

1. 兩位 PM 都可以**直接推 `main`**——小修正、雙方已經口頭對過的改動適用。
2. 改動較大、牽涉多章節、還沒跟對方對過、想讓對方先看過再定案 → **開分支走 PR**，指定另一位 PM（必要時加 mentor）review，approve 後 merge、刪分支。**不要 merge 自己的 PR。**
3. 不管走哪條路，一次改動只處理一個議題；標題以規格章節開頭（`B-2 ...`）或 `docs:`。
4. push 前先 `git pull`，避免覆蓋對方剛推的東西。
5. 未拍板的事：寫進 DECISIONS 開放問題，或開一個 Issue 追蹤。

### Issue 用法

- 規格上的疑問、待確認事項、發現的矛盾 → 開 Issue，標題講清楚問題。
- 工程師實作時發現 spec 講不清楚 / 不可行 → 開 Issue tag 對應 PM。
- Issue 有結論後：把結論寫回 DECISIONS，關閉 Issue。

---

## 用 Claude Code 維護

在這個資料夾裡用 **Claude Code**，三個 skill 涵蓋日常維護。clone 下來就有，全 team 都能用。

| 說這句 | 觸發 | 做什麼 |
|---|---|---|
| 「**推 spec**」「幫我開 PR」 | [`push-spec`](.claude/skills/push-spec/SKILL.md) | 問你要直接推 `main` 還是開 PR（給判斷依據），照選擇 commit、push，PR 的話給你連結 |
| 「**記 decision**」「這個決定記下來」「第X題有結論了」 | [`log-decision`](.claude/skills/log-decision/SKILL.md) | 把決策（決定什麼／為什麼／推翻什麼／誰拍板）寫進 `DECISIONS.md`〈決策紀錄〉，並把對應的開放問題標記為已解決 |
| 「**記 changelog**」「這次改動記一下」 | [`log-changelog`](.claude/skills/log-changelog/SKILL.md) | 把這次變更整理成一句話，加進 `CHANGELOG.md` 最上面 |

一次完整的 spec 變更 = 改 SPEC（`push-spec`）＋ `log-decision` ＋ `log-changelog`。

`log-decision`／`log-changelog` 不用特地開口——[CLAUDE.md](CLAUDE.md) 已經指示 Claude Code：**只要這次任務改了 SPEC 的定案內容，結束前會主動記 DECISIONS 與 CHANGELOG**，不等你要求。`push-spec` 仍需你明確說「推 spec」才會動，不會自動推。

這些 skill 會直接推 `main`（若你選這條路），但**不會**代你在 GitHub 網站上開 PR / 指定 reviewer / merge（牽涉帳號，自己點）。

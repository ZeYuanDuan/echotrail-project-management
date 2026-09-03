# EchoTrail 共鳴旅歷 — Spec Repo

這個 repo 是 **EchoTrail 產品規格的單一真實來源（single source of truth）**。
所有「產品要做什麼、為什麼這樣做、還有什麼沒決定」都寫在這裡，用 Git 管版本、用 Pull Request 做審閱。

- Gitea repo：<https://gitea.com/EchoTrail/echotrail-spec>（Private）
- 主要維護者：兩位 PM（Webber、Ariel）
- 協作規則詳見 [CONTRIBUTING.md](CONTRIBUTING.md)

---

## 團隊與角色

| 角色 | 成員 | 在這個 repo 做什麼 |
|---|---|---|
| PM | **Webber**（gitea: `TSUWEBBER`）、**Ariel（羽）** | 撰寫與維護 spec，開 PR、互相 review 後 merge |
| 工程師 | **Alson**、**Celine** | 讀 spec 實作；對規格有疑問時在 PR / Issue 留言或開 Issue；review 與實作相關的 PR |
| Mentor（PM） | **Roanne** | 視需要 review PR、給規格方向建議 |
| Mentor（ENG） | **Aaron** | 視需要 review 技術可行性、給架構建議 |

> gitea 帳號對照：加入 repo 後請把自己的 gitea 使用者名稱補進上表。
> 需要存取權限找 Webber 到 repo **Settings → Collaborators** 加人。

---

## 開始使用

```bash
git clone https://gitea.com/EchoTrail/echotrail-spec.git
cd echotrail-spec
```

第一次用 Git 推送時，帳號填 gitea 使用者名稱、密碼貼 **Personal Access Token**
（gitea 右上頭像 → Settings → Applications → Generate New Token，勾 `repo`）。

---

## Repo 內容

| 文件 | 用途 | 狀態 |
|---|---|---|
| [EchoTrail-MVP-SPEC.md](EchoTrail-MVP-SPEC.md) | 目前**已定案**的 MVP 規格（「現在是什麼」），依 A／B／C 功能分組 | 主文件 |
| [EchoTrail-DECISIONS.md](EchoTrail-DECISIONS.md) | 決策脈絡（為什麼）與**尚未拍板**的開放問題 | 主文件 |
| [CHANGELOG.md](CHANGELOG.md) | spec 變更的一句話摘要，按日期，給人快速掃 | 主文件 |
| [CONTRIBUTING.md](CONTRIBUTING.md) | 協作流程與 commit / PR 慣例 | 規範 |
| [archive/](archive/) | 已被併入或取代的歷史版本，僅供追溯，不再維護 | 封存 |
| `.claude/skills/` | Claude Code skills，見下方〈用 Claude Code 維護〉 | 工具 |

### 三份主文件的分工

| 想知道… | 看哪份 |
|---|---|
| 現在的規格是什麼 | **SPEC** |
| 這條規格當初為什麼這樣定、考慮過什麼 | **DECISIONS**〈一、決策紀錄〉對應條目 |
| 還有什麼沒決定 | **DECISIONS**〈二、開放問題〉，或 repo [Issues](https://gitea.com/EchoTrail/echotrail-spec/issues) |
| 最近 spec 改了哪些東西 | **CHANGELOG** |

規則：**改 SPEC 定案內容時，同一個 PR 內一起更新 DECISIONS 對應條目、並在 CHANGELOG 補一句。** 下方的 skill 會提醒你做這件事。

---

## 協作流程（重點摘要）

完整版見 [CONTRIBUTING.md](CONTRIBUTING.md)。

1. **不直接 push 到 `main`**，一律開分支走 Pull Request。
2. 一個 PR 只處理一個議題；PR 標題以規格章節開頭（`B-2 ...`）或 `docs:`。
3. PR 至少一位 reviewer approve 後才 merge：
   - 規格內容 → 另一位 PM review（必要時找 mentor Roanne）
   - 牽涉實作可行性 → 找工程師或 mentor Aaron review
4. merge 後刪掉分支。
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
| 「**推 spec**」「幫我開 PR」 | [`push-spec`](.claude/skills/push-spec/SKILL.md) | 從最新 `main` 開 `spec/<主題>` 分支、按慣例 commit、push，給你開 PR 的連結 |
| 「**記 decision**」「這個決定記下來」「第X題有結論了」 | [`log-decision`](.claude/skills/log-decision/SKILL.md) | 把決策（決定什麼／為什麼／推翻什麼／誰拍板）寫進 `DECISIONS.md`〈決策紀錄〉，並把對應的開放問題標記為已解決 |
| 「**記 changelog**」「這次改動記一下」 | [`log-changelog`](.claude/skills/log-changelog/SKILL.md) | 把這次變更整理成一句話，加進 `CHANGELOG.md` 最上面 |

一次完整的 spec 變更 = 改 SPEC（`push-spec` 開 PR）＋ `log-decision` ＋ `log-changelog`，三者放同一個 PR。`push-spec` 會提醒你別漏。

這些 skill **不會**直接 push `main`，也不會代你在 gitea 網站上開 PR / 指定 reviewer / merge（牽涉帳號，自己點）。

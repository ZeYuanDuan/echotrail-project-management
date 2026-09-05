# EchoTrail Spec Repo — 專案指示

這是 EchoTrail 產品規格的單一真實來源。完整背景見 [README.md](README.md)、協作規則見 [CONTRIBUTING.md](CONTRIBUTING.md)。

## 改 SPEC 時，主動走完整套流程——不用等使用者要求

只要這次任務**改動了 `EchoTrail-MVP-SPEC.md` 的定案內容**（新增/修改/刪除功能、規則、Scope 範圍等——不含純粹讀取、討論、或只改 DECISIONS/CHANGELOG 本身），在任務**結束前**，主動、不需使用者額外開口：

1. 用 `log-decision` skill，把這次改動的決策脈絡（改了什麼、為什麼、推翻了什麼、誰拍板）寫進 `EchoTrail-DECISIONS.md`。
   - 若這次已經直接手動編輯過 `EchoTrail-DECISIONS.md`、內容已經涵蓋這次變更，不用再跑一次 skill 重複記錄——但仍要確認條目確實存在。
2. 用 `log-changelog` skill，在 `CHANGELOG.md` 補一句話摘要。
   - `log-decision`／`log-changelog` 都要標改動者：`git config user.name` 對照 [README](README.md#團隊與角色) 換算成姓名，換不出來就用原始值，不要留空、不要用猜的。
3. **不要**主動呼叫 `push-spec`／執行 `git push`——是否送出、直接推 main 還是開 PR，等使用者明確要求再做。

例外：使用者明確說「先不要記」「這只是討論，還沒定案」「先別動 DECISIONS/CHANGELOG」時，不觸發上述流程。

## 三份主文件的分工

| 想知道… | 看哪份 |
|---|---|
| 現在的規格是什麼 | [EchoTrail-MVP-SPEC.md](EchoTrail-MVP-SPEC.md) |
| 這條規格當初為什麼這樣定、考慮過什麼 | [EchoTrail-DECISIONS.md](EchoTrail-DECISIONS.md)〈一、決策紀錄〉 |
| 還有什麼沒決定 | [EchoTrail-DECISIONS.md](EchoTrail-DECISIONS.md)〈二、開放問題〉 |
| 最近改了哪些東西 | [CHANGELOG.md](CHANGELOG.md) |

SPEC 只放**已定案**的規格結果，不放討論過程與日期標記；決策脈絡與待確認事項一律進 DECISIONS，不要混進 SPEC 本文（開放問題可用 🟡／🚩 標記直接寫在對應章節提醒讀者，但完整脈絡仍記在 DECISIONS）。

## 编修慣例

- 改動前後跑一次完整性檢查：`### ` 標題數與 `驗收條件` 出現次數應該一致（登入等無編號小節除外，會讓驗收條件數略多於編號標題數，屬正常）。
- 涉及編號重排（插入/合併/刪除功能）時，全文交叉引用（Scope、Figma/Wireframe、各章節內部提及的其他章節編號）都要跟著同步，改完務必全文搜尋確認沒有殘留舊編號。
- 若有發布給 PM 閱讀的手機版規格 Artifact，SPEC 改完後也要同步更新該 Artifact，保持兩邊一致。

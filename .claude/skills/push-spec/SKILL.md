---
name: push-spec
description: 把新的或改過的 EchoTrail spec 推上 gitea.com——直接推 main，或開分支＋Pull Request 給另一位 PM review，兩種都支援。當使用者說「推 spec」「上傳 spec」「spec 改好了要送出」「幫我開 PR」「push spec」或類似意圖，且工作目錄是 echotrail-spec repo 時使用。
---

# push-spec

把目前工作目錄裡改好的 spec 變更，依 `CONTRIBUTING.md` 的協作規則推上 gitea.com。
兩位 PM 都可以直接 push `main`；PR 是想讓對方先看過再合時才用的選項，不是強制流程。

## 前置檢查

1. 確認在正確的 repo：

   ```bash
   git remote get-url origin
   ```

   必須是 `https://gitea.com/EchoTrail/echotrail-spec.git`（或同 repo 的 ssh 形式）。不是的話停下來，告訴使用者這個 skill 只適用於 echotrail-spec repo。

2. 看有哪些變更，秀給使用者確認：

   ```bash
   git status --short
   git diff --stat HEAD
   ```

   - 沒有任何變更（工作區乾淨且沒有未推的 commit）→ 告訴使用者沒東西可推，結束。
   - 有變更 → 用一兩句話摘要「改了哪些檔、大概改了什麼」，請使用者確認這就是要送出的內容。

## 決定走哪條路

3. 如果使用者已經講清楚（「直接推 main」「開個 PR」），照做。沒講清楚就問，並給判斷依據：

   - **小修正**（錯字、措辭、格式）、**雙方已經口頭對過**的改動 → 建議直接推 main
   - **影響多個章節、改動較大、還沒跟對方對過、想讓對方先看過** → 建議開 PR

   不確定就預設建議開 PR（成本不高、比較保險），但使用者說要直接推就照辦，不要堅持。

4. 這次若動到 SPEC 的規格內容，提醒使用者：接下來（不管走哪條路）記得一起
   - 用 `記 decision`（log-decision skill）把決策脈絡寫進 `EchoTrail-DECISIONS.md`
   - 用 `記 changelog`（log-changelog skill）在 `CHANGELOG.md` 補一句摘要
   使用者要的話就先觸發那兩個 skill，改完再回來繼續。

5. 如果這次**新增了一份 spec 檔**，順便更新 `README.md` 的「文件導覽」表格，加一列。

---

## 路徑 A：直接推 main

6a. 同步最新 main（保留未 commit 的變更）：

   ```bash
   git stash push -u -m push-spec-tmp    # 只有在有未 commit 變更時才做
   git checkout main
   git pull --ff-only
   git stash pop                          # 對應上面有 stash 才做
   ```

7a. 加要送出的檔案、commit（訊息慣例見下方）：

   ```bash
   git add <改到的 .md 檔...>
   git commit -m "B-2 結果頁文案定稿

   把原本兩段合併為一段，語氣改得更貼近 persona；DECISIONS B-2 補上決策理由。"
   ```

8a. 推：

   ```bash
   git push origin main
   ```

   若被拒絕（remote 有新 commit）：`git pull --rebase` 後重推；有 conflict 就秀給使用者，不要自己猜著解。

9a. 回報：commit 標題、已同步到 origin/main。

---

## 路徑 B：開分支 + PR

6b. 問使用者這次改動的**主題**（短，用來當分支名，例如 `結果頁文案`、`新增-onboarding-spec`），對應的**規格章節**（`A-4`、`B-2`、`C-7`；純文件性的用 `docs`）。

7b. 從最新 main 開分支（保留未 commit 的變更）：

   ```bash
   git stash push -u -m push-spec-tmp    # 只有在有未 commit 變更時才做
   git checkout main
   git pull --ff-only
   git checkout -b spec/<主題>
   git stash pop                          # 對應上面有 stash 才做
   ```

   分支名用 kebab-case，中文可保留，例如 `spec/結果頁文案`。

8b. 加檔案、commit（訊息慣例見下方）：

   ```bash
   git add <改到的 .md 檔...>
   git commit -m "B-2 結果頁文案定稿

   把原本兩段合併為一段，語氣改得更貼近 persona；DECISIONS B-2 補上決策理由。"
   ```

9b. 推分支：

   ```bash
   git push -u origin spec/<主題>
   ```

10b. 產生開 PR 的連結給使用者：

   ```
   https://gitea.com/EchoTrail/echotrail-spec/compare/main...spec/<主題>
   ```

11b. 告訴使用者接下來手動做（牽涉帳號，Claude 不代做）：
   - 點上面連結 → 填 PR 標題（可沿用 commit 標題）與說明
   - Reviewers 指定另一位 PM（必要時加 mentor）
   - **不要自己 merge 自己的 PR**；對方 review 過再由對方或自己 merge，merge 後刪分支

12b. 回報：分支名、已推的 commit 標題、PR 連結。

---

## commit 訊息慣例（兩條路徑通用）

- 標題以章節開頭：`A-4 ...`、`B-2 ...`、`C-7 ...`；非章節性的用 `docs:`、`pitch:`。
- 內文一句話交代**為什麼這樣改**。

## 事後（走過 PR 的話）

- 使用者說「PR 過了 / merged」之後：
  ```bash
  git checkout main && git pull --ff-only && git branch -d spec/<主題>
  ```

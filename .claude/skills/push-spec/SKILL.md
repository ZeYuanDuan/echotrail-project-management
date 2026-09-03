---
name: push-spec
description: 把新的或改過的 EchoTrail spec 推上 gitea.com，開成分支 + Pull Request 給另一位 PM review。當使用者說「推 spec」「上傳 spec」「spec 改好了要送出」「幫我開 PR」「push spec」或類似意圖，且工作目錄是 echotrail-spec repo 時使用。
---

# push-spec

把目前工作目錄裡改好的 spec 變更，依 `CONTRIBUTING.md` 的協作規則，安全地推成一條分支並開 Pull Request。**絕不直接 push 到 `main`。**

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

3. 如果變更已經被 commit 在**本機 `main`** 上（不該發生但要處理）：
   - 記下這些 commit 的 hash，`git branch <新分支名> main`，然後 `git reset --hard origin/main` 把本機 main 拉回，再 `git checkout <新分支名>` 繼續。做之前先跟使用者說明。

## 建立分支

4. 問使用者兩件事（如果對話裡已經講清楚就不用問）：
   - 這次改動的**主題**（短，用來當分支名，例如 `結果頁文案`、`新增-onboarding-spec`）
   - 對應的**規格章節**（例如 `A-4`、`B-2`、`C-7`；純文件性的就用 `docs`）

5. 從最新的 main 開分支（保留目前未 commit 的變更）：

   ```bash
   git stash push -u -m push-spec-tmp    # 只有在有未 commit 變更時才做
   git checkout main
   git pull --ff-only
   git checkout -b spec/<主題>
   git stash pop                          # 對應上面有 stash 才做
   ```

   分支名用 kebab-case，中文可保留，例如 `spec/結果頁文案`。

## Commit

6. 把要送出的 spec 檔加進來（只加 spec 相關檔案，不要順手把無關檔案帶進去）：

   ```bash
   git add <改到的 .md 檔...>
   ```

7. 如果這次**新增了一份 spec 檔**，同一個 commit 裡順便更新 `README.md` 的「文件導覽」表格，加一列。

7b. 這次若動到 SPEC 的規格內容，提醒使用者在**同一個 PR** 裡一起：
    - 用 `記 decision`（log-decision skill）把決策脈絡寫進 `EchoTrail-DECISIONS.md`
    - 用 `記 changelog`（log-changelog skill）在 `CHANGELOG.md` 補一句摘要
    使用者要的話就依序觸發那兩個 skill，改完再回到下面第 8 步一起 commit。

8. Commit，訊息遵守慣例：
   - 標題以章節開頭：`B-2 結果頁文案定稿` / `docs: 補充 pitch 講稿第三段`
   - 內文一句話交代**為什麼這樣改**
   - 若同時改了 `EchoTrail-MVP-SPEC.md` 的定案內容，提醒使用者（並在可能時一起）更新 `EchoTrail-DECISIONS.md` 對應條目

   ```bash
   git commit -m "B-2 結果頁文案定稿

   把原本兩段合併為一段，語氣改得更貼近 persona；DECISIONS B-2 補上決策理由。"
   ```

## 推送 + 開 PR

9. 推分支：

   ```bash
   git push -u origin spec/<主題>
   ```

10. 產生開 PR 的連結並給使用者（把分支名做 URL encode）：

    ```
    https://gitea.com/EchoTrail/echotrail-spec/compare/main...spec/<主題>
    ```

11. 告訴使用者接下來手動做（這些動作牽涉帳號，Claude 不代做）：
    - 點上面連結 → 填 PR 標題（可沿用 commit 標題）與說明
    - **Reviewers 指定另一位 PM**（Webber 開的就指定羽，羽開的就指定 Webber）
    - `main` 受保護，需 1 個 approve 才能 merge
    - **不要自己 merge 自己的 PR**；對方 review 過再由對方或自己 merge，merge 後刪分支

12. 回報：分支名、已推的 commit 標題、PR 連結。

## 事後

- 使用者說「PR 過了 / merged」之後，可協助收尾：
  ```bash
  git checkout main && git pull --ff-only && git branch -d spec/<主題>
  ```

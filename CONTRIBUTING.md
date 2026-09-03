# 協作方式

Git 是**非同步協作**：不是 Google Docs 那種即時多人游標，而是「各自改 → 開 PR → 對方 review → 合併」。
好處是每次改動都有版本、逐行 diff、討論紀錄。

## 日常流程

```bash
# 1. 先同步最新的 main
git checkout main
git pull

# 2. 開一條主題分支（一個議題／一組改動一條）
git checkout -b spec/b2-結果頁文案

# 3. 改檔案，然後 commit（訊息寫「改了什麼、為什麼」）
git add EchoTrail-MVP-SPEC.md EchoTrail-DECISIONS.md
git commit -m "B-2 結果頁文案定稿；DECISIONS 對應條目補上決策理由"

# 4. 推上去
git push -u origin spec/b2-結果頁文案
```

然後到 Gitea 網站上對這條分支開 **Pull Request**，指定 reviewer（見規則 3）。

團隊角色見 [README](README.md#團隊與角色)：spec 由兩位 PM（Webber、Ariel）維護，工程師（Alson、Celine）與 mentor（Roanne、Aaron）視需要參與 review 與討論。

## 規則（輕量即可）

1. **不直接 push 到 `main`**，一律走 PR。（請 Webber 在 repo Settings → Branches 把 `main` 設為 Protected Branch。）
2. **一個 PR 只處理一個議題**，方便 review，也方便之後回溯。
3. PR 至少一位 reviewer approve 後才 merge，merge 後刪掉分支：
   - 規格內容 → 另一位 PM review（方向性問題可再找 mentor Roanne）
   - 牽涉實作可行性 / 架構 → 找工程師或 mentor Aaron review
   - **不要 merge 自己的 PR**（除非對方已 approve 且明確請你自己 merge）
4. 改 SPEC 的定案內容時，**同一個 PR 內**一起更新 DECISIONS 對應條目。
5. 未拍板的事寫進 DECISIONS 的「開放問題」，或直接開一個 Gitea Issue 追蹤。
6. 遇到同時改同一段造成 conflict：以 DECISIONS 記錄的最新決策為準，當面對一次再合。

## commit / PR 訊息慣例

- 標題用該規格章節開頭：`A-4 ...`、`B-2 ...`、`C-7 ...`；非章節性的用 `docs:`、`pitch:`。
- 內文一句話交代「為什麼這樣改」，讓對方 review 時有脈絡。

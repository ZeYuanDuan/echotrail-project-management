# 協作方式

兩位 PM（Webber、Ariel）都可以**直接 push 到 `main`**。PR 不是強制流程，是「想讓對方先看過再合」時才用的選項。
Git 本身是非同步的：不是 Google Docs 那種即時多人游標，改動都靠 commit 留紀錄。

## 什麼時候直接推 main，什麼時候開 PR

| 情況 | 怎麼做 |
|---|---|
| 小修正（錯字、措辭、格式）、雙方已經口頭對過的改動 | **直接推 main** |
| 影響多個章節、改動較大、還沒跟對方對過、想要對方看過再定案 | **開分支 + PR**，指定對方 review |
| 不確定 | 開 PR 比較保險，成本不高 |

## 直接推 main

```bash
git checkout main
git pull
git add EchoTrail-MVP-SPEC.md EchoTrail-DECISIONS.md
git commit -m "B-2 結果頁文案定稿；DECISIONS 對應條目補上決策理由"
git push origin main
```

## 走 PR（分支）

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

然後到 Gitea 網站上對這條分支開 **Pull Request**，指定另一位 PM 或相關 mentor 當 reviewer。approve 後 merge、刪掉分支。

Claude Code 的 `push-spec` skill 會先問你要直接推 main 還是開 PR，兩種都能自動跑完，見 [README](README.md#用-claude-code-維護)。

團隊角色見 [README](README.md#團隊與角色)：spec 由兩位 PM（Webber、Ariel）維護，工程師（Alson、Celine）與 mentor（Roanne、Aaron）視需要參與 review 與討論。

## 規則（輕量即可）

1. **一次改動只處理一個議題**，commit 訊息或 PR 標題講清楚範圍，方便之後回溯。
2. **不要覆蓋對方剛推上去的東西**：push 前先 `git pull`；遇到同時改同一段造成 conflict，以 DECISIONS 記錄的最新決策為準，當面對一次再合。
3. 改 SPEC 的定案內容時，**同一次改動內**一起更新 DECISIONS 對應條目、CHANGELOG 補一句（見下方 skill）。
4. 未拍板的事寫進 DECISIONS 的「開放問題」，或直接開一個 Gitea Issue 追蹤。
5. 走 PR 時，**不要 merge 自己的 PR**（除非對方已 approve 且明確請你自己 merge）。

## commit / PR 訊息慣例

- 標題用該規格章節開頭：`A-4 ...`、`B-2 ...`、`C-7 ...`；非章節性的用 `docs:`、`pitch:`。
- 內文一句話交代「為什麼這樣改」，讓對方 review 時有脈絡。

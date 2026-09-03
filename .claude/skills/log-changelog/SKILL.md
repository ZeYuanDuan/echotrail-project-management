---
name: log-changelog
description: 把這次的 spec 變更整理成一句話，加進 CHANGELOG.md。當使用者說「記 changelog」「更新 changelog」「這次改動記一下」「log changelog」或在改完 spec 想留一筆變更摘要時使用。工作目錄需為 echotrail-spec repo。
---

# log-changelog

在 `CHANGELOG.md` 最上面加上這次 spec 變更的**一句話摘要**。給人快速掃「spec 改了什麼」，不寫理由（理由寫 DECISIONS）。

## 這個 skill 只負責

CHANGELOG.md 的條目。**不碰** SPEC 內容、**不碰** DECISIONS。
一次完整的 spec 變更通常是：改 SPEC（走 push-spec 開 PR）＋ 記 DECISIONS（log-decision）＋ 記 CHANGELOG（本 skill），三者可在同一個 PR 裡。

## 步驟

1. 確認 repo：`git remote get-url origin` 要是 `echotrail-spec`。不是就停下。
   若 `CHANGELOG.md` 不存在，用現有格式建一個（標題 + 說明 + `---`）。

2. 抓出「這次改了什麼」，依情境擇一：
   - 目前在一條 spec 分支上 → `git diff --stat origin/main...HEAD` 加上 `git log origin/main..HEAD --format='%s'`
   - 使用者指定某個 PR → 問 PR 編號，看該 PR 的 commit 訊息與檔案
   - 都沒有，使用者用講的 → 照使用者描述
   秀出你的理解，請使用者確認。

3. 把變更拆成**逐條一句話**，每條格式：

   ```
   - `類別` 章節或範圍：一句話。#<PR編號>
   ```

   - 類別：`新增` / `變更` / `移除` / `更名` / `修正`
   - 章節用 SPEC 代號（`A-4`、`B-2`、`C-7`）；跨章節或非章節性的用「範圍」文字（例如「Background」「側邊欄」「文件」）
   - 一句話只講「變成什麼」，不講「為什麼」
   - PR 編號未知就先留 `#TBD`，PR 開好後補；沒有 PR（直接改 main 的少數情況）就省略

4. 找 `## <今天日期 YYYY-MM-DD>` 這個標題：
   - 已存在 → 把新條目**加在該日期區塊的條目最後**
   - 不存在 → 在 `---` 之後、最新日期區塊**之上**插入新的 `## YYYY-MM-DD` 區塊
   （日期新的永遠在上）

5. `git --no-pager diff CHANGELOG.md` 秀出來給使用者看。

6. 收尾：
   - 如果同一批還要改 SPEC / DECISIONS，提醒接著用 `log-decision` 記決策脈絡，再用 `推 spec`（push-spec）把整批一起開 PR。
   - 如果只有 CHANGELOG 這一個檔要動，一樣走 `推 spec` 開 PR（DECISIONS 與 CHANGELOG 的變更也照 CONTRIBUTING.md 走 PR）。

## 寫作風格

對齊現有條目：簡短、動詞開頭、繁中、代號大寫。一條講不完就拆成兩條，不要塞成一長句。

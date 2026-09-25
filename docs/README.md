# 支援文件導覽

`docs/` 放實作、測試與演示用的支援性資料。已定案的產品規格、決策脈絡與變更摘要仍以 repo 根目錄的 `EchoTrail-MVP-SPEC.md`、`EchoTrail-DECISIONS.md` 與 `CHANGELOG.md` 為準。

## 目錄

- [`ai/`](ai/)：AI prompt、版本變更說明與資料範例。
- [`demos/`](demos/)：Demo 路徑、故事腳本與測試情境。

## 新增文件時

- 橫跨多項功能的已定案規格，應整併回根目錄的 MVP SPEC，不在 `docs/` 建立第二份主規格。
- 可執行的 prompt 放在 `ai/system-prompts/`，並在檔名保留版本號。
- 版本間的工程調整說明放在 `ai/migrations/`。
- 假資料、seed 與輸入輸出範例放在 `ai/examples/`，不與規格文本混放。
- 資料過時後移到 `archive/`，並在檔案開頭標示取代來源與封存原因。

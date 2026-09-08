# CHANGELOG

EchoTrail spec 的變更摘要，**新的在上**。每筆一句話，細節看對應 PR 與 [EchoTrail-DECISIONS.md](EchoTrail-DECISIONS.md)。

類別標記：`新增` / `變更` / `移除` / `更名` / `修正`。
章節代號對應 [EchoTrail-MVP-SPEC.md](EchoTrail-MVP-SPEC.md) 的 A／B／C 分組。
每條結尾標註改動者 `（姓名）`，方便協作時知道找誰確認。

維護方式：改 spec 時用 Claude Code 說「**記 changelog**」，見 [.claude/skills/log-changelog](.claude/skills/log-changelog/SKILL.md)。

---

## 2026-09-09

- `變更` A-4 System Prompt 草稿改寫為 v2：從精神喊話擴充為可直接實作的完整 prompt（7 區塊＋好／壞回應對照），對齊 4 必填欄位／三段式／每輪一題／收尾時機。（Webber）
- `變更` A-4「四、批次模式與深挖模式」整節標記 Part 2，第一輪 MVP 只實作批次模式；連帶 A-4 功能概述、§二、A-5、B-2 的深挖模式引用同步加註 Part 2。（Webber）
- `修正` B-2 功能概述：「使用者完成 A-4 深挖對話」改為「完成 A-4 多輪對話（批次模式）」，批次模式本來就會產出 Echo Card。（Webber）

## 2026-09-08

- `變更` A-4 核心規則：MVP 不在任何階段設輸入品質 gate，拿掉「品質交給 B-2 信心分數／匹配分數把關」的說法。（Webber）
- `變更` A-4 輪數上限：軟＋硬雙層併為單一上限 8 輪，到頂只跳 CTA、永不強制結束對話；「資訊不完整」改綁「必填未齊就點 CTA」，與輪數脫鉤。（Webber）
- `變更` A-4 必填欄位由「事件內容／時間／情緒用字」改為 4 欄（事件內容、情緒用字、在意的點、不能接受的點），時間降為非必填；必填欄位以「從下游 output 反推」定義。（Webber）
- `變更` A-4「算有值」判準改綁下游 LLM 可用性；新增規則 5「蒐集深度指引（非 gating）」。（Webber）
- `變更` A-4 Rephrase／Skip 降為 Nice to Have（非本輪 MVP 必做）。（Webber）
- `變更` A-4 整段重整為六個編號小節，新增「下游 output ↔ 需要欄位」對照表。（Webber）
- `新增` Scope：C-8 RIASEC 長條圖、C-9 DISC 象限圖 重新納入 MVP Part 1（推翻 260901 移入 Part 2）。（Webber）
- `變更` SPEC 標題層級明確化：功能群組 `###` → 單一功能 `####` → A-4 內部小節 `#####`；登入／側邊欄升為功能標題；Part 2 功能標題加 `· Part 2` 標記。CLAUDE.md 完整性檢查同步改為數 `####`。（Webber）

## 2026-09-06

- `移除` DECISIONS〈二、開放問題〉24項全數歸零重來，原內容封存於 `archive/EchoTrail-DECISIONS-開放問題_260906前封存.md`，不代表已解決。（Webber）
- `移除` Figma / Wireframe 清單精簡為三項（Prototype可互動版、Pitch Deck、競品參考tryapt.ai），拿掉Prototype v3/v4、第三小組流程圖、Figma流程圖260830補充、完整腳本提示詞四個連結。（Webber）

## 2026-09-05

- `新增` 登入（簡易命名對應）：使用者輸入名字直接對應使用者ID，不做密碼／Email驗證。（Webber）
- `新增` A-4 艾可 System Prompt 草稿（教練人設核心精神，不洩漏系統內部術語）。（Webber）
- `新增` A-4 Echo Insights LLM 判斷邏輯：對照 Echo Card 六欄位追問，每次最多3題。（Webber）
- `新增` A-5〈產生洞察〉按鈕觸發機制：按鈕本質是自動送出「Please Generate my insight」的保留字指令。（Webber）
- `新增` A-5 Echo Card 各欄位 LLM 生成規則（事件的發生／我的情緒bullet格式、我在意／我討厭、我的價值主張）。（Webber）
- `新增` C-2 Persona卡片引言句生成規則（動機價值基礎＋職稱組合句）。（Webber）
- `變更` C-3 驅動卡片主視覺改為三圈交集Venn圖，原三卡片內容改為展開檢視。（Webber）
- `新增` C-4 文字雲兩種候選收集法（離散情緒標記／LLM自定義關鍵字），尚未定案。（Webber）
- `新增` C-5 行為模式排行收集法：從客觀事件萃取行為導向，取前3名。（Webber）
- `新增` C-7／C-8／C-9 完整技術方案：逐事件記分、累加平均；C-9附完整DISC座標轉換公式。（Webber）
- `變更` Scope 大幅縮範圍，改為只列本輪 MVP 實際範圍（登入、側邊欄、A-1／A-2／A-4／A-5、B-2、C-2／C-3／C-4／C-5／C-7／C-10），A-3、B-1（完整視覺化）／B-3／B-4／B-5／B-6、C-1／C-6／C-8／C-9 移入 Part 2。（Webber）
- `變更` 文件：spec repo 從 gitea 遷移至 GitHub（echotrail-project-management），README／CONTRIBUTING／push-spec skill 同步更新連結。（Webber）

## 2026-08-30

- `新增` 第三種 persona 類型「倦怠焦慮者」（有情緒×沒行動），與羽絨、Webber 並列，同步補進 SPEC Background。
- `變更` A 組插入 **A-3 語音輸入**，整組重新編號（多輪對話→A-4、產生洞察按鈕→A-5）。
- `變更` A-2、A-3 合併為單一「履歷與快速匯入冷啟動」入口；冷啟動入口由三種收斂為兩種；SPEC 功能數 22 → 21。
- `變更` A-5 產生洞察流程改為兩個獨立按鈕（〈產生洞察〉→〈是，請更新到 Dashboard〉），跳轉終點由 My Trail 改為 Dashboard。
- `變更` B-3／B-4 順序對調（新序：B-3 整體洞察、B-4 跳轉對話按鈕）。
- `新增` 側邊欄（全域導覽）定義：〈+New〉〈My Trail〉〈My Dashboard〉。
- `更名` A-5「時間軸／儀表板跳轉」→「產生洞察按鈕」；C-3「驅動卡片」→「驅動卡片（共鳴之錨）」。
- `新增` Figma 流程圖、可互動 Prototype、Pitch Deck 三個連結寫入 SPEC。

## 2026-08-29

- `變更` A-2 履歷由「唯一必填」改為非必填，改用 UI 強烈引導；無客觀資料時 B-2／B-4 顯示空狀態。
- `變更` C-4 文字雲範圍擴大為「情緒詞＋能力詞」兩類並存。
- `變更` Background 新增痛點 3（累積事件缺乏歸納）；Goal 由單一驗證目標擴為兩個。
- `修正` 全文一致性掃描：B-2 欄位命名、B-4 資料結構、Scope C-4 說明同步更新。
- `新增` SPEC / DECISIONS 文件拆分，SPEC 只留規格結果，決策過程與待確認移至本 repo 的 DECISIONS.md。

## 2026-08-28

- `變更` B 組重整為 B-1～B-6；移除「確認式對話」流程，改為「跳回 A-4」或「直接編輯卡片」。
- `新增` B-5 篩選器、B-6 情緒曲線（B-6 由 Part 2 移入 Part 1）。
- `變更` B-2 資料結構定為 Echo Card 六欄位，取代舊三欄位；匹配分數改為 LLM 自評 0–100。
- `變更` C 組重整為 C-1～C-10；捨棄「能力傾向儀表板」規則型長條圖，統計邏輯併入 C-4 文字雲。
- `新增` C-1 版面配置（Dashboard 整頁排版骨架）。

## 2026-08-27

- `變更` A 組重整為 A-1～A-5，改為入口／流程導向；「事件時間判斷」「專案標籤」併入 A-4。
- `變更` A-4 多輪對話四項核心規則拍板（必要欄位門檻、軟＋硬上限輪數、提前結束時機、反問邏輯）。
- `變更` A-5 定案為 CTA 按鈕，觸發「分析→產卡→確認→跳轉」序列。

## 2026-08-26

- `新增` 專案起點：依羽的《EchoTrail Prototype 完整腳本規格提示詞》整理為正式規格文件。
- `變更` Persona 摘要卡與三項職涯測評（職涯錨點雷達圖／RIASEC／DISC）由 Part 2 移入 Part 1。

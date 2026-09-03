# EchoTrail 共鳴旅歷 — Spec Repo

兩位 PM（Webber、羽）共同維護 EchoTrail 產品規格的地方。
協作方式見 [CONTRIBUTING.md](CONTRIBUTING.md)。

## 要推 spec 上去時

在這個資料夾裡對 Claude Code 說「**推 spec**」，會觸發 [`push-spec` skill](.claude/skills/push-spec/SKILL.md)：
自動開分支、commit、push，並給你開 Pull Request 的連結。兩人 clone 後都能用。

## 文件導覽

| 文件 | 用途 | 狀態 |
|---|---|---|
| [EchoTrail-MVP-SPEC.md](EchoTrail-MVP-SPEC.md) | 目前已定案的 MVP 規格（「現在是什麼」），A／B／C 功能分組 | 主文件 |
| [EchoTrail-DECISIONS.md](EchoTrail-DECISIONS.md) | 決策脈絡與尚未拍板的開放問題（「怎麼決定成這樣、還有什麼沒決定」） | 主文件 |
| [archive/](archive/) | 已被併入或取代的歷史版本，僅供追溯 | 封存 |

## 兩份主文件的關係

- **SPEC** 只放已定案的規格結果，不放討論過程。
- **DECISIONS** 保留討論過程，並追蹤未決事項；條目與 SPEC 章節（A-4、B-2、C-7…）互相對照。
- 改 SPEC 的同時，記得回頭更新 DECISIONS 對應條目。

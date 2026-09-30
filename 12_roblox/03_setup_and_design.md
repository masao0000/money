# 03 開発の準備と、最小の版の設計図 / Setup Guide and First-Version Design

作成：2026-09-30 ／ 対象：`02_concept.md` の「かかしの夜」
> 登録・支払い・公開は、本人と保護者が行う。この文書は手順と設計だけ。
*This file explains how to set up your tools and how to build the first small version.*

---

## 1. 準備の手順（順番どおりに）/ Setup Steps

| # | やること | 誰が | 注意 |
|---|---|---|---|
| 0 | 保護者に説明して同意をもらう：①アカウントの年齢確認（顔による年齢推定）②2段階認証 ③**Roblox Plus（月4.99ドル）を2か月**、または返金される一時金 ④換金（DevEx）の同意と口座 ⑤月の上限 | 本人＋保護者 | 16歳未満に広げる審査の条件（`01_analysis.md` §3）。Plusの2か月は約1,500円【推定：1ドル150円】 |
| 1 | **Roblox Studio**（無料）をデスクトップPC（Windows）に入れる | 本人 | — |
| 2 | Robloxのアカウントで**2段階認証**をオンにする。年齢確認をする | 本人 | 本名・学校名はプロフィールに書かない（ペンネーム） |
| 3 | **Studio の MCP を有効にして、Claude Code とつなぐ**。Studio の MCP の設定画面に出る「Claude Code」の接続方法（表示されるコマンド）をそのまま使う | 本人 | 【事実】MCPはStudioに組み込まれ、Claude Code が公式の接続先に載っている。**非公式のパッケージより、Studioに表示される公式の手順を優先**する。Claude Code の契約者・利用条件は保護者と確認（消費者向けのClaudeは18歳以上：R10-36） |
| 4 | （任意）**Rojo** を入れ、VS Code で Luau をファイルとして書き、Git で管理する | 本人 | 手順は Rojo の公式サイトに従う。最初は3だけで十分 |
| 5 | 練習：Claude Code に「Workspace に地面と木を10本置いて」と頼み、Studio に反映されるのを確認する | 本人 | ここまで1〜2時間【推定】 |

---

## 2. 最小の版の設計図 / Design of the First Version

### 2-1. 作るものの範囲（これ以外は「次の版」へ）
1. マップ1つ（りんご園：60×60程度、木・柵・収穫小屋・門・提灯）
2. 金のりんご5つ（12か所からランダム）
3. かかし（「見ている間は止まる」ルール）
4. 10分のラウンド（開始→鐘→収穫→脱出→結果）
5. 画面の表示（残りのりんご・時間・鐘までの秒数）
6. ゲームパス1つ（強い懐中電灯）と、開発者アイテム1つ（復活）

**次の版（今は作らない）**：雪の夜モード、ランキング、称号、見た目のアイテム、ペット、ロビーの飾り、多言語の手作業の翻訳

### 2-2. ファイルの構成（Rojo を使う場合の例）
```
src/
  shared/
    Config.luau            -- 時間・かかしの速さ・りんごの数などの数値（ここだけ直せば調整できる）
  server/
    GameLoop.server.luau   -- ラウンドの進行（ロビー→開始→鐘→脱出→結果）
    AppleSpawner.server.luau -- 12か所から5か所を選んで、りんごを置く・取ったら数える
    ScarecrowAI.server.luau  -- かかしの動き（見られていなければ近づく）
    Bell.server.luau       -- 2分ごとの鐘と、提灯を10秒消す演出
    Monetization.server.luau -- ゲームパス・開発者アイテムの購入の処理
  client/
    HUD.client.luau        -- 残りのりんご・時間・鐘までの秒数の表示
    Effects.client.luau    -- 暗転・音・画面のゆれ（見た目だけ）
```

### 2-3. 一番大事なルール：「見ている間は止まる」の判定
- **判定はサーバー側で行う**（利用者側の報告を信じると、ずる〔チート〕ができるため）。
- かかしごとに、各プレイヤーについて次の2つを調べ、**だれか1人でも満たせば止まる**：
  1. 向き：プレイヤーの体の正面の向きと、かかしへの方向のなす角が、視野の半分（例：45度）以内
  2. さえぎり：プレイヤーからかかしへ光線（レイキャスト）を飛ばし、壁や木にさえぎられていない
- 満たさなければ、かかしは経路探索（PathfindingService）で一番近いプレイヤーへ進む。
- 鐘で提灯が消えている10秒間は、**全員が「見ていない」扱い**になる。
- 数値（視野の角度・速さ・判定の間隔〔例：0.2秒〕）は Config.luau にまとめる。

### 2-4. お金の処理の注意
- 購入の処理は必ずサーバー側（Monetization）で行い、**購入の記録を保存してから効果を与える**（二重の付与や付与の漏れを防ぐ）。
- 価格・効果は `02_concept.md` §4。中身の分からない有料のくじは作らない。

### 2-5. Claude Code への頼み方の例（MCP でつないだ後）
1. 「Workspace に 60×60 の地面、りんごの木を30本、柵、収穫小屋、門を置いて。夜の明るさにして、提灯を20個」
2. 「ServerScriptService に GameLoop を作って。ロビー60秒→ラウンド10分→結果15秒を繰り返す。数値は ReplicatedStorage の Config にまとめて」
3. 「かかしのルールを作って：サーバー側で0.2秒ごとに、各プレイヤーの正面の向きが45度以内で、レイキャストがさえぎられていないかを調べる。だれも見ていなければ PathfindingService で近づく」
4. 「プレイテストを開始して、コンソールの出力を見せて」（MCP のテストプレイの機能）

---

## 3. 時間の割り当て（週5時間まで）/ Time Plan
| 期間 | 内容 | 時間の目安【推定】 |
|---|---|---|
| 10/1〜10/20 | 準備（§1）＋日本のヒット作を実際に遊ぶ（`01_analysis.md` の作品） | 6〜8時間 |
| 10/21〜11/14 | 最小の版（§2-1 の1〜5） | 15〜20時間 |
| 11/15〜12/15 | **作業しない**（GIA・期末考査） | 0 |
| 12/16〜12/24 | ゲームパス・調整・身内でのテスト→公開（成熟度の質問票に答える） | 6〜8時間 |
| 12/25〜 | 分析画面を見るだけ（翌日も遊ぶ人の割合・平均時間・1日の利用者） | 週0〜1時間 |

## 4. 公開のときのチェック / Before Publishing
- [ ] 成熟度とコンプライアンスの質問票に正しく答えた（軽いホラー＝Mild の想定）
- [ ] 本名・学校名・地名がゲーム内にもプロフィールにもない
- [ ] 他人のキャラクター・音楽・画像を使っていない（Roblox の Creator Store の素材は利用条件を確認）
- [ ] ゲームパスの説明が正しい（効果を大げさに書かない）
- [ ] 保護者の同意（Plus の支払い・換金）が済んでいる

## 5. 出典（確認日 2026-09-30）
| 内容 | URL | 区分 |
|---|---|---|
| Roblox Studio MCP Server（公式。単体版は開発終了し、Studio 組み込み版へ移行） | https://github.com/Roblox/studio-rust-mcp-server | 一次（直接確認） |
| Studio MCP Server Updates and External LLM Support for Assistant | https://devforum.roblox.com/t/studio-mcp-server-updates-and-external-llm-support-for-assistant/4415631 | 一次（検索結果） |
| Claude AI for Roblox Studio: Chat & MCP Workflows (2026) | https://www.obby.fun/blog/claude-ai-roblox-studio | 参考 |
| How to Connect Claude to Roblox Studio (August 2026 MCP Guide) | https://backyarddrunkard.com/game-guides/connect-claude-to-roblox-studio-mcp-guide/ | 参考 |
| Roblox Kids and Select（公開の条件） | https://create.roblox.com/docs/production/publishing/kids-and-select | 一次（直接確認） |
| Introducing Roblox Plus | https://about.roblox.com/newsroom/2026/04/introducing-roblox-plus-subscription | 一次（検索結果） |
| Creator Rewards | https://create.roblox.com/docs/creator-rewards | 一次（直接確認） |

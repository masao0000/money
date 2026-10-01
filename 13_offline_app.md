# 13 オフラインで動くスマホアプリの評価 / Offline Smartphone Apps

作成：2026-10-01 ／ 本人の質問：「オフラインでできるスマホアプリどう？」
*This file judges whether an offline smartphone app is a good way to earn money.*

---

## 1. 結論 / Conclusion
**Robloxより下**【意見】。サーバーが要らないので「手放し」には向くが、①客が来ない ②保護者の名前（とGoogle Playでは住所）が世界に公開される ③毎年の更新と固定費がかかる、の3つでRobloxに負ける。
*Offline apps need no server, but they rank below Roblox because of discovery, privacy, and yearly costs.*

| 比べる点 | オフラインのスマホアプリ | Roblox |
|---|---|---|
| 客の見つけ方 | ストアの検索（激戦）。自分で集める | Robloxがおすすめに出す（遊ばれ方で決まる） |
| 18歳未満 | **開発者登録は保護者名義**（Apple・Googleとも18歳以上） | 13歳以上で換金可（保護者の同意） |
| 公開される個人情報 | Google Playで収益化すると**登録者の氏名と住所が公開**される。Appleも契約者は保護者の本名 | ペンネームでよい |
| 固定費・手間 | Google Play：登録25ドル＋**新しい個人アカウントは12人のテスターで14日間のテストが必須**。Apple：年会費（米国99ドル。日本の金額は要確認）。両方とも**毎年のOS対応**が必要 | Roblox Plus 2か月（約1,500円）。毎年の必須の更新はない |
| サーバー費 | 0円（オフライン） | 0円（Robloxが持つ） |
| お金の分布 | 課金を入れたアプリでも、2年以内に月1,000ドルに届くのは17.3%（R9-15） | 上位に集中（くじに近い） |

---

## 2. 根拠 / Evidence
1. 【事実】Google Play：2023年11月13日以降に作った個人アカウントは、**12人以上のテスターが14日間続けて参加するクローズドテスト**をしないと公開できない（2024年12月に20人から12人へ緩和）。
2. 【事実】Google Play：有料アプリやアプリ内課金で収益化すると、**個人の開発者は本人確認と同じ氏名・住所がアプリのページに公開**される（個人開発者の報告が多数。住所を出さないためにバーチャルオフィス〔月990円前後〕や法人を使う例がある）。→ 本人が18歳未満なら、**保護者の氏名と自宅の住所**が出ることになる。
3. 【事実】Apple Developer Program は18歳以上（または成年）が条件で、未成年は保護者が契約する。
4. 【事実】Google Play は毎年、対象とするAndroidの版を上げるよう求める（2026年8月31日から新規・更新はAPI 36）。古いまま放っておくと、**新しい端末の新しい利用者に表示されなくなる**。→ 完全な放置はできない。
5. 【事実】スマホ新法（2025年12月18日に全面施行）で、外部の決済が使えるようになり手数料は下がりうる。ただし施行後も「無風」との評価があり、**未成年が保護者名義で出す条件は変わらない**。

## 3. それでもやるなら / If You Still Want to Try
- **順番を逆にする**：先にRobloxで題材を試し、遊ばれた題材だけを、18歳になってから自分の名義でスマホ版にする【意見】。
- **ストアを通さないオフラインのWebアプリ（PWA）**なら、本人の得意な技術で、年会費も住所の公開もない。ただし、客を集める道と課金の手段（Stripeは保護者がオーナー）が弱い（`02_research/R10.md` §7）。
- 保護者名義で出す場合は、**住所を公開しない手段（バーチャルオフィス）を先に用意**し、固定費（年1〜2万円台【推定】）を回収できる見込みがあるかを先に計算する。

## 4. 出典（確認日 2026-10-01）
| 内容 | URL | 区分 |
|---|---|---|
| 新しい個人用デベロッパー アカウント向けのアプリテスト要件（Play Console ヘルプ） | https://support.google.com/googleplay/android-developer/answer/14151465?hl=ja | 一次（検索抜粋） |
| 【2026年最新版】Google Playクローズドテスト完全ガイド（12人・14日） | https://bysho2.com/blog/google-play-closed-test-checklist-2026 | 参考 |
| Google Playで収益化すると氏名・住所が公開される（個人開発者の報告） | https://note.com/natty_yarrow1907/n/n9d7ba73d3e6d ／ https://qiita.com/NonamedDeveloper/items/23c4bbe3c7d4f9bc2204 | 参考 |
| Target API level requirements for Google Play apps | https://support.google.com/googleplay/android-developer/answer/11926878?hl=en | 一次（検索抜粋） |
| Apple Developer Program の年齢（未成年は保護者が契約） | https://discussions.apple.com/thread/6441831 | 参考 |
| アプリ手数料減少となる「スマホ新法」が本日18日全面施行 | https://www.businessinsider.jp/article/2512-japan-smartphone-act-apple-google/ | 参考（報道） |
| 関心がなさ過ぎて無風のスマホ新法（松村太郎） | https://news.yahoo.co.jp/expert/articles/19a2540e3bc2e7d6196e7f3c377f95cf0b0eb957 | 参考 |

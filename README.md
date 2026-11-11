# LJT Public

一般向けの Lexicosemantic Judgement Test (LJT)。登録・名前入力・CSV等のダウンロードは不要です。

- Short版（40問）: https://ryuya-dot-com.github.io/LJT-Public/short/
- Long版（160問）: https://ryuya-dot-com.github.io/LJT-Public/long/

## 動作と画面

練習4問、時間制限なし。音声が終わってからF（不適切）/J（適切）またはボタンで回答します。Long版は80問目の後に休憩があります。全体をモノクロで構成し、解答中は進捗・再生状態・回答ボタンだけを表示します。クレジット「小室竜也 (Ryuya Komuro)｜東北大学 PD」と原典論文は結果画面だけに掲載します。

回答はブラウザのメモリ内だけで扱い、外部への送信、localStorage/sessionStorageへの保存、ダウンロードを行いません。再読み込み・ページを閉じると消えます。ホスティングサービスの通常のアクセス処理とは区別します。音声エラー時には再試行または中断でき、聞けなかった問題を誤答扱いで先送りしません。未完了時にはCEFRを表示しません。

## 採点・CEFRの範囲

正答1問を1点として、Short版は40点、Long版は160点満点で表示します。練習は得点に含めません。

Short版は元の40問用換算表をそのまま利用します。Long版は160問の総得点と別に、Short版と共通する40問の得点を同じ換算表に当てはめます。40問すべての元音声ファイル名・対象語・正答を照合済みです。160点を40点へ比例換算しません。出題順・疲労条件が異なるため、Short版を単独で受けた場合との同等性は未確認です。

CEFRは既存換算表の参考目安です。公式判定や英語4技能全体の評価ではなく、下記原典が本Web版の換算を直接検証したという意味でもありません。新規の換算妥当性研究や研究用データ収集は本プロジェクトの範囲外です。

## 原典論文

- Uchihara, T., Saito, K., Kurokawa, S., Takizawa, K., & Suzukida, Y. (2025). Declarative and automatized phonological vocabulary knowledge: Recognition, recall, lexicosemantic judgment, and listening-focused employability of second language words. *Language Learning, 75*(2), 458–492. https://doi.org/10.1111/lang.12668
- Saito, K., Uchihara, T., Takizawa, K., & Suzukida, Y. (2025). Individual differences in L2 listening proficiency revisited: Roles of form, meaning, and use aspects of phonological vocabulary knowledge. *Studies in Second Language Acquisition, 47*(1), 26–52. https://doi.org/10.1017/S027226312300044X

出版社で確認した巻号確定後の刊行年を記載しています（オンライン先行公開はそれぞれ2024年、2023年）。Uchihara論文の2026年訂正は所属情報の補足です。

## 構成と出典

`assets/` は両版共通の画面・採点処理。`short/` と `long/` は各版の入口と問題設定、`data/` は既存Short版問題・換算表、`audio/` は音声です。音声のバイト列と問題・正答は原リポジトリのものを維持しています。Short版の制約付き順序、Long版のFisher–Yatesシャッフルを維持しています。

- https://github.com/Ryuya-dot-com/LJT-S — 原データ commit `74a9a1c4c216bc34cc817129ad86bfe20de7ea6a`
- https://github.com/Ryuya-dot-com/LexicoSemanticJudgement — 原データ commit `c8f49c369fc39e439c103a37b9b9e44652a27596`

## 検証と公開

```sh
node --test tests/public.test.js
node tests/browser-smoke.mjs short
node tests/browser-smoke.mjs long
```

ブラウザ検査は隔離した一時Chromeプロファイルを利用。音声イベントを模擬し、4+40 / 4+160問の完走、得点・共通40問の換算、音声失敗時の再試行・中断、早押し・キーリピート・連打、320px/390px幅、結果以外でのクレジット非表示、原典リンクを確認します。音声208本は原リポジトリで全件デコード検査済みで、新配置へのコピー後にバイト一致を確認しています。iPhone/Android実機は未確認です。

GitHub Pagesで `main` ブランチのルートから配信する、ビルド不要の静的サイトです。原リポジトリの公開設定は変更しません。

# Copilot / AI agent instructions — BehaviorCoding (BAS)

このリポジトリはシングルページのクライアントサイド「Behavior Annotation System (BAS)」です。
以下は、このコードベースで即座に生産的に動けるための要点です。

1) 大局観
- 構成: 複数の HTML variants (`bas.html`, `test.html`, `test2.html`, `test3.html`) がルートにあり、各ファイルに CSS + JS がインラインで埋め込まれた単一ファイルアプリです。
- 役割: UI（動画選択・再生・行動定義・タイムライン表示・JSON保存／読み込み・CSV出力）をすべてブラウザ側で完結させる設計です。サーバやビルド工程は想定されていません。

2) 主要ワークフロー（開発者向け速攻コマンド）
- ローカルで動かす: そのままブラウザで `file://` でも動くが、CORSやファイル参照を安定させるために簡易サーバを推奨します。
  例: `python -m http.server 8000` をリポジトリルートで実行し、http://localhost:8000/bas.html を開いて動作確認。
- デバッグ: ブラウザ DevTools の Console と Network を使ってイベント、JSON の読み書きを確認。ソースは HTML 内の <script> にあるため、Elements → script を見るか、Sources タブから編集可能。

3) プロジェクト特有のパターンと命名規約
- i18n: 各 HTML に `const i18n = { jp: {...}, en: {...}}` があり、テキストはこのオブジェクトを経由してセットされています。キー名（例: `btnSaveState`, `timelineEmpty`）を使って文言を追加／変更してください。
- DOM ID の集中利用: 重要な要素は ID で参照されています。よく使う ID の例:
  - `videoFile`, `video`, `playBtn`, `pauseBtn`, `stopBtn`, `speedLabel`, `timeLabel`
  - `timelineContainer`, `addBehaviorBtn`, `behaviorName`, `behaviorKey`
  - `saveStateBtn`, `loadStateInput`, `saveBehaviorsBtn`, `loadBehaviorsInput`, `saveTimelineBtn`, `loadTimelineInput`
  - `downloadCsvBtn`
- 行動キー: UI 側で「キー」は単一文字（maxlength=1）を想定する作りになっています。行動オブジェクトは少なくとも name/key/color を含む想定です（下記データ例参照）。

4) データ形（discoverable・使われているフィールド） — 参考例
  保存／読み込みされる JSON は少なくとも以下のような構造を想定してください（プロジェクト内のメッセージに `behaviors` フィールド参照あり）。

  {
    "behaviors": [
      { "name": "Look", "key": "a", "color": "#ffcc00" }
    ],
    "intervals": [
      { "key": "a", "start": 1.23, "end": 2.34 }
    ]
  }

  - `behaviors` 配列は行動定義（キー・表示名・色）。
  - `intervals`（タイムライン）はキー参照と start/end（秒）を持つことが期待されます。

5) 変更ルール（AI エージェント向け）
- 既存 HTML の DOM 構造・ID を壊さずに修正してください。UI 要素を削る場合は同時にイベントハンドラの更新を行うこと。
- 文言変更は `i18n` オブジェクトの該当キーを編集するだけで OK。
- 新しい機能はまず `bas.html`（または最も安定している方）で PoC を作り、他ファイルに同期してください。

6) テスト／検証のやり方（手早いチェックリスト）
- 動画読み込みが必要: サンプル動画を選んで再生確認。時間表示（`timeLabel`）や再生制御ボタンが動くこと。
- 行動追加: `behaviorName`/`behaviorKey` に入力して `addBehaviorBtn` をクリック → タイムライン行とボタンが生成されること。
- 保存/読込: `saveStateBtn` で JSON をダウンロードし、`loadStateInput` で同ファイルを再読込して復元できること。
- CSV 出力: `downloadCsvBtn` を押してダウンロードされる CSV の中身（タイムスタンプ・キー・行動名など）を確認。

7) 既存ファイル参照（作業の起点）
- UI とロジックは各 HTML ファイルにまとめられています。まず `bas.html` → `test.html` → `test2.html` → `test3.html` の順に目を通してください。

8) 追加情報が必要な場合（問いかけ候補）
- JSON の正式なスキーマ（フィールド名と必須／任意）を教えてください（複数ツールでの互換性のため）。
- 将来的にビルド手順や外部パッケージ導入を考えていますか？（今は純クライアント実装で外部依存はありません）

---
変更を作成しました。足りない箇所（例: 期待する JSON スキーマの細部、テスト用のサンプル動画パスなど）があれば教えてください。追加で反映して更新します。

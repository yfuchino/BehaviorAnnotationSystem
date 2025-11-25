# Behavior Annotation System (BAS)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Language: HTML/CSS/JS](https://img.shields.io/badge/Language-HTML%2FCSS%2FJS-blue.svg)](#)

シングルページのクライアントサイド「Behavior Annotation System (BAS)」は、ブラウザ上で動画を再生しながら行動（behaviors）を定義・記録・編集・保存できる軽量ツールです。外部依存なく、ローカルファイルのみで完結します。

---

**ファイル**
- `bas.html` — メインのシングルファイルアプリ（推奨）

---

**主要機能**
- 動画ファイル読み込み（ローカルファイルを使用）
- 行動定義（名前・キー・色）の追加・編集
- 再生中のキー／ボタンで行動の Start/Stop を記録（区間データ）
- タイムライン表示と区間の視覚化
- 行動一覧のドラッグ＆ドロップ並べ替え
- 状態（behaviors + intervals）の JSON 保存／読み込み
- 行動テンプレート（behaviors のみ）の保存／読み込み
- タイムラインのみの保存／読み込み
- CSV エクスポート（完了した区間のみ）
- 日本語 / English の i18n 切替

---

**素早いセットアップ（PowerShell）**
1. リポジトリルート（`bas.html` があるディレクトリ）に移動します。
2. 簡易サーバを起動してブラウザで開くことを推奨します（ローカルファイルだと一部ブラウザで挙動が異なるため）。

```powershell
# カレントディレクトリをリポジトリルートにして実行
python -m http.server 8000
```

ブラウザで `http://localhost:8000/bas.html` を開いてください。

---

**使い方（ステップバイステップ）**

| 操作 | 手順 |
|------|------|
| **動画を読み込む** | `動画ファイルを選択` ボタンをクリック → ローカル動画ファイルを選択 |
| **行動を追加** | `行動名` と `キー`（1文字）を入力 → `追加` をクリック |
| **記録を開始/終了** | 動画再生中に行動ボタンをクリック or 対応キーを押す（一時停止中は無効） |
| **行動を編集** | 行動一覧の右端 `\|` ボタンをクリック → 名前・キー・色を変更 |
| **行動を並べ替え** | 行動一覧の行をドラッグして上下に移動 |
| **状態を保存** | `保存` ボタン → JSON ファイルをダウンロード（behaviors + intervals） |
| **状態を読み込む** | `読込` ボタン → 保存した JSON を選択 → 同じ動画ファイルを再選択（必要に応じて） |
| **CSV をエクスポート** | `CSV ダウンロード` ボタン → CSV ファイルをダウンロード（完了した区間のみ） |

---

**補足**

---

**保存される JSON の想定スキーマ**
- フル状態（例）

```json
{
  "type": "full_state",
  "version": 1,
  "videoName": "sample.mp4",
  "behaviors": [
    { "name": "Look", "key": "a", "color": "#ffcc00" }
  ],
  "intervals": [
    { "key": "a", "start": 1.23, "end": 2.34, "duration": 1.11 }
  ]
}
```

- 行動テンプレート（behaviors のみ）
```json
{ "type": "behaviors_template", "version":1, "behaviors": [ /* ... */ ] }
```

- タイムラインのみ
```json
{ "type": "timeline_only", "version":1, "videoName": "...", "intervals": [ /* ... */ ] }
```

---

**i18n（翻訳）**
- 言語文字列は `bas.html` 内の `i18n` オブジェクトに定義されています。
- `applyLanguage()` が DOM に反映するので、文言を追加・修正したらそのキーを `applyLanguage()` にも反映してください。

---

**注意／トラブルシューティング**
- ファイル入力は内部で `input.value` をクリアする処理があります。読み込み後に同じファイルを再選択する場合でも `change` イベントが発火するようになっています。
- 保存された状態に含まれる `videoName` は実ファイルを保存しているわけではありません。復元後は同じ動画を手動で選択してください。
- ブラウザのセキュリティやコーデックによっては一部動画が再生できないことがあります。再生できない場合は別のブラウザや動画フォーマット（例: mp4）をお試しください。

---

**開発者向けメモ**
- DOM ID の集中利用（`playBtn`、`loadStateInput`、`addBehaviorBtn` など）が多いため、要素の ID を変更する場合はスクリプト側も更新してください。
- 行動のキーは `maxlength=1` で想定されています。複数文字キーを使う場合は UI とロジックの両方を変更してください。

---

## License / ライセンス

This project is provided under the MIT License. See the `LICENSE` file in the repository root for details.

---

## English Version

# Behavior Annotation System (BAS)


The Behavior Annotation System (BAS) is a lightweight, single-file client-side web app that lets you define, record, edit, and save behaviors while playing a local video in your browser.

---

**Files**
- `bas.html` — Single-file application

---

**Key features**
- Load a local video file and play it in the browser
- Define/edit behaviors (name, key, color)
- Record Start/Stop intervals while the video is playing (keyboard or button)
- Timeline view with visualized intervals
- Drag-and-drop ordering of behavior rows
- Save/load full state (behaviors + intervals) as JSON
- Save/load behavior templates (behaviors only) as JSON
- Save/load timeline-only JSON
- Export completed intervals to CSV
- Japanese / English i18n support

---

**Quick start (PowerShell)**
1. Change into the repository root (where `bas.html` lives).
2. Start a simple HTTP server for more consistent browser behavior:

```powershell
python -m http.server 8000
```

Open `http://localhost:8000/bas.html` in your browser.

---

**Usage (step-by-step)**

| Task | Steps |
|------|-------|
| **Load a video** | Click `Load video` → Select a local video file |
| **Add a behavior** | Enter `Behavior name` and `Key` (1 character) → Click `Add` |
| **Record Start/Stop** | Click the behavior button or press the corresponding key while video is playing (paused video does not record) |
| **Edit a behavior** | Click `\|` button on the behavior row → Edit name/key/color |
| **Reorder behaviors** | Drag behavior rows up and down |
| **Save state** | Click `Save` → Download JSON file (behaviors + intervals) |
| **Load state** | Click `Load` → Select saved JSON → Re-select the same video file if needed |
| **Export to CSV** | Click `CSV Download` → Download CSV file (completed intervals only) |

---

**Notes**
- Full state example (same as Japanese section):

```json
{
  "type": "full_state",
  "version": 1,
  "videoName": "sample.mp4",
  "behaviors": [
    { "name": "Look", "key": "a", "color": "#ffcc00" }
  ],
  "intervals": [
    { "key": "a", "start": 1.23, "end": 2.34, "duration": 1.11 }
  ]
}
```

---

**i18n**
- All UI strings live in the `i18n` object inside `bas.html`.
- Update the object and `applyLanguage()` when you add or change text keys.

---

**Troubleshooting**
- The file inputs are cleared programmatically after reading so selecting the same file again still triggers a `change` event.
- `videoName` included in saved JSON is only metadata — the video file itself is not embedded. Re-select the same video file when restoring state.
- Some videos may not play in all browsers due to codec or security restrictions—try a different browser or a widely supported format such as MP4.

---

**Developer notes**
- The app relies on specific DOM IDs (eg. `playBtn`, `loadStateInput`, `addBehaviorBtn`). If you rename elements, update script references accordingly.
- Behavior keys are assumed to be single characters (`maxlength=1`). Changing that requires UI and logic updates.
- 動画ファイル読み込み（ローカルファイルを使用）
- 行動定義（名前・キー・色）の追加・編集
- 再生中のキー／ボタンで行動の Start/Stop を記録（区間データ）
- タイムライン表示と区間の視覚化
- 行動一覧のドラッグ＆ドロップ並べ替え
- 状態（behaviors + intervals）の JSON 保存／読み込み
- 行動テンプレート（behaviors のみ）の保存／読み込み
- タイムラインのみの保存／読み込み
- CSV エクスポート（完了した区間のみ）
- 日本語 / English の i18n 切替

---

**素早いセットアップ（PowerShell）**
1. リポジトリルート（`bas.html` があるディレクトリ）に移動します。
2. 簡易サーバを起動してブラウザで開くことを推奨します（ローカルファイルだと一部ブラウザで挙動が異なるため）。

```powershell
# カレントディレクトリをリポジトリルートにして実行
python -m http.server 8000
```

ブラウザで `http://localhost:8000/bas.html` を開いてください。

---

**使い方（概要）**
- 動画ファイルを選択: `動画ファイルを選択` ボタンを押してローカル動画を読み込みます。
- 行動を追加: `行動名` と `キー` を入力して `追加` を押すと行動が一覧に追加されます（キーは1文字）。
- 記録開始/終了: 動画を再生中に該当の行動ボタンをクリック、または対応キーを押すと Start/Stop が記録されます（動画が一時停止中だと記録されません）。
- 編集: 行動一覧の右端の `|` ボタンで名前／キー／色を編集できます。
- 並べ替え: 行動一覧の各行をドラッグして上下に並べ替えられます。
- 保存: 「保存」ボタンで JSON をダウンロードします。種類は「状態（behaviors + intervals）」「行動テンプレート（behaviorsのみ）」「タイムラインのみ」で分かれています。
- 読込: `読込` ボタンで保存した JSON を選択して復元します。ロード後は必要に応じて同じ動画ファイルを再選択して使用してください。
- CSV: `CSV ダウンロード` で完了した区間のみを CSV にエクスポートします。

---

**保存される JSON の想定スキーマ**
- フル状態（例）

```json
{
  "type": "full_state",
  "version": 1,
  "videoName": "sample.mp4",
  "behaviors": [
    { "name": "Look", "key": "a", "color": "#ffcc00" }
  ],
  "intervals": [
    { "key": "a", "start": 1.23, "end": 2.34, "duration": 1.11 }
  ]
}
```

- 行動テンプレート（behaviors のみ）
```json
{ "type": "behaviors_template", "version":1, "behaviors": [ /* ... */ ] }
```

- タイムラインのみ
```json
{ "type": "timeline_only", "version":1, "videoName": "...", "intervals": [ /* ... */ ] }
```

---

**i18n（翻訳）**
- 言語文字列は `bas.html` 内の `i18n` オブジェクトに定義されています。
- `applyLanguage()` が DOM に反映するので、文言を追加・修正したらそのキーを `applyLanguage()` にも反映してください。

---

**注意／トラブルシューティング**
- ファイル入力は内部で `input.value` をクリアする処理があります。読み込み後に同じファイルを再選択する場合でも `change` イベントが発火するようになっています。
- 保存された状態に含まれる `videoName` は実ファイルを保存しているわけではありません。復元後は同じ動画を手動で選択してください。
- ブラウザのセキュリティやコーデックによっては一部動画が再生できないことがあります。再生できない場合は別のブラウザや動画フォーマット（例: mp4）をお試しください。

---

**開発者向けメモ**
- DOM ID の集中利用（`playBtn`、`loadStateInput`、`addBehaviorBtn` など）が多いため、要素の ID を変更する場合はスクリプト側も更新してください。
- 行動のキーは `maxlength=1` で想定されています。複数文字キーを使う場合は UI とロジックの両方を変更してください。

---

ライセンス・著作権情報はこのリポジトリに明示されていません。利用に際して社内ポリシーや第三者ライブラリの要件を確認してください。

---

作成しました: `README.md` — 他に含めたいスクリーンショット、GIF、または追加の使用例（例: CSV のカラム説明など）があれば教えてください。
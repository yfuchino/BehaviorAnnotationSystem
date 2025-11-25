# Contributing to Behavior Annotation System (BAS)

このプロジェクトへの貢献ありがとうございます。以下のガイドラインに従ってください。

---

## 貢献の方法

### バグ報告・機能提案
- **Issue を作成**: GitHub の Issues タブから、問題や機能提案を報告してください。
- **詳細な情報**: 再現手順、期待される動作、実際の動作を含めてください。
- **環境情報**: ブラウザ、OS、動画形式などを記載してください。

### コード修正・新機能
1. **Fork**: このリポジトリを Fork します
2. **Branch を作成**: `fix/issue-name` または `feature/feature-name` という命名規則でブランチを作成
3. **編集**: `bas.html` を編集（単一ファイルアプリ）
4. **ローカルテスト**:
   ```powershell
   python -m http.server 8000
   ```
   ブラウザで `http://localhost:8000/bas.html` を開いて検証
5. **Commit**: わかりやすいコミットメッセージを記述
6. **Push**: Fork したリポジトリに Push
7. **Pull Request**: 元のリポジトリに PR を送信

---

## コーディング規約

### JavaScript
- **命名規則**: キャメルケース（例: `behaviorName`、`toggleBehavior`）
- **変数**: DOM 要素は `Element` サフィックスまたは ID 名から派生（例: `playBtn`、`videoFile`）
- **関数**: 動作を説明する名前（例: `addBehavior()`、`updateTimeline()`）
- **コメント**: 複雑なロジックには `/* ... */` ブロックコメント、セクション分けに `// ====== ... ======` を使用

### CSS
- **クラス名**: ケバブケース（例: `.file-controls`、`.timeline-row`）
- **ID**: キャメルケース（例: `#playBtn`、`#timelineContainer`）
- **構成**: セクションごとにコメント区切り（`/* ====== Section Name ====== */`）

### HTML
- **インデント**: 2 スペース
- **ID/Class**: 意味のある名前（ユーティリティのみ例外）
- **属性**: 日本語コメントとセットで説明

---

## 修正・機能追加の例

### テキストの修正（i18n対応）
1. `bas.html` の `i18n` オブジェクトにキーを追加
2. `applyLanguage()` 関数を更新してそのキーを使用
3. 両言語（`jp`、`en`）のテキストを追加

**例:**
```javascript
const i18n = {
  jp: { /* ... */ myNewKey: "新しいテキスト" },
  en: { /* ... */ myNewKey: "New text" }
};

function applyLanguage() {
  // ...
  document.getElementById("myElement").textContent = t("myNewKey");
}
```

### UI 機能の追加
1. HTML の構造を追加（ID/Class を明確に）
2. CSS でスタイリング
3. JavaScript で動作を実装
4. i18n 対応が必要な場合はテキストキーを追加

---

## テスト・検証

修正・追加後、以下の項目を確認してください：

- [ ] ローカルサーバで動作確認（Chrome、Firefox など複数ブラウザ推奨）
- [ ] 動画読み込み・再生が正常に動作
- [ ] 行動の追加・編集・削除が正常に動作
- [ ] JSON 保存・読み込みが正常に動作
- [ ] CSV エクスポートが正常に動作
- [ ] 日本語・英語の言語切替が正常に動作（i18n 対応の場合）
- [ ] コンソールエラーがないこと（DevTools で確認）

---

## ファイル構成

```
bas.html          メインのシングルファイルアプリ
                  - HTML 構造
                  - CSS（<style> タグ内）
                  - JavaScript（<script> タグ内）

README.md         ドキュメント（日本語・英語）
LICENSE           MIT ライセンス
.gitignore        Git 除外ファイル
CONTRIBUTING.md   このファイル
```

---

## 質問・相談

不明な点や大きな変更を計画している場合は、先に Issue で相談してください。

---

## クイックリファレンス

### よくある修正パターン

**テキストを変更する**
1. `i18n` オブジェクトのキーを更新
2. `applyLanguage()` に反映
3. 両言語のテキストを提供

**UI 要素を追加する**
1. HTML に ID/Class を明記
2. CSS でスタイリング
3. JavaScript で動作実装

**バグを修正する**
1. 問題を再現
2. 根本原因を特定
3. ミニマルな修正を適用
4. ブラウザで検証

---

変更ありがとうございました！🎉

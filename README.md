# AIX 請求書オートメーション

広告媒体の請求書を「PDF取込 → AI読取（Gemini対応）→ 部署確認 → 経理照合」まで処理する単一HTMLアプリ。
サーバ不要・`index.html` のみで動作します。データはブラウザ（localStorage）に自動保存されます。

## 公開（GitHub Pages）

1. このリポジトリを GitHub に push
2. リポジトリの **Settings → Pages → Branch: `main` / `(root)`** を選択して Save
3. 数十秒後、`https://<ユーザー名>.github.io/<リポジトリ名>/` で公開されます

## Gemini API の設定

1. 公開ページを開き、**設定 → AI抽出**
2. 接続モード: **Gemini API（キー使用）**
3. APIキー: Google AI Studio（https://aistudio.google.com/apikey）で発行した `AIza…` キー
4. **接続テスト** で疎通確認

### 推奨: キーの保護

Google Cloud コンソールでキーに **HTTPリファラー制限** を設定し、
`https://<ユーザー名>.github.io/*` のみ許可すると、キーが漏れても他所から使えません。

### 注意

- キーは各利用者のブラウザ（localStorage）に保存されます。リポジトリには含まれません。
- 組織で本番運用する場合は、キーをサーバ側に置く「社内API（プロキシ）」モードを推奨します。

## 機能

- 請求書の登録 / 編集 / 削除、CSV取込・書出、JSONバックアップ
- PDF取込: Gemini / Anthropic / 社内APIでAI読取（スキャンPDF可）。未接続時は内蔵推定にフォールバック
- 確認依頼メールの自動生成（mailto・自動送信なし）
- 承認 / 差戻し、経理AI照合（許容差設定）、経理向けCSV書出
- 削減効果の自動計算（件数・分/件・AI代替率・時給を設定可能）

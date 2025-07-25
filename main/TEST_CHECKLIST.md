# Bolcha デプロイ後テストチェックリスト

## 基本機能のテスト

### ログイン・認証
- [ ] Googleアカウントでログインできる
- [ ] ログアウトできる
- [ ] 未認証状態でログイン画面にリダイレクトされる

### ルーム管理
- [ ] ルーム一覧が表示される
- [ ] 新しいルームを作成できる
- [ ] ルーム名の文字数制限が機能する（全角18文字/半角36文字）
- [ ] 重複したルーム名で作成できない
- [ ] ルームを削除できる（管理者権限）

### **新機能：ルーム数制限**
- [ ] 管理者画面でルーム数制限を設定できる
- [ ] ルーム数制限が0の場合、無制限でルームを作成できる
- [ ] ルーム数制限を設定した場合、上限に達するとルーム作成ボタンが無効になる
- [ ] ルーム数制限に達した状態でルーム作成を試行するとエラーメッセージが表示される
- [ ] ルームリスト画面に「ルーム数: X/Y」または「ルーム数: X (制限なし)」が表示される
- [ ] 既存ルーム数が設定値を超えていても自動削除されない

### チャット機能
- [ ] ルームに入室できる
- [ ] メッセージを送信できる
- [ ] リアルタイムでメッセージが表示される
- [ ] 言語切り替えができる
- [ ] 自動翻訳が機能する
- [ ] 返信機能が動作する
- [ ] いいね機能が動作する
- [ ] メッセージ削除ができる（送信者・管理者）

### プロフィール機能
- [ ] プロフィール設定画面にアクセスできる
- [ ] 表示名を変更できる
- [ ] アバター画像を変更できる
- [ ] バブル色・テキスト色を変更できる
- [ ] サイド表示設定を変更できる

### 管理者機能
- [ ] 管理者アカウントで管理画面にアクセスできる
- [ ] ルーム自動削除時間を設定できる
- [ ] プレゼンスカウンター機能を有効/無効にできる
- [ ] **ルーム数制限を設定できる（新機能）**
- [ ] ユーザー管理ができる
- [ ] ルーム削除ができる

### UI/UXのテスト
- [ ] レスポンシブデザインが機能する（モバイル/タブレット/デスクトップ）
- [ ] ルーム名が画面幅に応じて適切に表示される
- [ ] メッセージ入力欄の幅がチャットエリアと同じになっている
- [ ] メッセージ入力欄のサイズが適切
- [ ] 送信ボタンの位置が適切

### パフォーマンステスト
- [ ] ページ読み込み時間が適切
- [ ] リアルタイム更新が遅延なく動作する
- [ ] 大量のメッセージがある場合もスムーズに動作する

### セキュリティテスト
- [ ] 未認証ユーザーがチャットルームにアクセスできない
- [ ] 管理者以外が管理画面にアクセスできない
- [ ] XSSやその他のセキュリティ脆弱性がない

## ブラウザ互換性テスト
- [ ] Chrome（最新版）
- [ ] Firefox（最新版）
- [ ] Safari（最新版）
- [ ] Edge（最新版）
- [ ] モバイルブラウザ（iOS Safari, Android Chrome）

## 重要な新機能のテストシナリオ

### ルーム数制限機能の詳細テスト

1. **制限なしの状態**
   - [ ] 管理者画面でmaxRooms = 0に設定
   - [ ] ルームリスト画面で「ルーム数: X (制限なし)」と表示される
   - [ ] 何個でもルームを作成できる

2. **制限ありの状態（例：maxRooms = 3）**
   - [ ] 管理者画面でmaxRooms = 3に設定
   - [ ] ルームリスト画面で「ルーム数: 2/3」のように表示される
   - [ ] 3個目のルーム作成まで正常に動作する
   - [ ] 4個目のルーム作成時にボタンが無効化される
   - [ ] 4個目のルーム作成を試行するとアラートが表示される

3. **既存ルーム数が制限を超えている場合**
   - [ ] 5個のルームが存在する状態でmaxRooms = 3に設定
   - [ ] 既存の5個のルームが削除されない
   - [ ] 新しいルームは作成できない
   - [ ] ルームリスト画面で「ルーム数: 5/3 (上限に達しています)」と表示される

4. **リアルタイム更新**
   - [ ] 管理者が制限値を変更すると、ルームリスト画面がリアルタイムで更新される
   - [ ] 他のユーザーがルームを作成/削除すると、カウントがリアルタイムで更新される

## 報告すべき問題

- 機能が動作しない
- エラーメッセージが表示される
- パフォーマンスが著しく悪い
- UI表示が崩れている
- セキュリティ上の懸念

## テスト完了時の確認

- [ ] 全ての基本機能が正常に動作する
- [ ] 新機能（ルーム数制限）が期待通りに動作する
- [ ] ユーザーエクスペリエンスが良好
- [ ] セキュリティ設定が適切
- [ ] 本番環境での安定稼働が見込める
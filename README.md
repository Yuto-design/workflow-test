# CI/CD テスト（GitHub Actions）
GitHub Actions を用いて Pull Request 作成時に自動で pytest を実行する CI/CD テストを行っています。

## 概要

- main ブランチ向けの Pull Request をトリガーに実行
- macOS 環境上で Python をセットアップ
- 依存関係をインストール後、pytest を実行
- テスト失敗時のログ出力や、環境変数・Secrets・Step 出力の確認を実施

## 目的
- GitHub Actions による CI/CD パイプラインの動作確認
- pytest を用いた自動テストの導入検証
- 環境変数・Secrets・Step 出力の扱い方の理解

## ワークフロー構成
### トリガー
- pull_request
- 対象ブランチ：main

### 実行環境
|項目|内容|
|----|----|
|OS|*macos-latest*|
|Python|*3.13*|

### 環境変数
|変数名|値|
|----|----|
|*DB_USER*|*postgres*|

## 実行ステップ

**1. リポジトリのチェックアウト**
- actions/checkout@v6

**2. Python のセットアップ**
- actions/setup-python@v5
- Python バージョン：3.13

**3. 依存関係のインストール**
- requirements.txt を使用して pip install

**4. pytest の実行**
- テストコードを自動実行

**5. 失敗時ログの出力**
- pytest などの Step が失敗した場合にメッセージを表示

**6. 環境変数の確認**
- DB_USER の値を出力

**7. GitHub Secrets の確認**
- secrets.API_KEY の値を出力（※ 実際の値はマスクされる）

**8. Step Output の利用例**
- date< コマンドで時刻を取得
- $GITHUB_OUTPUT を用いて次の Step へ出力を受け渡し

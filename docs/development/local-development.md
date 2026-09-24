# Priv.KaleidoStudio ローカル開発環境

## 目的

Priv.KaleidoStudioのローカル開発環境における基本方針と、各環境の責務を定義する。

開発者ごとの環境差異を抑え、別PCやCI環境でも再現可能な開発環境を目指す。

## 開発方針

本プロジェクトでは、Node.jsやPythonなどのアプリケーション実行環境をホストOSへ直接導入せず、原則としてDockerコンテナ内で管理する。

ホストOSには、開発に必要な最小限のツールのみを配置する。

### ホストOS
* Docker実行環境
  * macOS: Docker Desktop / Docker CLI
  * Linux: Docker Engine / Docker Compose
* Git
* GitHub CLI
* Editor

### Dockerコンテナ

* Node.js / npm
* Python
* フロントエンド依存パッケージ
* バックエンド依存パッケージ
* ローカルAWS相当サービス

## 各環境の責務

### Frontend

`apps/web` に配置する。

フロントエンドの実行環境および依存パッケージは、Frontend用コンテナ内で管理する。

Frontend開発環境の詳細は、後続Issueで構築する。

### Backend

`services/api` に配置する。

Python実行環境およびバックエンド依存パッケージは、Backend用コンテナ内で管理する。

Backend開発環境の詳細は、後続Issueで構築する。

### Local AWS

S3およびDynamoDBなど、開発時に必要となるAWSサービス相当の環境はDocker Composeで管理する。

具体的なサービス構成は、Local AWS環境構築Issueで追加する。

### Docker Compose

リポジトリルートの `compose.yaml` で、ローカル開発に必要なコンテナを統合管理する。

現時点では共通基盤のみ定義し、各サービスは対応するIssueで段階的に追加する。

## 環境変数

ローカル環境の実値は `.env` に設定する。

`.env` はGit管理対象外とする。

必要な環境変数および安全に共有可能なサンプル値は `.env.example` で管理する。

```bash
cp .env.example .env
```

パスワード、APIキー、アクセストークンなどの秘密情報の実値は、Git管理対象のファイルへ記載しない。

## 基本原則

* ホストOSへのアプリケーションRuntimeの直接導入を原則として行わない
* Runtimeと依存関係はコンテナ内で管理する
* 環境差異を可能な限りDocker設定としてコード化する
* 必要になっていないサービスや設定を先行して追加しない
* Frontend、Backend、Local AWSの責務を分離する
* 秘密情報をGitへコミットしない

## 現在の対象外

以下は後続Issueで対応する。

* Frontendコンテナの実装
* Backendコンテナの実装
* S3 / DynamoDBのローカル環境
* Amazon Cognitoとの接続
* AWS本番環境
* AWS CDK
* CI/CD

# CLAUDE.md

このファイルは、Claude Code (claude.ai/code) がこのリポジトリのコードを扱う際のガイダンスを提供します。

## 重要な指示

**Claude Codeへ：今後このプロジェクトに関するすべての質問と回答は日本語で行ってください。**

## プロジェクト概要

FreshBuddy（フレッシュバディ）は、食品の賞味期限を管理するWebサービスです。本プロジェクトはPythonで構築されており、現在初期開発段階にあります。

**プロジェクトの目的**: 食品の賞味期限を管理するWebサービス

## 技術スタック

### バックエンド
- **言語**: Python 3.11+
- **Webフレームワーク**: Flask 3.x
- **API**: RESTful API
- **データベース**: PostgreSQL（開発時はSQLite）
- **ORM**: SQLAlchemy
- **認証**: Flask-JWT-Extended
- **タスクキュー**: Celery + Redis

### フロントエンド
- **言語**: TypeScript
- **フレームワーク**: React 18+
- **ビルドツール**: Vite
- **CSSフレームワーク**: Tailwind CSS
- **状態管理**: React Context API / Zustand
- **HTTP通信**: Axios
- **音声認識**: Web Speech API

### アーキテクチャ
- **パターン**: SPA（Single Page Application）
- フロントエンド（React）とバックエンド（Flask）を分離した構成
- REST APIでフロントエンドとバックエンドが通信

## 開発環境のセットアップ

### バックエンド（Flask）

```bash
# プロジェクトルートでバックエンドディレクトリに移動
cd backend

# 仮想環境の作成
python -m venv venv
source venv/bin/activate  # Windowsの場合: venv\Scripts\activate

# 依存関係のインストール
pip install -r requirements.txt

# データベースマイグレーション
flask db upgrade

# 開発サーバー起動
flask run
```

### フロントエンド（React）

```bash
# プロジェクトルートでフロントエンドディレクトリに移動
cd frontend

# 依存関係のインストール
npm install

# 開発サーバー起動
npm run dev
```

### Docker（推奨）

```bash
# すべてのサービスを起動（Flask、React、PostgreSQL、Redis）
docker-compose up
```

## プロジェクト構成

本プロジェクトは、バックエンドとフロントエンドを分離したモノレポ構成を採用します：

```
FreshBuddy/
├── backend/              # Flaskバックエンド
│   ├── app/
│   │   ├── __init__.py
│   │   ├── models/      # データベースモデル
│   │   ├── api/         # APIエンドポイント
│   │   ├── services/    # ビジネスロジック
│   │   └── utils/       # ユーティリティ
│   ├── migrations/      # データベースマイグレーション
│   ├── tests/           # テストコード
│   ├── requirements.txt
│   └── config.py
│
├── frontend/            # Reactフロントエンド
│   ├── src/
│   │   ├── components/  # Reactコンポーネント
│   │   ├── pages/       # ページコンポーネント
│   │   ├── hooks/       # カスタムフック
│   │   ├── services/    # API通信
│   │   ├── types/       # TypeScript型定義
│   │   └── utils/       # ユーティリティ
│   ├── public/
│   ├── package.json
│   └── vite.config.ts
│
├── docs/                # ドキュメント
│   └── requirements.md  # 要件定義書
│
├── .claude/             # Claude Code設定
├── docker-compose.yml   # Docker設定
└── README.md
```

### 主要機能の整理

- **ユーザー認証と管理**: Flask-JWT-Extended
- **食品アイテムのデータモデル**: SQLAlchemy（名前、購入日、賞味期限、カテゴリ）
- **賞味期限通知システム**: Celery定期タスク
- **ユーザーインターフェース**: React + TypeScript
- **データ永続化**: PostgreSQL

## 開発における注意事項

### バックエンド（Flask）
- 本プロジェクトは、複数のパッケージマネージャー（pip、poetry、uv、pdm、pixi）をサポートする包括的なPython用.gitignoreを使用しています
- 環境変数は`.env`ファイルに保存してください（既に.gitignoreに含まれています）
- 本プロジェクトは、リンティング用のRuffを含む最新のPythonツールをサポートしています
- API開発時は、適切なHTTPステータスコードとエラーハンドリングを実装してください
- CORS設定を適切に行い、フロントエンドからのアクセスを許可してください

### フロントエンド（React + TypeScript）
- TypeScriptの型定義を厳格に行い、型安全性を確保してください
- コンポーネントは再利用可能な粒度で設計してください
- Tailwind CSSを活用し、一貫性のあるデザインを実装してください
- アクセシビリティ（a11y）を考慮したUI設計を心がけてください

### セキュリティ
- パスワードは必ずハッシュ化してデータベースに保存
- JWT トークンの有効期限を適切に設定
- CSRF対策、XSS対策を実装
- HTTPS通信を使用（本番環境）

### テスト
- バックエンド: pytest を使用した単体テスト・統合テスト
- フロントエンド: Jest + React Testing Library を使用したコンポーネントテスト

## 参考リンク

- 要件定義書: `docs/requirements.md`
- Flask公式ドキュメント: https://flask.palletsprojects.com/
- React公式ドキュメント: https://react.dev/
- TypeScript公式ドキュメント: https://www.typescriptlang.org/

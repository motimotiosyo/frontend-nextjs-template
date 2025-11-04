# Next.js テンプレート

Rails API + Next.jsのプロジェクトで使い回せる**最小限の環境構築テンプレート**です。

## 概要

このテンプレートは、新しいプロジェクトを始める際にコピー&ペーストですぐに開発を始められるように設計されています。

### 技術スタック

- **Node.js**: 20
- **Next.js**: 15.5.3
- **React**: 19.1.0
- **TypeScript**: 5系
- **スタイリング**: Tailwind CSS v4
- **Docker**: Compose v2形式（compose.yml）
- **ポート**: 3000

### 含まれているパッケージ

**dependencies:**
- `react` 19.1.0
- `react-dom` 19.1.0
- `next` 15.5.3

**devDependencies（開発・コード品質ツール、不要なら削除可能）:**
- `typescript` ^5 - TypeScript本体
- `@types/node` ^20 - Node.jsの型定義
- `@types/react` ^19 - Reactの型定義
- `@types/react-dom` ^19 - React DOMの型定義
- `@tailwindcss/postcss` ^4 - Tailwind CSS用PostCSS
- `tailwindcss` ^4 - Tailwind CSS本体
- `eslint` ^8 - リンター（コード品質チェック）
- `eslint-config-next` 15.5.3 - Next.js用ESLint設定
- `prettier` ^3 - フォーマッター（コード整形）

## 使い方

### 1. このリポジトリをクローン

```bash
git clone <このリポジトリのURL>
cd <リポジトリ名>
```

### 2. Docker環境で起動

```bash
docker compose up
```

初回起動時に自動的に以下が実行されます：
- Dockerイメージのビルド
- npm パッケージのインストール
- Next.js開発サーバー起動

### 3. 動作確認

ブラウザで http://localhost:3000 にアクセス

**疎通確認ページ:**
- 初回アクセス時に表示される「テンプレート疎通確認」ページ
- フロントエンドとバックエンドAPIの接続状態を自動的に確認します
- バックエンドが起動していない場合はエラーが表示されます

### 4. 新しいプロジェクト用にカスタマイズ

**疎通確認ページの置き換え:**
- `src/app/page.tsx` はサンプル実装です
- プロジェクトに合わせて作り直してください
- バックエンドの `/api/v1/health` エンドポイントと連携しています

**必須: メタデータの変更**

`src/app/layout.tsx` のTODOコメントに従って変更：
```typescript
export const metadata: Metadata = {
  title: "App",  // アプリ名に変更
  description: "App",  // アプリの説明に変更
};
```

言語の変更（必要に応じて）：
```typescript
<html lang="ja">  {/* 必要に応じて言語を変更 */}
```

**その他のカスタマイズ:**
- ページの追加（`src/app/` 配下）
- コンポーネントの作成（必要に応じて `src/components/` を作成）
- API連携の実装
- Tailwind CSSのカスタマイズ
- etc...

## 環境変数

開発環境の環境変数は `compose.yml` に記載済みです。
環境変数ファイルのコピーは不要です。

**本番環境では `.env.local` ファイルで管理してください。**

### 環境変数一覧（compose.yml参照）

- `NEXT_PUBLIC_API_BASE_URL`: バックエンドAPI URL（デフォルト: http://localhost:3001/api/v1）

## コンテナの停止

```bash
docker compose down
```

ボリュームも削除する場合：
```bash
docker compose down -v
```

## プロジェクトへの組み込み手順

1. このリポジトリの内容を新しいプロジェクトリポジトリにコピー
2. `docker compose up` で起動確認
3. `src/app/layout.tsx` のメタデータを変更
4. プロジェクト固有の実装を開始

## Tailwind CSSについて

### 最小構成

`tailwind.config.ts` は最小構成になっています：
```typescript
content: [
  "./src/app/**/*.{js,ts,jsx,tsx,mdx}",
],
```

### コンポーネントディレクトリを使う場合

`src/components/` ディレクトリを作成したら、`tailwind.config.ts` に追加してください：
```typescript
content: [
  "./src/app/**/*.{js,ts,jsx,tsx,mdx}",
  "./src/components/**/*.{js,ts,jsx,tsx,mdx}",  // 追加
],
```

## バックエンドとの連携

このテンプレートは Rails API バックエンドとの連携を前提としています。

- API URL は環境変数 `NEXT_PUBLIC_API_BASE_URL` で設定
- デフォルトでは http://localhost:3001/api/v1 に接続

## 注意事項

- Mac/Windows両対応（Docker Desktop必須）
- 開発環境専用の設定です
- 本番環境では適切な環境変数とビルド設定を行ってください

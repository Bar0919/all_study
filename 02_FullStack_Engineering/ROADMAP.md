# `02_FullStack_Engineering` - フルスタックエンジニアリング 詳細ロードマップ

このドキュメントは、モダンでスケーラブル、かつ保守性の高いWebアプリケーションを構築するため、フロントエンド、バックエンド、API設計を深く探求するためのロードマップです。

## 1. `Frontend_Deep` (フロントエンド深掘り)

**目標:** コンポーネントベースのUI構築に習熟し、Webアプリケーションのパフォーマンス最適化、大規模な状態管理、そして最新のWeb技術を扱えるようになる。

### Level 1: モダンフロントエンドの基礎
- **学習内容:**
  - HTML5, CSS3（Flexbox, Grid, カスタムプロパティ）
  - JavaScript (ES6+): `let/const`, アロー関数, Promise, async/await, クラス構文
  - コンポーネントベースのフレームワーク（**React** または **Vue**）の基本
  - パッケージマネージャ（npm/yarn）とビルドツール（Vite/Webpack）の基本操作
- **推奨リソース:**
  - **Web:** MDN Web Docs, The Odin Project, freeCodeCamp
  - **書籍:** 『JavaScript本格入門』
  - **Web:** ReactまたはVueの公式チュートリアル
- **マイルストーン:**
  - Vanilla JS（フレームワークなし）でToDoリストや電卓などの小規模なSPAを作成できる。
  - ReactまたはVueを使い、コンポーネント指向で同じアプリケーションを再構築し、その利点を説明できる。

### Level 2: パフォーマンスと型のある開発
- **学習内容:**
  - **TypeScript**による静的型付け
  - ブラウザのレンダリングパイプライン（Critical Rendering Path）
  - パフォーマンス最適化（Code Splitting, Lazy Loading, メモ化）
  - 大規模状態管理パターン（Redux, Vuex, またはContext APIの高度な利用）
  - テスティング（Jest, React Testing Library）
- **推奨リソース:**
  - **Web:** Googleの[web.dev](https://web.dev/), TypeScript Deep Dive
  - **書籍:** 『プロを目指す人のためのTypeScript入門』、『ハイパフォーマンスブラウザネットワーキング』
- **マイルストーン:**
  - 既存のJavaScriptプロジェクトにTypeScriptを導入し、型安全な開発を実践できる。
  - Chrome DevTools（Lighthouse, Performanceタブ）を使い、自作アプリケーションのパフォーマンスボトルネックを特定し、改善策を施せる。
  - 状態管理ライブラリを使い、認証機能やショッピングカート機能を持つような、より複雑なアプリケーションを構築できる。

### Level 3: 先進技術とアーキテクチャ
- **学習内容:**
  - WebAssembly (Wasm) の概念と、Rust/C++からの利用
  - Web WorkersによるUIをブロックしない並列処理
  - Progressive Web Apps (PWA)によるオフライン対応とネイティブ風体験
  - マイクロフロントエンドの設計思想
- **推奨リソース:**
  - **Web:** [The Rust and WebAssembly Book](https://rustwasm.github.io/book/), MDNのPWA関連ドキュメント
- **マイルストーン:**
  - Rustで書いた簡単な計算処理をWasmにコンパイルし、JavaScriptから呼び出して利用できる。
  - 作成したWebアプリケーションにService Workerを追加し、PWA化（オフラインでも動作、ホーム画面に追加可能）する。

## 2. `Backend_Design` (バックエンド設計)

**目標:** 単純なCRUD APIを超え、保守性・拡張性の高いバックエンドアーキテクチャを設計・実装し、高負荷に耐えるシステムを構築できるようになる。

### Level 1: 基本的なWebサーバーとデータベース連携
- **学習内容:**
  - Webサーバー構築（Node.js with **Express**, or Python with **FastAPI**）
  - REST APIの設計原則
  - ORM（Prisma, SQLAlchemyなど）を用いたデータベース（PostgreSQL, MySQL）連携
  - ユーザー認証（JWTまたはセッションベース）の実装
- **推奨リソース:**
  - **Web:** Express/FastAPIの公式ドキュメント
  - **書籍:** 『Node.jsデザインパターン』
- **マイルストーン:**
  - フロントエンドと連携する、一通りのCRUD操作を持つREST APIを構築できる。
  - データベーススキーマを設計し、ORMを介してデータの永続化ができる。
  - 認証機能を実装し、保護されたエンドポイントを作成できる。

### Level 2: 高度なアーキテクチャと高並行処理言語
- **学習内容:**
  - ドメイン駆動設計（DDD）の基本（エンティティ, 値オブジェクト, 集約, リポジトリ）
  - クリーンアーキテクチャ、ヘキサゴナルアーキテクチャ
  - 高並行処理言語（**Go** または **Rust**）の学習
  - Goのgoroutine/channel、Rustのasync/awaitと所有権モデル
- **推奨リソース:**
  - **書籍:** 『クリーンアーキテクチャ』、『エリック・エヴァンスのドメイン駆動設計』、『Go言語による並行処理』
  - **Web:** A Tour of Go, The Rust Programming Language (The Book)
- **マイルストーン:**
  - 既存のバックエンドアプリケーションを、クリーンアーキテクチャの思想に基づいてレイヤー（ドメイン、ユースケース、インフラ）に分割してリファクタリングできる。
  - GoまたはRustを学び、簡単なWebサーバーやTCPサーバーを構築して、その言語の並行処理モデルの利点を説明できる。

### Level 3: マイクロサービスと分散システム
- **学習内容:**
  - マイクロサービスアーキテクチャの長所と短所
  - サービス間通信（同期: REST/gRPC, 非同期: メッセージキュー）
  - メッセージキュー（RabbitMQ, Kafka）の基本
  - サービスディスカバリ、サーキットブレーカーパターン
- **推奨リソース:**
  - **書籍:** 『マイクロサービスアーキテクチャ』(Sam Newman)、『データ指向アプリケーションデザイン』
- **マイルストーン:**
  - 既存のモノリシックなバックエンドを、関心事に基づいて2〜3のマイクロサービスに分割できる。
  - サービス間の非同期通信を実現するためにメッセージキューを導入できる。

## 3. `API_Standards` (API標準)

**目標:** RESTの成熟度を高め、GraphQLやgRPCといったモダンなAPI技術を適切に選択・設計できるようになる。

### Level 1: RESTful APIの成熟度向上とドキュメンテーション
- **学習内容:**
  - Richardson Maturity Model
  - HATEOAS (Hypermedia as the Engine of Application State)
  - OpenAPI Specification (OAS) を用いたAPIドキュメンテーション
- **推奨リソース:**
  - **Web:** OpenAPI (Swagger) の公式ドキュメント
- **マイルストーン:**
  - 自身が作成したREST APIに対してOAS (swagger.json/yaml) を記述し、Swagger UIやRedocでドキュメントを自動生成できる。

### Level 2: GraphQL
- **学習内容:**
  - GraphQLの基本（Query, Mutation, Subscription）
  - スキーマ定義言語（SDL）
  - N+1問題とその解決策（DataLoaderパターン）
- **推奨リソース:**
  - **Web:** [GraphQL.org](https://graphql.org/), Apollo Server/Clientのドキュメント
- **マイルストーン:**
  - 既存のREST APIの前にGraphQLサーバーを立て、複数のバックエンドサービスを呼び出して単一のエンドポイントでデータを提供するBFF（Backend for Frontend）を構築できる。

### Level 3: gRPCと冪等性設計
- **学習内容:**
  - gRPCのアーキテクチャ（Protocol Buffers, HTTP/2ベース）
  - 4種類のRPC（Unary, Server streaming, Client streaming, Bidirectional streaming）
  - APIの冪等性（Idempotency）設計
- **推奨リソース:**
  - **Web:** gRPCの公式サイト, StripeやGoogleのAPI設計ガイド
- **マイルストーン:**
  - マイクロサービス間の内部通信をRESTからgRPCに置き換える。
  - 決済処理など、冪等性が重要になるAPIエンドポイントを、リクエストIDやトークンを用いて設計・実装できる。

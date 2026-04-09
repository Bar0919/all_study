# `04_Security_Provable` - 実践的セキュリティ 詳細ロードマップ

このドキュメントは、事後対応的なセキュリティから脱却し、攻撃と防御の論理を理解することで、証明可能（provably secure）な堅牢なシステムを構築するためのロードマップです。

## 1. `Application` (アプリケーションセキュリティ)

**目標:** 開発するアプリケーションに脆弱性を生まないためのセキュアコーディング技術と、モダンな認証・認可の仕組みをマスターする。

### Level 1: Web脆弱性の理解と対策
- **学習内容:**
  - **OWASP Top 10** の各脆弱性の原理（SQLインジェクション, XSS, CSRF, IDORなど）
  - セキュアコーディングの基本原則（入力値の検証, 出力のエスケープ, 最小権限の原則）
- **推奨リソース:**
  - **Web:** [OWASP Top 10](https://owasp.org/www-project-top-ten/), [OWASP Juice Shop](https://owasp.org/www-project-juice-shop/)（実践学習用）
  - **書籍:** 『体系的に学ぶ 安全なWebアプリケーションの作り方（徳丸本）』、『Real-World Bug Hunting』
- **マイルストーン:**
  - OWASP Juice Shopなどの脆弱なWebアプリを使い、OWASP Top 10の主要な脆弱性について、実際に攻撃を成功させ、その原理と対策コードを説明できる。
  - 自身のアプリケーションに静的解析（SAST）ツール（SonarQube, Snyk Codeなど）を導入し、検知された脆弱性を修正できる。

### Level 2: 認証・認可の標準
- **学習内容:**
  - 認証（Authentication） vs 認可（Authorization）
  - **OAuth 2.0** の主要なフロー（認可コードフロー, クライアントクレデンシャル フロー）
  - **OpenID Connect (OIDC)** の役割とIDトークン
  - **JWT (JSON Web Token)** の構造（ヘッダー, ペイロード, 署名）と検証方法
- **推奨リソース:**
  - **書籍:** 『OAuth 2.0/OpenID Connect 実践入門』
  - **Web:** RFC 6749 (OAuth 2.0), OIDC公式サイト, [jwt.io](https://jwt.io/)
- **マイルストーン:**
  - Auth0やOktaなどのIdP（Identity Provider）を利用し、自身のアプリケーションにOIDCベースのログイン機能（ソーシャルログインなど）を実装できる。
  - JWTの署名検証を自前で実装し、改ざんされたトークンを正しく拒否できることを確認する。

### Level 3: 高度な防御機構
- **学習内容:**
  - Content Security Policy (CSP)
  - HTTP Strict Transport Security (HSTS), CORS, CSRFトークン
  - APIセキュリティのベストプラクティス（レートリミット, 過度なデータ公開の防止）
- **推奨リソース:**
  - **Web:** MDN Web Docsのセキュリティ関連ページ, OWASP API Security Top 10
- **マイルストーン:**
  - 自身のWebアプリケーションに適切なCSPとHSTSヘッダを設定し、セキュリティ診断ツール（Observatory by Mozillaなど）で高評価を得る。

## 2. `Network_Sec` (ネットワークセキュリティ)

**目標:** 古典的な境界防御モデルから脱却し、ゼロトラストの原則に基づいた最新のネットワークセキュリティを設計・構築できるようになる。

### Level 1: 暗号技術の基礎
- **学習内容:**
  - 共通鍵暗号と公開鍵暗号
  - ハッシュ関数（一方向性、衝突困難性）とデジタル署名
  - **TLS/SSL** ハンドシェイクのシーケンスと証明書の役割
- **推奨リソース:**
  - **書籍:** 『暗号技術入門』（結城浩）
  - **ツール:** OpenSSLコマンドラインツール
- **マイルストーン:**
  - OpenSSLを使い、自己署名証明書の作成、CSR（証明書署名要求）の生成、ファイルのハッシュ値計算、デジタル署名の作成・検証ができる。
  - WiresharkでTLSハンドシェイクをキャプチャし、どのステップで何が行われているかを説明できる。

### Level 2: ネットワーク防御コンポーネント
- **学習内容:**
  - ファイアウォールとセキュリティグループ
  - IDS（侵入検知システム）/ IPS（侵入防止システム）
  - WAF（Web Application Firewall）の役割とシグネチャ
  - VPN（Virtual Private Network）
- **推奨リソース:**
  - **Web:** 各クラウドプロバイダーのWAFやセキュリティグループのドキュメント
- **マイルストーン:**
  - クラウドのWAFを有効にし、SQLインジェクションやXSSを試みるリクエストをブロックするルールを設定できる。

### Level 3: Zero Trustアーキテクチャ
- **学習内容:**
  - "Never trust, always verify" の原則
  - GoogleのBeyondCorpモデル
  - Identity-Aware Proxy (IAP)
  - サービスメッシュによるmTLS（mutual TLS）
- **推奨リソース:**
  - **Web:** NIST SP 800-207 (Zero Trust Architecture), Google CloudのIAPドキュメント, Istio/Linkerdのドキュメント
- **マイルストーン:**
  - サービスメッシュ（Istioなど）を使い、Kubernetesクラスタ内のサービス間通信をデフォルトで全てmTLSで暗号化する。
  - IAP（GCP IAP, Cloudflare Accessなど）を使い、社内アプリケーションへのアクセスをVPNなしで、IDベースの認証・認可で安全に提供する構成を試す。

## 3. `DevSecOps` (開発プロセスへのセキュリティ統合)

**目標:** セキュリティを開発ライフサイクルの最終工程から「シフトレフト」させ、CI/CDパイプラインに自動的に組み込む文化と技術を習得する。

### Level 1: CI/CDへの自動スキャン導入
- **学習内容:**
  - シフトレフトの考え方
  - SAST (静的アプリケーションセキュリティテスト)
  - DAST (動的アプリケーションセキュリティテスト)
  - SCA (ソフトウェア構成分析) - 依存関係の脆弱性スキャン
- **推奨ツール:**
  - Snyk, Trivy, Dependabot (GitHub), SonarQube
- **推奨リソース:**
  - **Web:** OWASP DevSecOps Guideline
- **マイルストーン:**
  - GitHub ActionsなどのCIパイプラインに、SnykやTrivyを組み込む。
  - Dockerイメージのビルド時に脆弱性スキャンを実行し、クリティカルな脆弱性が発見されたらビルドを失敗させる。
  - Dependabotを有効にし、依存ライブラリの脆弱性を自動で検知・修正するPull Requestを作成させる。

### Level 2: Secret管理
- **学習内容:**
  - Secret（APIキー, DBパスワードなど）をコードや設定ファイルに含めない原則
  - Secret管理のベストプラクティス
- **推奨ツール:**
  - HashiCorp Vault, AWS Secrets Manager, GCP Secret Manager, Azure Key Vault
- **推奨リソース:**
  - **Web:** The Twelve-Factor App (III. Config), Vault公式サイト
- **マイルストーン:**
  - `git-secrets`や`gitleaks`を導入し、SecretがGitリポジトリにコミットされるのを防ぐ。
  - VaultやクラウドのSecret管理サービスを使い、アプリケーションが起動時や実行時に動的にSecretを取得する仕組みを構築する。

### Level 3: ポリシー・アズ・コード (Policy as Code)
- **学習内容:**
  - インフラやセキュリティのポリシー（ルール）をコードで記述し、自動で強制するアプローチ
- **推奨ツール:**
  - **Open Policy Agent (OPA)**, Gatekeeper (Kubernetes向け)
- **推奨リソース:**
  - **Web:** OPA公式サイト, Rego (OPAのポリシー言語) のドキュメント
- **マイルストーン:**
  - OPAのポリシー言語`Rego`を学び、簡単なポリシー（例: 「S3バケットはpublic-readを許可しない」）を記述できる。
  - Gatekeeperを使い、Kubernetesクラスタに対して「全てのPodは特定のラベルを持たなければならない」「特権コンテナは許可しない」といったポリシーを強制する。

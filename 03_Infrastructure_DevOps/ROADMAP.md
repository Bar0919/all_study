# `03_Infrastructure_DevOps` - インフラ & DevOps 詳細ロードマップ

このドキュメントは、スケーラブルで信頼性が高く、かつ効率的に運用可能なシステムを、モダンなDevOpsプラクティスを用いて構築・維持するためのロードマップです。

## 1. `IaC` (Infrastructure as Code)

**目標:** インフラのプロビジョニングと構成管理をコード化・自動化し、手作業によるミスをなくし、再現性と一貫性を確保する。

### Level 1: サーバープロビジョニングと構成管理
- **学習内容:**
  - IaCの原則（宣言的 vs 命令的、冪等性）
  - 不変なインフラストラクチャ（Immutable Infrastructure）の概念
  - プロビジョニングツール（**Terraform**）と構成管理ツール（**Ansible**）の役割分担
- **推奨リソース:**
  - **書籍:** 『Terraform: Up & Running』、『Infrastructure as Code』(O'Reilly)
  - **Web:** Terraform, Ansibleの公式ドキュメント
- **マイルストーン:**
  - Terraformを使い、主要クラウド（AWS, GCP, Azureのいずれか）にVPC, Subnet, VMインスタンス, セキュリティグループといった基本的なインフラを構築できる。
  - Ansible Playbookを書き、起動したVMインスタンスにWebサーバー（Nginxなど）をインストール・設定できる。

### Level 2: コンテナオーケストレーション
- **学習内容:**
  - コンテナ技術の基礎（Docker）
  - コンテナオーケストレーションの必要性
  - **Kubernetes** のコアコンセプト（Pod, Service, Deployment, ReplicaSet, Namespace）
  - `kubectl`コマンドの基本操作
  - マニフェストファイル（YAML）の記述方法
- **推奨リソース:**
  - **書籍:** 『Kubernetes: Up & Running』、『入門 Kubernetes』
  - **Web:** Kubernetes公式サイトのチュートリアル, "The Illustrated Children's Guide to Kubernetes"
- **マイルストーン:**
  - アプリケーションのDockerfileを書き、コンテナイメージをビルドできる。
  - ローカルのKubernetes環境（minikube, Docker Desktopなど）で、Deploymentを使ってアプリケーションをデプロイし、Service（NodePort/LoadBalancer）で外部に公開できる。

### Level 3: 高度なIaCパターン
- **学習内容:**
  - Terraformのモジュール化、Workspace、Remote State管理
  - Kubernetesの高度なオブジェクト（StatefulSet, DaemonSet, ConfigMap, Secret）
  - Kubernetes OperatorパターンとCustom Resource Definition (CRD)
  - パッケージ管理（Helm）
- **推奨リソース:**
  - **Web:** Terraform Modules/Workspacesのドキュメント, Operator SDK/Kubebuilderのチュートリアル, Helm公式サイト
- **マイルストーン:**
  - 繰り返し利用するインフラ構成をTerraformモジュールとして切り出せる。
  - Helm Chartを利用して、サードパーティのアプリケーション（Prometheus, Redisなど）をKubernetesクラスタにデプロイできる。
  - （挑戦的）簡単なKubernetes Operatorを自作してみる。

## 2. `Reliability` (信頼性)

**目標:** SRE（Site Reliability Engineering）の原則を学び、システムの信頼性を定量的に計測・改善し、障害に強い文化を醸成する。

### Level 1: モニタリングとアラート
- **学習内容:**
  - モニタリングの4つの黄金律（レイテンシ, トラフィック, エラー, サチュレーション）
  - USEメソッド、REDメソッド
  - モニタリングの3本柱（メトリクス, ログ, トレース）
- **推奨ツール:**
  - **メトリクス:** **Prometheus**
  - **可視化:** **Grafana**
  - **ロギング:** Loki, Elasticsearch (ELK Stack)
  - **アラート:** Alertmanager
- **推奨リソース:**
  - **書籍:** 『入門 監視』、『Site Reliability Engineering (SRE)』
- **マイルストーン:**
  - アプリケーションにクライアントライブラリを導入し、カスタムメトリクス（リクエスト数、エラー率など）をPrometheusに公開できる。
  - Grafanaでダッシュボードを作成し、システムの健康状態を可視化できる。
  - Alertmanagerを設定し、サービスのレイテンシが閾値を超えたらSlackなどに通知が飛ぶように設定できる。

### Level 2: SREプラクティス
- **学習内容:**
  - SLI（Service Level Indicator）、SLO（Service Level Objective）、SLA（Service Level Agreement）の違い
  - エラーバジェットの概念と運用
  - Toil（手作業）の特定と削減
  - ポストモーテム（事後検証）の文化と実践
- **推奨リソース:**
  - **書籍:** 『The Site Reliability Workbook』、『SREの探求』
  - **Web:** Google CloudのSREに関するドキュメント
- **マイルストーン:**
  - 担当するアプリケーションのユーザーにとって重要なSLIと、達成可能なSLOを定義できる。
  - エラーバジェットを計算し、それを基に「機能開発を優先するか」「信頼性向上に注力するか」の意思決定をシミュレーションできる。
  - 軽微な障害対応の経験を基に、非難を目的としないポストモーテムを記述できる。

### Level 3: カオスエンジニアリング
- **学習内容:**
  - カオスエンジニアリングの原則（本番環境での実験、仮説の構築など）
  - 障害注入実験の計画と実行
- **推奨ツール:**
  - Chaos Toolkit, Gremlin, LitmusChaos
- **推奨リソース:**
  - **書籍:** 『カオスエンジニアリング』(O'Reilly)
  - **Web:** [Principles of Chaos Engineering](http://principlesofchaos.org/)
- **マイルストーン:**
  - ステージング環境で、意図的にVMインスタンスの停止、ネットワーク遅延の発生、CPU負荷の上昇などを引き起こす。
  - システムがどのように振る舞うかを観測し、仮説との違いを分析して、システムの弱点を特定・修正する。

## 3. `Cloud_Native` (クラウドネイティブ)

**目標:** 特定のクラウドベンダーにロックインされない、ポータブルでスケーラブルなクラウドネイティブアプリケーションの設計・構築原則を学ぶ。

### Level 1: 主要クラウドサービスの理解
- **学習内容:**
  - IaaS vs PaaS vs SaaS vs FaaS
  - 主要なコアサービス（AWS: EC2, S3, RDS, IAM | GCP: GCE, GCS, Cloud SQL, IAM | Azure: VM, Blob Storage, SQL DB, AAD）
  - 各クラウドのWell-Architected Framework
- **推奨リソース:**
  - **Web:** 各クラウドプロバイダーの公式ドキュメントと入門チュートリアル
- **マイルストーン:**
  - 主要クラウドの無料利用枠を使い、Webアプリケーション（Webサーバー + DB）を手動でデプロイできる。

### Level 2: マネージドサービスとサーバーレス
- **学習内容:**
  - マネージドKubernetes（AWS EKS, GCP GKE, Azure AKS）
  - サーバーレスコンピューティング（AWS Lambda, Google Cloud Functions, Azure Functions）
  - サーバーレスデータベース（AWS DynamoDB, Google Firestore）
- **推奨リソース:**
  - **書籍:** 『サーバーレスアプリケーション開発ガイド』
- **マイルストーン:**
  - 作成したコンテナ化アプリケーションを、マネージドKubernetesクラスタにデプロイする。
  - 簡単なREST APIをLambda/Cloud Functionsで構築し、API Gateway経由で公開する。

### Level 3: クラウドネイティブアーキテクチャ
- **学習内容:**
  - Cloud Native Computing Foundation (CNCF) のエコシステムとTrail Map
  - サービスメッシュ（Istio, Linkerd）
  - イベント駆動アーキテクチャとCloud Events
  - 分散トレーシング（Jaeger, Zipkin）
- **推奨リソース:**
  - **Web:** [CNCF Cloud Native Interactive Landscape](https://landscape.cncf.io/), Istio/Linkerdの公式ドキュメント
- **マイルストーン:**
  - KubernetesクラスタにIstioを導入し、mTLSによるサービス間通信の暗号化、カナリアリリース、分散トレーシングなどを試す。
  - クラウドのイベントソース（例: S3へのファイルアップロード）をトリガーに、サーバーレス関数を実行するイベント駆動の処理を構築する。

---
title: "モック API (Mock API)"
emoji: 📝
type: "tech"
topics: ["MSW"]
published: true
---

:::details API テストにおける API モック

API モックは、API 設計およびテストにおいて重要な要素です。これは、実際の API が利用可能でなくても、システムのさまざまな側面をテストできるように、API の動作をシミュレーションする手法です。開発やテストの段階では、API が未定義であったり、変更が予想されることがあるため、モックが活用されます。このような場合、ソフトウェア開発者やテスターがシステムを分離し、独立して作業できるようになり、テストの入出力をより細かく制御できるようになります。その目的は、API の機能性、信頼性、パフォーマンス、さらにはセキュリティのテストに及びます。そのため、効果的な API モック戦略を理解し、実装することは、API 設計および開発プロセスの効率化に大きく貢献します。

> API mocking is a crucial aspect of API design and testing. It involves simulating the behaviors of real APIs to test various aspects of the system without the need of the real API being readily available. During the stages of development and testing, the API might be undefined or changes in the API can be expected, hence mocking comes into the picture. In such cases, it helps software developers and testers to isolate the system and work independently, enhancing the control over the input and output of the test. The focus here ranges from testing the API for functionality, reliability, performance, to security. Therefore, understanding and implementing effective API mocking strategies can significantly streamline the API design and development process.

(引用: https://roadmap.sh/api-design)

:::

- API が未定義の場合

モック API とは？
モック API（Mock API） とは、本番環境の API を模倣（mock）したものです。本物の API を使わずに、開発・テスト環境で API の動作をエミュレート するために使用します。

API の開発が完了していない場合や、外部 API に依存せずローカルでテストしたい場合に役立ちます。

## なぜモック API が必要なのか？

1. フロントエンドとバックエンドの開発を並行して進めるため
   バックエンドの開発が遅れていても、フロントエンド側で API のレスポンスを想定して開発が可能。

2. 開発・テストの効率を上げるため

- 実際の API にアクセスしなくても、ローカルで素早くテストができる。
- API のレスポンスを自由にカスタマイズできるため、エラーハンドリングのテストがしやすい。

3. 外部 API への依存を減らす

- 実際の API がメンテナンス中・開発中・有料 API で回数制限がある場合でも、自由にテストが可能。

4. テストデータを管理しやすくする

- 実際のデータベースを使わずに、特定の状態（ユーザーが未ログイン、エラー発生時など）をシミュレートできる。

## モック API の種類

モック API には、大きく分けて 3 つのタイプ があります。

1. スタンドアロンのモックサーバー
   例: json-server、GraphQL Faker、Apollo Server Mocks

特徴:
本番 API と同じように動作するが、データはダミー（モックデータ）。
バックエンドの開発が完了していなくても、フロントエンド開発を進められる。
実際の API サーバーとは別に動作する。

メリット:
フロントエンド・バックエンドのチーム間でモック API を共有しやすい。
実際の API のように動作するため、開発の進行がスムーズ。

デメリット:
モックサーバーを別途立ち上げる必要がある。
モック API のメンテナンスが必要になる。

2. クライアントサイドのモック
   例: MSW (Mock Service Worker)

特徴:
ブラウザの fetch() や XMLHttpRequest をインターセプトして、API のレスポンスを変更する。
フロントエンドのテストや開発環境で API をエミュレートできる。

メリット:
フロントエンド開発時に、バックエンドの影響を受けずに開発が進められる。
実際の API を使わず、すべてローカルで完結するため、API の呼び出し回数制限などを気にする必要がない。

デメリット:
本番環境とは異なる挙動になる場合がある。
スタンドアロンのモックサーバーと比べると、バックエンドの開発チームと共有しづらい。

3. API Gateway を利用したモック
   例: AWS API Gateway の Mock Integration、Postman Mock Server

特徴:
クラウド上で API をモック化し、本番環境と同じように API を提供する。
CI/CD パイプラインや E2E テストに組み込みやすい。

メリット:
クラウド環境でモック API を提供できるため、フロントエンド・バックエンドのチーム間で共有しやすい。
実際の API に近い形で動作する。

デメリット:
セットアップに時間がかかる。
AWS などのクラウド環境を利用するため、ローカルで動かすより手間が増える。

## どのモック API を選ぶべきか？

モック API の方法 適した用途 代表的なツール
スタンドアロンのモックサーバー バックエンドが未完成の状態でフロントエンドを開発する json-server, GraphQL Faker, Apollo Server
クライアントサイドのモック フロントエンドの開発・テストを効率化する MSW (Mock Service Worker)
API Gateway のモック クラウド環境でのテスト・チーム間の共有 AWS API Gateway, Postman Mock Server

バックエンド側でもモック API が必要 なら、Apollo Server + Mocks や GraphQL Faker を追加するのもあり。

## まとめ

モック API は、本番 API の代わりにテストや開発用の API を提供するもの。
主な目的は「フロントエンドとバックエンドの開発を並行して進める」「外部 API への依存を減らす」「開発・テストの効率化」
モック API の種類は「スタンドアロンのモックサーバー」「クライアントサイドのモック」「API Gateway のモック」がある
バックエンド側のモック API が必要なら Apollo Server や GraphQL Faker を併用するのが良い

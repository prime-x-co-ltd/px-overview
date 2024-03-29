# Development

-   開発ルールの「基本」とします
-   ブランチの運用やコーディングルールについて

    -   プロジェクトの性格、使用するフレームワークなどに応じてカスタマイズして使用してください
    -   コーディングルールに関しては最低限 1 リポジトリ（1 プロジェクト）内で統一してください

---

- [Development](#development)
  - [ドキュメント](#ドキュメント)
  - [技術の選定](#技術の選定)
    - [現在](#現在)
    - [新技術の取り入れ](#新技術の取り入れ)
  - [開発フロー](#開発フロー)
    - [全体](#全体)
    - [各流れ](#各流れ)
      - [新規に開発したい](#新規に開発したい)
      - [追加機能をつけたい](#追加機能をつけたい)
      - [Help を求める](#help-を求める)
      - [バグを発見した](#バグを発見した)
  - [コーディングルール](#コーディングルール)

---

## ドキュメント

-   README.md に記載する事項として。Markdown で記載しましょう。
-   例を記載しておきます。プロジェクトの規模や内容によってカスタマイズしてください

```markdown
# リポジトリ名

-   アプリの概要

## 要件

-   レコード保存するときにマスタにデータを保存する
-   ...

## 環境

-   TypeScript
-   webpack
-   ...

## 構成図

あれば

## 備考

-   関連するリンクなど
```

## 技術の選定

### 現在

以下を使用します。

-   言語
    -   TypeScript, JavaScript
    -   Python
    -   PHP（一部）
-   フレームワーク
    -   React, Next.js
    -   Vue, Nuxt.js（一部）
    -   ServerlessFramework, SAM
    -   CakePHP（一部）
-   ビルドツール etc
    -   webpack
    -   Vite（試用）
-   クラウド
    -   AWS
    -   GCP

### 新技術の取り入れ

-   言語/フレームワーク/ビルドツール
    -   現状は特に縛らず、プロジェクトに応じて柔軟に取り入れたいと思います
    -   ただし、命名やリソースの作成粒度などは既存のルールに合わせるようにしてください
    -   取り入れる場合は、みんなで集まる MTG などで、技術の違いや選定理由などを共有できたらいいなと思います
    -   具体的な方法については思案中...（何か取り入れるときにやってみる）
-   AWS
    -   新しいリソースを開発に取り入れたい場合は、情報システムチームに一報します
    -   別途存在する「管理方針」に定められている事項（命名、運用などのルール）を定め、情報システムチームと連携します

## 開発フロー

### 全体

-   ソースコードを管理したい単位にてリポジトリを作成する
    -   リポジトリの単位について [Repository.md を参照](./overview/repository.md)
-   ソースコードに関する課題管理を Issue で行う
    -   要件資料がある場合は Issue にリンクを貼る
    -   ※Issue に記載する事項は下記を参考にしてください
        -   [Issue テンプレート](./.github/ISSUE_TEMPLATE/)
-   レビューを PullRequest（PR） ベースで行う
    -   チーム内外で 1 名以上指定する
    -   ※PullRequest に記載する事項は下記を参考にしてください
        -   [PullRequest テンプレート](./.github/pull_request_template.md)
    -   仕様理解（どの処理でどのようなことを行なっているか）を重視する
-   コミット時のコメントには 関連 Issue の番号を `#number` にて含める

-   ブランチの運用
    -   `main` ブランチには、**現在本番環境に適用しているソースコードをおく**
    -   `main` ブランチには直接 push せず、`dev` からマージする
    -   開発作業は `dev` ブランチ、または `dev` 派生のブランチで行う
        -   `feat/**` :機能追加
        -   `fix/**` :機能修正
        -   名前の付け方 i.g. `feat/issue5` など issue 番号で良いかも??やってみよう..!
    -   `dev -> main` のマージには、PullRequest を使用する
    -   緊急修正の場合は、`main` ブランチから `hotfix/**` ブランチを切り、`dev`, `main` にマージする

**※Issue,PullRequest のテンプレートについて**

-   [本リポジトリの .github 以下](./.github/) をリポジトリのルートディレクトリに取り込むことにより、適用することが可能です
-   複数人で開発する場合は適用してください。メンバー同士の意思疎通、要件整理が楽になります
-   テンプレートの修正要望については本リポジトリ（px-overview）に対し、Issue でご意見をください

---

### 各流れ

ブランチ、Issue、PullRequest の使い方について

#### 新規に開発したい

1. Repository 作成
2. branch `dev` 作成
3. 要件：README に記載
4. 要件：Issue 作成、開発要件記載
5. 開発：Issue のチェックリストをもとに branch `dev` で開発を実施
6. レビュー：PullRequest 作成
7. レビュー：レビュワー確認
8. branch `main` にマージ、Issue Close
9. branch `main` deploy

#### 追加機能をつけたい

1. branch `dev` より、branch `feat/XX` 作成
2. 要件：Issue 作成、追加要件記載
3. 開発：Issue のチェックリストをもとに branch `dev` で開発を実施開発
4. レビュー：PullRequest 作成
5. レビュー：レビュワー確認
6. branch `dev` にマージ、Issue Close
7. branch `main` を deploy

#### Help を求める

1. Issue 作成、Help 内容を記載、Assignee 指定
2. Assignee 確認対応
3. Help 完了後、Issue Close

#### バグを発見した

1. Issue 作成、Help 内容を記載、Assignee 指定
2. Assignee 確認対応、チェックリスト作成
3. （必要に応じて Assignee は変更）
4. branch `dev` より `fix/XX` 作成
5. 修正：Issue のチェックリストをもとに修正
6. レビュー：PullRequest 作成
7. レビュー：レビュワー確認
8. branch `dev` にマージ、Issue Close
9. branch `main` を deploy

---

## コーディングルール

[こちらに記載します](./overview/dev-coding.md)

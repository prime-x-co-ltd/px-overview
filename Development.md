# Development

-   リポジトリにおける開発ルールの「原則」
-   コーディングルールに関しては最低限 1 リポジトリ（1 プロジェクト）内で統一する

## 開発の流れ

-   ソースコードを管理したい単位にてリポジトリを作成する
    -   リポジトリの単位について [Repository.md を参照](./Repository.md)
-   ソースコードに関する課題管理を Issue で行う
    -   要件資料がある場合は Issue にリンクを貼る
    -   Issue に記載する事項は下記を参考にしてください※
        -   [Issue テンプレート](./.github/ISSUE_TEMPLATE/)
-   レビューを PullRequest（PR） ベースで行う

    -   チーム内外で 1 名以上指定する
    -   PullRequest に記載する事項は下記を参考にしてください※
        -   [PullRequest テンプレート](./.github/pull_request_template.md)
    -   仕様理解（どの処理でどのようなことを行なっているか）を重視する

### ※Issue、PullRequest テンプレートについて

-   [本リポジトリの .github 以下](./.github/) をリポジトリのルートディレクトリに取り込むことにより、適用することが可能です
-   複数人で開発する場合は適用してください。メンバー同士の意思疎通、要件の整理が楽になります
-   テンプレートの修正要望については本リポジトリ（px-overview）に対し、Issue でご意見をください

### 各流れ

#### 新規開発

1. Repository 作成
2. branch `dev` 作成
3. default branch を `dev` に設定
4. 要件：README に記載
5. 要件：Issue 作成、対応内容を記載
6. 開発：Issue のチェックリストをもとに開発
7. レビュー：PullRequest 作成
8. レビュー：レビュワー確認
9. branch `dev` で開発を実施
10. branch `main` にマージ、Issue Close
11. branch `main` deploy

#### 追加機能をつけたい

1. branch `dev` より、branch `feat-XX` 作成
2. 要件：Issue 作成、対応内容を記載
3. 開発：Issue のチェックリストをもとに開発
4. レビュー：PullRequest 作成
5. レビュー：レビュワー確認
6. branch `dev` にマージ、Issue Close
7. branch `main` を deploy

#### 途中で Help したい

1. Issue 作成、Help 内容を記載、Assignee 指定
2. Assignee 確認対応
3. Help 完了後、Issue Close

#### バグを発見した

1. Issue 作成、Help 内容を記載、Assignee 指定
2. Assignee 確認対応、チェックリスト作成
3. （必要に応じて Assignee は変更）
4. branch `dev` より `fix-XX` 作成
5. 修正：Issue のチェックリストをもとに修正
6. レビュー：PullRequest 作成
7. レビュー：レビュワー確認
8. branch `dev` にマージ、Issue Close
9. branch `main` を deploy

###

## コーディングルール

-   別ファイル

###

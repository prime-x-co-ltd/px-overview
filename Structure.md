# px-overview 構成..案

-   Github 運用ルール
-   開発ルール？？？　＝運用ルールに含むか..それ以外のものも入るなら Github と分ける
-   コーディングルール

## 運用ルール

-   管理対象

    -   社内向け業務システム
    -   社内向け制作物
    -   社外向け制作物
    -   検証

-   利用者
    -   管理対象のソースを扱う社員
    -   （現状 DM 部/デザイン部のうち一部の社員）

### リポジトリ

-   Repository
-   Description
-   Type
-   Branch
    -   ブランチの運用方法は検討中
-   Issue
    -   `[Feat]` : 新規機能追加
    -   `[Bug]` :不具合対応
    -   `[Help]` :ヘルプ対応
-   PullRequest
    -   レビュー
    -   マージリクエスト
-   Wiki

### Team

### 禁止事項

-   Project の使用
    -   プロジェクト管理ドキュメント及び Backlog にて課題管理を行う
    -

## 開発フロー

### フロー

#### 新規

1. Repository 作成
2. branch `dev` 作成
3. default branch を `dev` に設定
4. 要件：README に記載
5. 要件：Issue 作成、対応内容を記載
6. 開発：Issue のチェックリストをもとに開発
7. レビュー：PullRequest 作成
8. レビュー：レビュワー確認
9. branch `main` にマージ、Issue Close
10. branch `main` deploy

#### 追加機能をつけたい

1. branch `dev` より、 `feat-XX` 作成
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

### ブランチ運用

-   作業時
-   プルリク（レビュー）
-   マージ

###

###

## コーディングルール

-   別ファイル

###

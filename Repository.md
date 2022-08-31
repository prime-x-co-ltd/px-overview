# リポジトリ

## 共通

-   検証用リポジトリは、接頭に `dev-` をつける
-   クライアント向けのリポジトリは、接頭に `{project code}-` をつける

## 業務システム

| systemName | clientName / segment | appId / function / project | description | i.g.                       |
| :--------- | :------------------- | :------------------------- | :---------- | :------------------------- |
| kintone    | app                  | 1207                       |             | kintone-app-1207           |
|            | plugin               | multisearch                |             | kintone-plugin-multisearch |
|            | portal               | top                        |             | kintone-portal-top         |
|            | app                  | template                   |             | kintone-app-template       |
|            | plugin               | template                   |             | kintone-plugin-template    |
| formbridge | form                 |                            |             | formbridge-form            |
|            | mypage               |                            |             | formbridge-mypage          |
| aws        | common               | modules                    |             | aws-common-modules         |
| gas        | kintone              | getfields                  |             | gas-kintone-getfields      |
| slack      | tw                   | timeline                   | delete      | slack-tw-timeline-delete   |
|            | portal               | top                        | template    |                            |

## アプリケーション（業務システム以外）

| applicationName | clientName / segment | appId / function / project | description | i.g.         |
| :-------------- | :------------------- | :------------------------- | :---------- | :----------- |
| primeXXX        |                      |                            |             | primeXXX     |
| primeXXX        | api                  |                            |             | primeXXX-api |

## ドキュメント

| systemName | clientName / segment | appId / function / project | description | i.g.        |
| :--------- | :------------------- | :------------------------- | :---------- | :---------- |
| px         | overview             |                            |             | px-overview |
|            | blog                 |                            |             | px-blog     |

# 今あるリポジトリ（メモベース）

-   kintone

    -   app 1 アプリ
    -   plugin 1 プラグイン

-   formbridge

    -   1 クライアント

-   slack

    -   1 やりたいこと

-   shell

    -   1 やりたいこと

-   アプリケーション

    -   prime-stream Frontend
    -   api-prime-stream API

    -   aws-aop-portal EC2 の中にいる子たち
    -   google-sheets-api

-   テンプレート

    -   １テンプレート

-   GAS

    -   1 ファイル

-   その他

    -   px-blog ドキュメントまとめ
    -   px-ide ドキュメントまとめ
    -   px-dev 検証系
    -   sql-learning 学習系

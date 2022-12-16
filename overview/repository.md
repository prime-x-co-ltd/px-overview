# リポジトリ

## 共通

-   検証用リポジトリは、接頭に `dev-` をつける
-   クライアント向けのリポジトリは、接頭に `{project code}-` をつける

## 業務システム

| systemName | clientName / segment | appId / function / project | description | i.g.                     |
| :--------- | :------------------- | :------------------------- | :---------- | :----------------------- |
| kintone    | app                  | 777                        |             | kintone-app-777          |
|            | plugin               | search                     |             | kintone-plugin-search    |
|            | portal               | top                        |             | kintone-portal-top       |
|            | app                  | template                   |             | kintone-app-template     |
|            | plugin               | template                   |             | kintone-plugin-template  |
| formbridge | form                 |                            |             | formbridge-form          |
|            | mypage               |                            |             | formbridge-mypage        |
| aws        | common               | modules                    |             | aws-common-modules       |
| gas        | kintone              | getfields                  |             | gas-kintone-getfields    |
| slack      | tw                   | timeline                   | delete      | slack-tw-timeline-delete |
|            | portal               | top                        | template    |                          |

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

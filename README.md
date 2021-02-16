# px-overview
運用ルールや総合的なドキュメント管理



## 運用ルール

- リポジトリ

  - 命名ルール

    - 構文

      ```javascript
      systemName-[ clientName | division ]-[ appId | appName ]-[ description ]
      ```
      - systemNameーシステム名（kintone, awsなど）
      - clinetNameークライアント名の略称（mjr, nccなど）
      - divisionー部署名の略称（ap, boなど）
      - appId/appNameーアプリID、アプリ名などを略して記載
      - descriptionーその他補足（任意）

    - 全角禁止

    - ケバブケース*で記載する　　*-(ハイフン)で単語をつなぐ

  - Description

    - 作成時にリポジトリの概要を記載する（日本語可）

  - README.md

    - システム構成、スクリプト構成、大まかな制御フローなどソフトウェア申請準拠レベルの内容を記載する
    - 別途ドキュメントに記載する場合はリンクを貼る（ドキュメント管理は後述）

- 運用フロー

  - 作業時はブランチを切る。ブランチ名は作業内容が分かるように記載する

    　ex) test-IconButton-bugFix

  - 作業が終わったらレビューを経てmasterブランチにマージする
  
- リポジトリ名の変更

  - Gitサーバ側

    ```bash
    Settings > Repository name > Rename
    ```

  - ローカルサーバ側

    ```bash
    vim .git/config #ローカルリポジトリ内で叩く
    ```

    ```bash
    [remote "origin"]
            url = git@github:px-develop/kintone-dm-1405.git #urlを変更
    ```

    



## ディレクトリ構造

```
.
├── README.md
├── dist
│   └── customize.js
├── package-lock.json
├── package.json
├── src
│   ├── css
│   └── js
└── webpack.config.js
```





## ドキュメント管理

- docsディレクトリ配下に格納する

- JSDoc3（参考）

  ```bash
  npm install -g jsdoc
  ```

  - 設定ファイル | conf.json

    ```javascript
    {
        "source": {
          "include": ["./src/js"],
          "excludePattern": "(^|\\/)node_modules\\/"
        },
        "opts": {
          "destination": "./docs/"
        }
    }
    ```

  - ドキュメント作成

    ```bash
    jsdoc -c ./conf.json src
    ```

  - GitHub Pagesで/docsのみ公開する




## 共通モジュール

- Git submoduleを使います

  <a href="https://github.com/px-develop/kintone_common_modules">kintone共通モジュール</a>

  <a href="https://github.com/prime-x-co-ltd/aws-common-modules">aws共通モジュール</a>

- サブモジュールの追加

  ```bash
  git submodule add git@github.com:px-develop/kintone_common_modules [submoduleName]
  ```

- 詳細 | 複雑なので以下を参考にしてください。

  <a href="https://qiita.com/kinpira/items/3309eb2e5a9a422199e9">submoduleと仲良くなる</a>



## kintone

- カスタマイズ画面にリポジトリのURLを設定する



## AWS

px-appサーバ or px-batchサーバにツールを作成した場合は、gitディレクトリ直下にあるaws-common-modulesのモジュールをツールに適用する(ツールの処理成功/失敗ログをRDSに格納し、監視ダッシュボード上に反映するため)。※

※PHP,TypeScript,Python以外の言語でツールを作成した場合は、そのときにツール使用言語でモジュールを作成する。

＜AWSモジュール適用＞

ツール使用言語に応じて以下のコードを追記する。

```bash
#PHPの場合

require_once [aws-common-modules/src/php/aws.phpのパス];

#処理成功時に以下を追記
putLogEvents([
    'iam' => [
        'access_key_id' => [AWSアクセスキーID(文字列)],
        'secret_access_key': [AWSシークレットアクセスキー(文字列)]
    ],
    'cwl' => [
        'root_dir' => [ツールのルートディレクトリ名(文字列)],
        'system_status' => 'Success'
    ]
    # SNS通知する場合は以下も追記
    ,'sns' => [
        'topic_arn' => [SNSトピックのARN(文字列)],
        'subject' => [メール件名(文字列)],
        'message' => [メール本文(文字列)]
    ]
]);

#処理失敗時に以下を追記
putLogEvents([
    'iam' => [
        'access_key_id' => [AWSアクセスキーID(文字列)],
        'secret_access_key': [AWSシークレットアクセスキー(文字列)]
    ],
    'cwl' => [
        'root_dir' => [ツールのルートディレクトリ名(文字列)],
        'system_status' => 'Error',
        'error_title' => [エラー内容(文字列)]
    ]
    # SNS通知する場合は以下も追記
    ,'sns' => [
        'topic_arn' => [SNSトピックのARN(文字列)],
        'subject' => [メール件名(文字列)],
        'message' => [メール本文(文字列)]
    ]
]);
```

```bash
#TypeScriptの場合

import {putLogEvents} from [aws-common-modules/src/js/aws.tsのパス]

#処理成功時に以下を追記
putLogEvents({
    iam: {
        accessKeyId: [AWSアクセスキーID(文字列)],
        secretAccessKey: [AWSシークレットアクセスキー(文字列)]
    },
    cwl: {
        systemStatus: 'Success'
    }
    # SNS通知する場合は以下も追記
    ,sns: {
        topicArn: [SNSトピックのARN(文字列)],
        subject: [メール件名(文字列)],
        message: [メール本文(文字列)]
    }
})

#処理失敗時に以下を追記
putLogEvents({
    iam: {
        accessKeyId: [AWSアクセスキーID(文字列)],
        secretAccessKey: [AWSシークレットアクセスキー(文字列)]
    },
    cwl: {
        systemStatus: 'Error',
        errorTitle: [エラー内容(文字列)]
    }
    # SNS通知する場合は以下も追記
    ,sns: {
        topicArn: [SNSトピックのARN(文字列)],
        subject: [メール件名(文字列)],
        message: [メール本文(文字列)]
    }
})  
```

```bash
#Pythonの場合

import sys
sys.path.append("/home/ec2-user/git/aws-common-modules/src/py")
from AWS import AWS

# 処理成功時に以下を追記
AWS({
    "iam": {
        "accessKeyId": [AWSアクセスキーID(文字列)],
        "secretAccessKey": [AWSシークレットアクセスキー(文字列)]
    },
    "cwl": {
        "rootDir": [ツールのルートディレクトリ名(文字列)],
        "systemStatus": "Success"
    },
    # SNS通知する場合は以下も追記
    ,"sns": {
        "topicArn": [SNSトピックのARN(文字列)],
        "subject": [メール件名(文字列)],
        "message": [メール本文(文字列)]
    }
}).putLogEvents()

#処理失敗時に以下を追記
AWS({
    "iam": {
        "accessKeyId": [AWSアクセスキーID(文字列)],
        "secretAccessKey": [AWSシークレットアクセスキー(文字列)]
    },
    "cwl": {
        "rootDir": [ツールのルートディレクトリ名(文字列)],
        "systemStatus": "Error",
        "errorTitle": [エラー内容(文字列)]
    },
    # SNS通知する場合は以下も追記
    ,"sns": {
        "topicArn": [SNSトピックのARN(文字列)],
        "subject": [メール件名(文字列)],
        "message": [メール本文(文字列)]
    }
}).putLogEvents()
```



## レビュー概念図

```sequence
作業者->確認者: レビュー依頼(Issue)
確認者-->作業者: 修正依頼
Note left of 作業者: リポジトリ作成\n実装
Note right of 確認者: ブランチ作成\nkintone更新
確認者->作業者: マージ依頼(Pull request)
作業者->確認者: kintone更新依頼
```


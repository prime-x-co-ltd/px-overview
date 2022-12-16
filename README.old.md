# px-overview

運用ルールや総合的なドキュメント管理

## 運用ルール

-   リポジトリ

    -   RepositoryName

        -   構文（旧）

            ```javascript
            systemName - [clientName | division] - [appId | appName] - [description]
            ```

            -   systemName ーシステム名（kintone, aws など）
            -   clinetName ークライアント名の略称（mjr, ncc など）
            -   division ー部署名の略称（ap, bo など）
            -   appId/appName ーアプリ ID、アプリ名などを略して記載
            -   description ーその他補足（任意）

        -   構文（新案）

            ```
            [systemName | applicationName ] - [clientName | segment ] - [appId | function | project ] - [description]
            ```

            -   systemName - 業務システム名（kintone, aws, slack, gas など）
            -   applicationName - アプリケーション名（業務システム以外）
            -   clinetName - クライアント名の略称
            -   segment - セグメントの略称（kintone:app, plugin, slack:tw など）\* gas:関連するシステム kintone や ss など
            -   appId/function/project - アプリ ID、機能名/プラグイン名、プロジェクト名などを略して記載
            -   description - その他補足（任意）

        -   全角禁止

        -   ケバブケース*で記載する　　*-(ハイフン)で単語をつなぐ

    -   Description

        -   作成時にリポジトリの概要を記載する（日本語可）
        -   構文

            ```
            [ systemCategory※ ] [ appName ] [ description ] [ ※運用終了年月(YYYY/MM/DD) ]
            ```

            -   systemCategory - システムカテゴリ。従業員管理、案件管理、情報システム、etc
            -   appName - アプリ名。プロジェクト管理、企業マスタ、etc
            -   description - アプリの概要
            -   運用終了年月 - 運用終了時に記載する。理由がある場合は理由を添える　 i.g 代替システム ◯◯ 運用開始のため

    -   README.md

        -   システム構成、スクリプト構成、大まかな制御フローなどソフトウェア申請準拠レベルの内容を記載する
        -   別途ドキュメントに記載する場合はリンクを貼る（ドキュメント管理は後述）

    -   Type
        -   社内アプリケーション
            -   リポジトリ作成時に `Private` を選択する
            -   運用終了時に `Archived`* にする `*リポジトリ Settings > Danger Zone > Archive`
        -   社外アプリケーション
            -   ＃＃

-   運用フロー

    -   作業時はブランチを切る。ブランチ名は作業内容が分かるように記載する

        ex) test-IconButton-bugFix

    -   作業が終わったらレビューを経て main ブランチにマージする

-   リポジトリ名の変更

    -   Git サーバ側

        ```bash
        Settings > Repository name > Rename
        ```

    -   ローカルサーバ側

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

-   ※１アプリケーション内のディレクトリ構造
-   ※適用アプリケーションによって変動あり

## ドキュメント管理 ※検討中..

### TypeDoc を検討中..（設定ファイル見直し中..）

-   docs ディレクトリ配下に格納する

### JSDoc3（参考）

-   docs ディレクトリ配下に格納する

```bash
npm install -g jsdoc
```

-   設定ファイル | conf.json

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

-   ドキュメント作成

    ```bash
    jsdoc -c ./conf.json src
    ```

-   GitHub Pages で/docs のみ公開する

### dependency-cruiser

-   ルールに則って依存関係をバリデーション・描画する
    https://www.npmjs.com/package/dependency-cruiser

-   設定ファイル | .dependency-cruiser.js

    ```zsh
    $ npx depcruise --init

    ? Where do your source files live? src
    ? Do your test files live in a separate folder? No
    ? Looks like you're using TypeScript. Use a 'tsconfig.json'? Yes
    ? Full path to your 'tsconfig.json': tsconfig.json
    ? Also regard TypeScript dependencies that exist only before compilation? Yes
    ? Looks like you're using webpack - specify a webpack config? Yes
    ? Full path to your webpack config: webpack.config.js

    ```

-   依存関係図 | hoge.svg

    ```zsh
    $ npx depcruise -T dot -x node_modules src/js/index.ts | dot -T svg > docs/hoge.svg
    ```

-   コマンド
    -   `depcruise {オプション} {エントリーファイル}`
        -   `-T`|`--output-type`：specify the output format
        -   `-x`|`--exclude`：exclude dependencies from being cruised
    -   `dot`
        -   `-T`：output format

## 共通モジュール

-   Git submodule を使います

    <a href="https://github.com/px-develop/kintone_common_modules">kintone 共通モジュール</a>※今後アップデート予定（多分）

    <a href="https://github.com/prime-x-co-ltd/aws-common-modules">aws 共通モジュール</a>

-   サブモジュールの追加

    ```bash
    git submodule add git@github.com:px-develop/kintone_common_modules [submoduleName]
    ```

-   詳細 | 複雑なので以下を参考にしてください。

    <a href="https://qiita.com/kinpira/items/3309eb2e5a9a422199e9">submodule と仲良くなる</a>

## kintone

-   カスタマイズ画面にリポジトリの URL を設定する

### customize-uploader

-   指定の kintone アプリに JS/CSS ファイルを上書きアップロードする

-   設定ファイル ① | dest/customize-manifest.json

    ```zsh
    #設定ファイルの作成
    $ npx kintone-customize-uploader init

    ? アプリIDを入力してください: 2206
    ? カスタマイズの適用範囲を選択してください: ALL
    dest/customize-manifest.json を生成しました
    ```

    ```json:/dest/customize-manifest.json

    {
        "app": "2206",
        "scope": "ALL",
        "desktop": {
            "js": ["./dist/customize.js"], //ルートからの相対パスで読み込みファイルを指定
            "css": []
        },
        "mobile": {
            "js": [],
            "css": []
        }
    }

    ```

-   設定ファイル ② | package.json

    ```json:package.json
    {
      "scripts": {
        "upload": "kintone-customize-uploader --base-url https://{DOMAIN}.cybozu.com ./dest/customize-manifest.json --watch",
      }
    }

    ```

### customize-plugin-uploader

## AWS

px-app サーバ or px-batch サーバにツールを作成した場合は、git ディレクトリ直下にある aws-common-modules のモジュールをツールに適用する(ツールの処理成功/失敗ログを RDS に格納し、監視ダッシュボード上に反映するため)。※

※PHP,TypeScript,Python 以外の言語でツールを作成した場合は、そのときにツール使用言語でモジュールを作成する。

**AWS モジュール適用**

-   ツール使用言語が TypeScript の場合は事前に「aws-sdk」「moment」ライブラリをインストールしておく。

-   ツール使用言語に応じて以下のコードを追記する。

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
    }
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
    }
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

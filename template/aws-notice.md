# AWS 通知

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

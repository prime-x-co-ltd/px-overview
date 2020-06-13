# 自社開発ツール（AWS利用）の管理について

* 自社開発ツールのうち、AWSを用いたものの管理要領について記す。
* 開発に際する留意事項を記す。
* 自社開発ツール保守の要領は<a href="https://primeweb1.backlog.jp/alias/wiki/1074830458" target="_blank">Wiki</a>に記載。

## GitHub上で管理するもの

* 開発に関するドキュメント（px-overview/docs/awsに保管）

  * 管理要領＋開発に際する留意事項（本ドキュメント）
  * 自社開発ツール（EC2インスタンスレベル）のALL構成図
  * 自社開発ツール（AWSサービスレベル）の構成図
  * 構成図フォーマット

* １ツールに関するもの（各ツールでリポジトリを作成）
  * 運用ルールに則ったもの
  * テーブル定義書
  * ソース


## 構成図作成

* EC2インスタンスレベルの構成図はツール作成次第、<a href="https://px-develop.github.io/px-overview/aws/diagram/ec2instance/aws-自社開発システム構成図.pptx" target="_blank">aws-自社開発システム構成図.pptx</a>に追記する。
* AWSサービスレベルの構成図は<a href="https://px-develop.github.io/px-overview/aws/diagram/service/FMT/aws-diagram.drawio" target="_blank">フォーマット</a>をダウンロードし、<a href="https://app.diagrams.net/" target="_blank">作図ツール</a>を用いてpngファイルにて作成する。作成後、px-overview/docs/aws/diagram/serviceに保存する。

## クラウド申請

* ツール作成後、<a href="https://px-develop.github.io/px-overview/aws/diagram/ec2instance/aws-自社開発システム構成図.pptx" target="_blank">構成図</a>を添えて作成報告（ICT・イノベーション推進部ICTマネジメント課）。
* 必要あればクラウド申請を実施する。

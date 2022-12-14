# Template & Tips

アプリケーションテンプレート（リポジトリ）、コーディングテンプレートや、ドキュメントを豊かにするための Tips。充実させていきましょう..

---

- [Template \& Tips](#template--tips)
  - [Application Template](#application-template)
  - [Coding Template](#coding-template)
    - [kintone：customize-uploader](#kintonecustomize-uploader)
    - [kintone：plugin-uploader](#kintoneplugin-uploader)
    - [AWS：Serverless Framework / SAM](#awsserverless-framework--sam)
    - [AWS：通知](#aws通知)
  - [Tips](#tips)
    - [共通モジュール](#共通モジュール)
    - [dependency-cruiser](#dependency-cruiser)

## Application Template

-   kintone のアプリテンプレートや、GAS のテンプレートが存在します

## Coding Template

-   コーディングする上で共通化しておきたいものです
-   （アプリテンプレ（リポジトリ）に適用することも..）

### kintone：customize-uploader

-   カスタマイズした JS/CSS ファイルを CLI から指定のアプリにアップロードします
-   準備中

### kintone：plugin-uploader

-   開発したプラグインを CLI から kintone にアップロードします
-   準備中

### AWS：Serverless Framework / SAM

-   Lambda 関数を作成します
-   準備中

### AWS：通知

-   `px-app` or `px-batch` に構築したアプリケーションに適用します
-   ツールの処理成功/失敗ログを RDS に格納し、監視ダッシュボード上に反映します
-   細部はこちらに記載しています [template/aws-notice.md](./template/aws-notice.md)

## Tips

### 共通モジュール

-   Git submodule を使います
    <a href="https://github.com/px-develop/kintone_common_modules">kintone 共通モジュール</a>
    <a href="https://github.com/prime-x-co-ltd/aws-common-modules">aws 共通モジュール</a>

-   サブモジュールの追加

    ```bash
    git submodule add git@github.com:px-develop/kintone_common_modules [submoduleName]
    ```

-   詳細 | 複雑なので以下を参考にしてください。

    <a href="https://qiita.com/kinpira/items/3309eb2e5a9a422199e9">submodule と仲良くなる</a>

### dependency-cruiser

-   ルールに則って依存関係をバリデーション・描画する子です
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

-   README への適用
    -   `[image-name](./docs/hoge.svg)` で描画できます

# kintoneのスクリプト管理について

* webpackを使用してkintone適用のスクリプトを作成し、GitHubで管理する。
* 現状kintone上にて管理されているものは、随時GitHubへの管理に移行する。


## 1. webpackを使用する
GitHubにおける管理にあたり、webpackを使用する。

webpackとは
* 複数のモジュールを1つのファイルにまとめて出力するもの

なぜ利用するか
* 機能ごとにスクリプトファイルを分けられる＝モジュール化
  * 読みやすくなる
  * 開発・運用保守の分担作業が容易になる
  * 自身の作成モジュールだけでなく外部モジュールも利用できる
  * 汎用性が高まる

* kintone内のスクリプト管理が容易・簡潔になる
  * kintoneにはバンドルしたファイル1つを記述するのみ
  * 今まで煩雑だったスクリプト管理がすっきりとする
  * 保守性が高まる


### 1-[0] 下準備…
* スクリプトを管理するディレクトリを作成し、package.jsonを生成する
  ```
  npm init -y
  ```

### 1-[1] ディレクトリ内にwebpackをインストール

webpack
* webpack　─ node_modulesとpackage-lock.jsonを取得
* webpack-cli　─ "webpack" コマンドで実行するために必要
  ```
  npm install --save-dev webpack webpack-cli
  ```

ローダー
* バンドルする前にモジュールに対して実行する機能
* 必要なものをインストール
* babel-loader
  * @babel/core　─ Babel本体
  * @babel/preset-env　─ 環境に合わせてJSをトランスパイルする。IE11対策も
  ```
  npm install --save-dev babel-loader @babel/core @babel/preset-env 
  ```

プラグイン 
* モジュールのバンドル時に実行される処理
* 必要なものをインストール


### 1-[2] webpack.config.jsの設定

```
const path = require('path');

module.exports = {
  mode: 'development',
  entry: './src/index.js',
  output: {
    filename: 'customize.js',
    path: path.resolve(__dirname, 'dist')
  },
  (***)
}
```

* mode　：モードの設定
  * development　─ 開発用
  * production　─ 本番用
  * cf. 公式ではconfigを分けて作成することを推奨…
    * webpack.common.js
    * webpack.dev.js
    * webpack.prod.js
  * cf. webpack.config.jsに記述せずpackage.jsonのscripts記述で指定することも可能（後述）

* entry　：エントリーポイント
  * 各モジュールを読み込んでメインの処理するファイルを指定
  * 原則１ファイルを指定 ※複数指定も可能
  * エントリーファイルはsrc内に作成する（運用ルール）

* output　：出力先
  * filename　─ バンドルして作られた新しいJSファイルの名前
  * path　─ 出力先のパス。dist内に出力する（運用ルール）


```
module.exports = {
  (***)
  //ローダーの設定
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: [
          {
            loader: 'babel-loader',
            options: {
              presets: ['@babel/preset-env']
            }
          }
        ]
      }
    ]
  },
  //デベロッパーツールの設定
  devtool: 'cheap-module-eval-source-map',

  //webpack-dev-server サーバーの設定
  devServer: {
    open: true,
    openPage: 'index.html',
    contentBase: path.join(__dirname, 'public'),
    watchContentBase: true,
    port: 8080
  },
}
```

* module - rules　：ローダーの設定を行う
  * test　─ 処理対象の拡張子を正規表現で指定
  * exclude　─ 処理対象外のファイルを記述
  * use　─ 利用するローダーとそのオプションを指定


* devtool　：デバッグのためのソース出力の設定
  * 公式：https://webpack.js.org/configuration/devtool/


* devServer　：webpack-dev-serverの設定
  * open　─ true/false：サーバー起動時に自動的にブラウザを開く/開かない
  * openPage　─ 指定したページを自動的に開く
  * watchContentBase　─ true/false：コンテンツの変更監視をする/しない。trueの場合、ファイル変更時に自動リロード
  * port　─ ポート番号


### 1-[3] package.jsonの設定
* scripts　：コマンドの設定。"npm run ＊＊" で実行できる
  ```
  "scripts": {
    "start": "webpack-dev-server",
    "build": "webpack"
  },
  ```

  ※ modeの設定をwebpack.config.jsonで行わない場合
  → scriptsでmodeの指定を行う
    ```
    "scripts": {
      "start": "webpack-dev-server",
      "build": "webpack",
      "build:prod": "webpack --mode=production"
    },
    ```

* devDependencies
  * 使用するモジュールリスト。インストールしたら自動的に記載


### 1-[4] スクリプトを配置
* 機能ごとにスクリプトファイルを作成し、/src/js/内に配置
* エントリーポイントのファイルから各ファイルを読み込み


### 1-[5] ディレクトリ構造
```
ルートディレクトリ
[kintone-**-appId]
  │
  ├─ dist/           //配布用ファイル配置
  │    └─ customize.js
  ├─ src/            //スクリプト配置
  │    ├─ js/            //機能毎
  │    │   └─ ***.js
  │    └─ index.js       //エントリーポイント
  ├─ docs/            //ドキュメント配置
  │    └─ ***.md
  ├─ package.json
  ├─ package-lock.json
  ├─ webpack.config.js
  ├─ ****
  :
```

## 2. 動作の確認
手段は2通り

### ローカルWebサーバーを立てる
* kintoneのアプリ「設定」 > 「JS/CSSでカスタマイズ」
* https://localhost:8080/customize.js を追加
* "npm run start" でサーバー立ち上げ、動作はこちらで確認

### @kintone/customize-uploaderの利用
→細部確認中


## 3. アプリに適用
* バンドルした dist/customize.js をkintoneに記述


## 4. GitHubに配置
* 運用ルールにのっとってリポジトリをたててpushする

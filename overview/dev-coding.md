# コーディングルール

- [コーディングルール](#コーディングルール)
	- [命名](#命名)
		- [原則](#原則)
		- [詳細](#詳細)
		- [kintone DOM](#kintone-dom)
	- [スタイル](#スタイル)
		- [原則](#原則-1)
		- [prettier](#prettier)
		- [コメント](#コメント)
	- [禁止事項](#禁止事項)
	- [制限事項](#制限事項)
	- [推奨事項](#推奨事項)

## 命名

### 原則

-   プロジェクトの性格、使用するフレームワークなどに応じてカスタマイズして使用する

| 区分     | 種別                   | タイプ                  | ex. |
| :------- | :--------------------- | :---------------------- | :-- |
| ファイル | HTML/CSS               | `kebab-case`            |     |
|          | JS/TS                  | `lowerCamelCase`        |     |
| 関数     | -                      | `lowerCamelCase`        |     |
| 定数     | -                      | `UPPER_SNAKE_CASE`      |     |
|          | kintone DOM※           | DOM\_`UPPER_SNAKE_CASE` |     |
| 変数     | dynamic 変数           | `lowerCamelCase`        |     |
|          | static 変数            | `lowerCamelCase`        |     |
| クラス   | Class                  | `UpperCamelCase`        |     |
|          | Class メンバ・メソッド | `lowerCamelCase`        |     |
| 型       | -                      | `UpperCamelCase`        |     |

### 詳細

-   不安なスペルは確認する（えいやで書かない）
-   `名詞`、`動詞/形容詞+名詞`、`動詞` で命名する。命名したものが何の情報を保持しているか、何の役割を持つか明示する
-   各ファイルで命名するときの注意など...

### kintone DOM

-   [kintone JavaScript コーディングガイドライン](https://developer.cybozu.io/hc/ja/articles/201793484)

> 各要素に付与されている id/class 属性の値は、予告なく変更されることがあります。また、DOM 構造についても変更されることがあります。
> カスタマイズをされる際は、id/class 属性の値や DOM 構造を変更するカスタマイズを加えないようご注意ください。

-   DOM 操作を行う場合は、DOM 操作を行なっていることを明示する
    -   処理内で使用: id/class 名を定数に入れ、名称の接頭に `DOM_` をつける。`ex. DOM_XXX_XXX`
    -   CSS 内で指定: CSS ファイルをわけ、CSS ファイル名称の接頭に `dom-` をつける。

## スタイル

### 原則

-   プロジェクトの性格、使用するフレームワークなどに応じてカスタマイズして使用する

### prettier

-   VSCode `Prettier` 拡張プラグインを設定する
-   設定ファイル `.prettierrc` を `package.json` と同階層に配置する

```json
{
	"tabWidth": 4,
	"useTabs": true,
	"semi": false,
	"singleQuote": true,
	"jsxBracketSameLine": true,
	"bracketSpacing": true,
	"printWidth": 120
}
```

-   発展※`husky`を導入する（今後検討）

### コメント

## 禁止事項

## 制限事項

## 推奨事項

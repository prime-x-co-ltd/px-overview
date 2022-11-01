# コーディングルール

## 命名

おまとめ表

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

kintone とか

-   spaceId とか..

### 詳しく書くかもしれない

-   各ファイルで命名するときの注意など...
-   `動詞/形容詞→名詞` など..

### kintone DOM ※

-   [kintone JavaScript コーディングガイドライン](https://developer.cybozu.io/hc/ja/articles/201793484)

> 各要素に付与されている id/class 属性の値は、予告なく変更されることがあります。また、DOM 構造についても変更されることがあります。
> カスタマイズをされる際は、id/class 属性の値や DOM 構造を変更するカスタマイズを加えないようご注意ください。

-   DOM 操作を行う場合は、id/class 名を定数に入れ、名称の接頭に `DOM_` をつける。`ex. DOM_XXX_XXX`
-   CSS ファイル内で操作する場合は、ファイルをわけ、CSS ファイル名称の接頭に `dom_` をつける。

## スタイル

### prettier

-   VSCode `Prettier` 拡張プラグインを設定する
-   設定ファイル `.prettierrc` を `package.json` と同階層に配置する

```json
{
	"tabWidth": 4,
	"semi": false,
	"useTabs": true,
	"singleQuote": true,
	"jsxBracketSameLine": true,
	"printWidth": 120,
	"bracketSpacing": true
}
```

### コメント

-   変数
-   関数・クラス

## 禁止事項

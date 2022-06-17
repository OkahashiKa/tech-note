# ESLintルールについて

プロジェクトで利用しているESLintルールを記載します。
ESLintのルールに違反している構文を利用する場合は、次のコメントで回避してください。このルールはやむを得ない場合を除いて原則禁止とします。

```javascript
// eslint-disable-next-line no-restricted-syntax
```

ESLintのルールをこちらをご参照下さい。

<https://eslint.org/docs/rules/>

## ルール

推奨されたルールは`eslint:recommended`によって定められます。
次のリンクのチェックされた項目が推奨ルールとなります。

<https://eslint.org/docs/rules/>

- TSEnumDeclaration

Enum 禁止。

- VariableDeclaration[kind='var']

var 禁止。基本的には const、どうしても再代入しなければいけない状況下では letを利用する。

- jsdoc/require-jsdoc

クラス、メソッドのコメントを強制する。
Angular のライフサイクルメソッドは書かなくてよい。

- jsdoc/require-description

コメントに説明を書くことを必須とする。

- jsdoc/require-param

コメントにパラメータを書くことを必須とする。

- jsdoc/require-returns

コメントに戻り値を書くことを必須とする。

- prefer-template

テンプレート構文を強制する。

```javascript
// NG
const fullName = firstName + ' ' + lastName
// OK
const fullName = `${firstName} ${lastName}`
```

- no-console

console 系を禁止にする。警告が出るがデバッグで利用出来る。

- TryStatement

try、catch 禁止。

- no-unused-vars

未使用変数を禁止。

- no-alert

alert 禁止。

- @typescript-eslint/no-explicit-any

any 禁止。

- import/order

importのソートを強制する。

- @typescript-eslint/explicit-member-accessibility

アクセス修飾子を強制する。

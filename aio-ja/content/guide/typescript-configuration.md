# TypeScriptの設定

TypeScriptは、Angularアプリケーション開発の主要言語です。
これはJavaScriptのスーパーセットで、型安全性とツーリングのための設計時サポートを備えています。

ブラウザはTypeScriptを直接実行できません。Typescriptは、*tsc*コンパイラを使用してJavaScriptに "変換"する必要があります。
そのためにはいくつか設定が必要です。

このページでは、Angular開発者にとって重要なTypeScriptの構成と環境について、
主に次のファイルの詳細を説明します。

* [tsconfig.json](guide/typescript-configuration#tsconfig)&mdash;TypeScriptコンパイラの設定。
* [typings](guide/typescript-configuration#typings)&mdash;TypesScriptの宣言ファイル.


{@a tsconfig}



## *tsconfig.json*
通常、`tsconfig.json`というTypeScript構成ファイルをプロジェクトに追加し、
コンパイラがJavaScriptファイルを生成する際のガイドを行います。

<div class="l-sub-section">



`tsconfig.json`の詳細については、公式の
[TypeScript wiki](http://www.typescriptlang.org/docs/handbook/tsconfig-json.html)を参照してください。

</div>



[セットアップガイド](guide/setup)では、次の`tsconfig.json`が使用されています。

<code-example path="quickstart/src/tsconfig.1.json" title="tsconfig.json" linenums="false"></code-example>

このファイルには、Angularアプリケーションに不可欠なオプションとフラグが含まれています。


{@a noImplicitAny}

<!-- ここのくだり、セクションごとあとで見直す。今はひとまず直訳っぽく。-->
### *noImplicitAny* と *suppressImplicitAnyIndexErrors*

TypeScriptの開発者は、`noImplicitAny`フラグを`true`または`false`にするかどうかについては同意しません。
この問題に正解はなく、あとでフラグを変更することができます。
しかし、この選択は大規模プロジェクトにおいて大きな影響を与える可能性があるので、議論に値します。

`noImplicitAny`フラグが`false`（デフォルト）のとき、
コンパイラが変数の型を自動推論できなかった場合は、
型を`any`にデフォルト設定します。それは*暗黙の`any`*とみなされます。

ドキュメンテーションのセットアップでは、`noImplicitAny`フラグが`true`に設定されます。
`noImplicitAny`フラグが`true`で、TypeScriptコンパイラが型を推論できない場合でも、
JavaScriptファイルは生成されますが、**エラーも出力されます**。
これはより厳格な型チェックとなりますが、コンパイル時に型チェックが意図していないエラーをキャッチできるので、
多くのベテラン開発者が好む傾向にあります。

`noImplicitAny`フラグが`true`の場合でも、変数の型を`any`に設定することが可能です。

`noImplicitAny`フラグが`true`の場合、*暗黙のインデックスエラー*も発生する可能性があります。
ほとんどの開発者は、*この特定のエラー*が役立つよりも迷惑であると感じています。
次の追加フラグを使用してそれらを制御することができます：

<code-example format=".">
  "suppressImplicitAnyIndexErrors":true

</code-example>



ドキュメントのセットアップでは、このフラグも`true`に設定されます。


{@a typings}



## TypeScript Typings
jQuery・Jasmineテストライブラリ・Angularなどの多くのJavaScriptライブラリは、
TypeScriptコンパイラが認識できない機能と構文を用いて
JavaScript環境を拡張しています。
コンパイラが何かを認識できないと、エラーをスローします。

Use [TypeScript type definition files](https://www.typescriptlang.org/docs/handbook/writing-declaration-files.html)&mdash;`d.ts files`&mdash;to tell the compiler about the libraries you load.

TypeScript-aware editors leverage these same definition files to display type information about library features.

Many libraries include definition files in their npm packages where both the TypeScript compiler and editors
can find them. Angular is one such library.
The `node_modules/@angular/core/` folder of any Angular application contains several `d.ts` files that describe parts of Angular.

**You need do nothing to get *typings* files for library packages that include `d.ts` files.
Angular packages include them already.**

### lib.d.ts

TypeScript includes a special declaration file called `lib.d.ts`. This file contains the ambient declarations for various common JavaScript constructs present in JavaScript runtimes and the DOM.

Based on the `--target`, TypeScript adds _additional_ ambient declarations
like `Promise` if the target is `es6`.

Since the QuickStart is targeting `es5`, you can override the
list of declaration files to be included:


<code-example format=".">
  "lib": ["es2015", "dom"]

</code-example>



Thanks to that, you have all the `es6` typings even when targeting `es5`.

### Installable typings files
Many libraries&mdash;jQuery, Jasmine, and Lodash among them&mdash;do *not* include `d.ts` files in their npm packages.
Fortunately, either their authors or community contributors have created separate `d.ts` files for these libraries and
published them in well-known locations.

You can install these typings via `npm` using the
[`@types/*` scoped package](http://www.typescriptlang.org/docs/handbook/declaration-files/consumption.html)
and Typescript, starting at 2.0, automatically recognizes them.

For instance, to install typings for `jasmine` you could do `npm install @types/jasmine --save-dev`.


QuickStart identifies two *typings*, or `d.ts`, files:

* [jasmine](http://jasmine.github.io/) typings for the Jasmine test framework.

* [node](https://www.npmjs.com/package/@types/node) for code that references objects in the *nodejs* environment;
you can view an example in the [webpack](guide/webpack) page.

QuickStart doesn't require these typings but many of the samples do.


{@a target}


### *target*

By default, the target is `es5`, you can configure the target to `es6` if you only want to deploy the application to
es6 compatible browser. But if you configure the target to `es6` in some old browser such as `IE`, `Syntax Error` will be thrown.

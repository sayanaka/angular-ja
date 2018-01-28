# Npm Packages

 The [**Angular CLI**](https://cli.angular.io/), Angular applications, and Angular itself depend upon features and functionality provided by libraries that are available as [**npm**](https://docs.npmjs.com/) packages.

You can download and install these npm packages with the [**npm client**](https://docs.npmjs.com/cli/install), which runs as a node.js application.

[**yarn**](https://yarnpkg.com/en/)は、npmパッケージをインストールするための一般的な方法です。
Angular CLIは新しいプロジェクトを作成する際、`yarn`を用いてnpmパッケージをインストールしています。

<div class="l-sub-section">

Node.jsとnpmは、Angularの開発に不可欠です。

まだインストールされていない場合は、[こちら](https://docs.npmjs.com/getting-started/installing-node "Node.jsのインストールと npmのアップデート")から入手してください。

ターミナル/コンソールウィンドウで、コマンド`node -v` および` npm -v` を実行して、**Node.js `v4.x.x以上` かつ `npm 3.x.x以上`を実行していること**を確認します。これより古いバージョンではエラーが発生します。

他のバージョンのNode.jsとnpmを使用しているプロジェクトが存在している場合は、[nvm](https://github.com/creationix/nvm) を用いて、複数バージョンのNode.jsとnpmを管理することを検討してください。

</div>

## _package.json_

`npm`と`yarn`はともに、[**package.json**](https://docs.npmjs.com/files/package.json)に指定されているパッケージをインストールします。

CLIの `ng new` コマンドは、デフォルトの `package.json` を作成します。この `package.json` には、さまざまなアプリケーションに対応できるように、_基本的なパッケージ_ が指定されています。

また、アプリケーションの必要性に応じて、パッケージを追加・削除することができます。

このガイドでは、_基本的なパッケージ_ の中でも特に重要度が高いものに焦点を当てています。

#### *dependencies* と *devDependencies*

`package.json` には、[dependencies](guide/npm-packages#dependencies) と [devDependencies](guide/npm-packages#dev-dependencies) の２種類のパッケージ区分があります。

*dependencies* は、*アプリケーションの実行* に不可欠です。*devDependencies* は、 *アプリケーションの開発時* のみ必要となります。

{@a dependencies}

## *Dependencies*
`package.json` の `dependencies` セクションには、次のものが含まれています:

* **Angular packages**: パッケージ名が `@angular/` から始まる、Angular のコアライブラリ及びオプションライブラリ

* **Support packages**: Angularアプリを実行するために必要な サードパーティー製ライブラリ

* **Polyfill packages**: ブラウザのJavaScript実装の差異を埋める Polyfillsライブラリ

### Angular Packages

**@angular/animations**: Angularのアニメーションライブラリは、ページ遷移やリスト遷移などのアニメーション効果を簡単に定義・適用することができます。
詳細は [Animations guide](guide/animations) を参照してください。

**@angular/common**: Angularチームが提供する service/pipe/directive。
また、[`HttpClientModule`](guide/http) は、 '@ angular / common / http'内にあります。

**@angular/core**: Angularの重要なランタイム部。
すべてのメタデータデコレータ・`Component`・`Directive`・依存関係注入・コンポーネントのライフサイクルフックが含まれています。

**@angular/compiler**: Angularの *テンプレートコンパイラ*。
テンプレートを理解し、アプリケーションを実行・レンダリングするコードに変換します。
通常、コンパイラとは直接対話しません。ブラウザが [JITコンパイル](guide/aot-compiler) する際に、`platform-browser-dynamic`経由で間接的に使用します。

**@angular/forms**: [template-driven](guide/forms) と [reactive forms](guide/reactive-forms) のサポート。

**@angular/http**: 廃止予定のHTTPクライアント。

**@angular/platform-browser**: すべてのDOMとブラウザ、特にDOMへのレンダリングを担う。
このパッケージには、[AOT](guide/aot-compiler) で事前コンパイルするプロダクションビルド用のアプリケーションをブートストラップするための`bootstrapStatic()`メソッドも含まれています。

**@angular/platform-browser-dynamic**: [JITコンパイラ](guide/aot-compiler) を使用してクライアント上でアプリケーションをコンパイル・実行する [Providers](api/core/Provider) とメソッドを含みます。

**@angular/router**: URLが変更されると、[ルータモジュール](/guide/router) がアプリページを遷移させます。

**@angular/upgrade**: AngularJSのアプリケーションをAngularアプリケーションにアップグレードするためのユーティリティ。

{@a polyfills}

### Polyfill packages

Many browsers lack native support for some features in the latest HTML standards,
features that Angular requires.
"[Polyfills](https://en.wikipedia.org/wiki/Polyfill)" can emulate the missing features.
The [Browser Support](guide/browser-support) guide explains which browsers need polyfills and 
how you can add them.

The default `package.json` installs the **[core-js](https://github.com/zloirock/core-js)** package
which polyfills missing features for several popular browser.

### Support packages

**[rxjs](https://github.com/benlesh/RxJS)**: Many Angular APIs return _observables_. RxJS is an implementation of the proposed [Observables specification](https://github.com/zenparsing/es-observable) currently before the
[TC39](http://www.ecma-international.org/memento/TC39.htm) committee that determines standards for the JavaScript language.


**[zone.js](https://github.com/angular/zone.js)**: Angular relies on zone.js to run Angular's change detection processes when native JavaScript operations raise events.  Zone.js is an implementation of a [specification](https://gist.github.com/mhevery/63fdcdf7c65886051d55) currently before the
[TC39](http://www.ecma-international.org/memento/TC39.htm) committee that determines standards for the JavaScript language.


{@a dev-dependencies}

## *DevDependencies*

The packages listed in the *devDependencies* section of the `package.json` help you develop the application on your local machine.

You don't deploy them with the production application although there is no harm in doing so.

**[@angular/cli](https://github.com/angular/angular-cli/)**: The Angular CLI tools.


**[@angular/compiler-cli](https://github.com/angular/angular/blob/master/packages/compiler-cli/README.md)**: The Angular compiler, which is invoked by the Angular CLI's `build` and `serve` commands.


**[@angular/language-service](https://github.com/angular/angular-cli/)**: The Angular language service analyzes component templates and provides type and error information that TypeScript-aware editors can use to improve the developer's experience.
For example, see the [Angular language service extension for VS Code](https://marketplace.visualstudio.com/items?itemName=Angular.ng-template)


**@types/... **: TypeScript definition files for 3rd party libraries such as Jasmine and node.


**[codelyzer](https://www.npmjs.com/package/codelyzer)**: A linter for Angular apps whose rules conform to the Angular [style guide](guide/styleguide).


**jasmine/... **: packages to support the [Jasmine](https://jasmine.github.io/) test library.


**karma/... **: packages to support the [karma](https://www.npmjs.com/package/karma) test runner.


**[protractor](https://www.npmjs.com/package/protractor)**: an end-to-end (e2e) framework for Angular apps. 
Built on top of [WebDriverJS](https://github.com/SeleniumHQ/selenium/wiki/WebDriverJs).


**[ts-node](https://www.npmjs.com/package/ts-node)**: TypeScript execution environment and REPL for node.


**[tslint](https://www.npmjs.com/package/tslint)**: a static analysis tool that checks TypeScript code for readability, maintainability, and functionality errors.


**[typescript](https://www.npmjs.com/package/typescript)**:
the TypeScript language server, including the *tsc* TypeScript compiler.


## So many packages! So many files!

The default `package.json` installs more packages than you'll need for your project.

A given package may contain tens, hundreds, even thousands of files,
all of them in your local machine's `node_modules` directory.
The sheer volume of files is intimidating, 

You can remove packages that you don't need but how can you be sure that you won't need it?
As a practical matter, it's better to install a package you don't need than worry about it.
Extra packages and package files on your local development machine are harmless.

By default the Angular CLI build process bundles into a single file just the few "vendor" library files that your application actually needs.
The browser downloads this bundle, not the original package files.

See the [Deployment](guide/deployment) to learn more.

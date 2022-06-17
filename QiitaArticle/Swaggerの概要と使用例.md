# Swaggerの概要と使用例

## はじめに

この記事は「[PERSOL PROCESS & TECHNOLOGY Advent Calendar 2020](https://qiita.com/advent-calendar/2020/ppt)」の18日目の記事です。
幅広い範囲の記事が記載されておりかなり面白いので、興味がある方はこちらもぜひご覧ください。

お疲れ様です。お酒を作ることとお酒を飲むことしか能のない人です。
当方脳をお酒に侵食されておりますので、内容がでたらめな場合はご指摘のほどよろしくお願いいたします。

本日は、最近何かと業務内外で触ることの多かったSwaggerとその周辺ツールについての概要と使用例を自分なりにまとめ、記事にしたいと思います。

## Swaggerとは

Swaggerとは、OpenAPI Specification(以下OAS)という「RESTful APIを定義するフォーマットに基づいて構築された一連のオープンソースツール群」を指します。
なので、一般にSwaggerというとyaml形式で書かれたAPI定義を連想する方が多いかと思いますが、あれは正確にはSwaggerではなくOASといいます。（実際の現場では往々にしてSwaggerと呼ばれます。）

以前はRESTful APIを定義するフォーマットもSwagger Specificationという名称が使われていましたが、
Smarter Bear社のSwaggerは2015年12月に、マイクロソフトやグーグルなどにより設立されたOAI(Open API Initiative)に寄贈されるなど紆余曲折あり、2017年7月のバージョン3.0のリリースと共にOASへと名前を変更しました。
公式曰く、
> OpenAPI = 仕様
> Swagger = 仕様を実装するためのツール

だそうです。

詳しくは公式にSwaggerとOpenAPIの違いについての記事があるので、興味のある方はそちらをご覧ください。
[What Is the Difference Between Swagger and OpenAPI?](https://swagger.io/blog/api-strategy/difference-between-swagger-and-openapi/)

## Swaggerツール群

メジャーなSwaggerツールは以下のようなものがあります。

| 名称 | 概要 |
|:-:|:-:|
|[Swagger UI](https://swagger.io/tools/swagger-ui/)|yamlやjsonで書かれたOASを人間が理解できるようにレンダリングしてくれます。多くのOASエディターのプレビュー機能ではこのUIが使用されています。|
|[Swagger Editor](https://editor.swagger.io/)|ブラウザ上で動作するOASエディターです。フォーマットに反した記載をすると怒られます。Swagger UIでレンダリングされたプレビューが右側に表示されます。VScodeにも同様の機能を提供する拡張機能が存在します。|
|[Stoplight Studio](https://stoplight.io/studio/)|OASをGUI操作で直感的に作成することができます。私はいまだにVScodeで脳をとろかしながらyamlを書いていますが、慣れたら絶対こっちの方が早い。|
|[Swagger Codegen](https://swagger.io/tools/swagger-codegen/)|OASからクライアント/サーバコードを「ある程度」自動生成するコマンドラインツールです。「ある程度」というのはあくまでエンドポイント部分が作られるのみでロジック等は自分で実装する必要があります。なのでどちらかというと定義したAPIのスタブを自動生成してくれるツールというイメージが近いです。|

## Swaggerを使うメリット

Swaggerを使用するメリットとしては主に以下の点が挙げられます。

- **API定義書をExcel管理しなくても良い**
OASがそのままAPI定義となるため、Excel等にAPI定義書を用意する必要がなくなります。
（納品物にExcelでのAPI定義が必要な場合等Excelの仕様書が必要な場合は諦めてSwagger UIに表示されるものを写経しましょう。。。）<br>さらにOASはyamlまたはjsonで記載されるため、ソースと同様にGitで管理することが可能です。変更管理の必要がなくなります。

- **定義と実装の隔離が起きにくい**
完全に防げるというわけではありませんが、OpenAPI Generatorで自動生成されるソースをライブラリ登録し、そのライブラリ内のスタブをOverrideして実装するなど運用次第で、定義と大きくズレることはなくなります。
- **スキーマファーストで開発が行える**
OASを起点としてサーバ/クライアントの開発を始めることでスキーマファーストでの開発を行うことが可能です。

## 使用例

ここまでSwaggerの概要をつらつらと書き連ねてきたので、
ここからは実際に私も使っているSwaggerの使用例を紹介していきます。

### 静的HTML生成

OASから人間が理解可能な形に整形された静的HTMLを生成する方法です。
今回は[ReDoc](https://redocly.github.io/redoc/)というツールを使用します。生成後のイメージはこんな感じです。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/919921/58fb2fd6-73e0-8dfe-2d2c-6152c06b5e18.png)

公式が提供しているSwagger UIやSwaggerCodegenからも静的HTMLが出力可能ですが、
こんな感じでとても見にくいです。なので今回は使いません。
![MicrosoftTeams-image (1).png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/919921/c7fc878a-8db5-17f6-87a5-66228864b1f1.png)

#### OASの用意

最初は、あたりまえですがHTMLにするOASを用意する必要があります。
OASの記載方法もこの記事で書くつもりだったのですが、それだけでかなりの文量になってしまいそうなので今回は省略し、実際に遭遇したハマりポイントとTIPS等も交えて別の機会で記事にまとめようと思っています。。。

とはいえ、構造自体はそこまで複雑ではないので記載方法は公式のリファレンスを見れば大体理解できるかと思います。
[OpenAPI Specification 公式](https://swagger.io/specification/)

今回はサンプルとして、カクテル情報の全件リストを取得するというAPIのOASを用意しました。

``` yaml
openapi: 3.0.1
info:
  title: Cocktail API
  description: カクテルの情報を取得するAPIです。
  contact:
    email: kazuki.okahashi@cloudsteady.jp
  version: 0.1.0
servers:
  - url: 'http://localhost/api/v1/cocktail'
    description: Local server
tags:
  - name: Cocktail
    description: カクテルに関するAPIです。

paths:
  /cocktail:
    get:
      tags:
        - Cocktail
      summary: カクテルの情報を全件取得します。
      security:
        - bearerAuth: []
      responses:
        '200':
          $ref: '#/components/responses/CocktailGetResponce'
components:
  responses:
    CocktailGetResponce:
      description: カクテル情報取得レスポンス
      content:
        application/json:
          schema:
            $ref: '#/components/schemas/CocktailList'
  schemas:
    CocktailList:
      description: カクテル情報リスト
      type: array
      items:
        $ref: '#/components/schemas/CocktailModel'
    CocktailModel:
      description: カクテル情報モデル
      type: object
      properties:
        cocktailId:
          $ref: '#/components/schemas/CocktailId'
        cocktailName:
          description: カクテル名
          type: string
          format: string
          example: ジントニック

    # 以下、複数モデルで使用する共通部品
    CocktailId:
      description: カクテルID
      type: integer
      format: integer
      example: 1
```

#### ReDocのインストール

次にReDocはCLIも提供しているのでCLIをインストールします。

``` bash
npm install -g redoc-cli
```

#### 静的HTMLの生成

最後に以下のコマンドでHTMLを生成します。

``` bash
redoc-cli bundle [OAPファイル] -o [出力ファイル名]
```

先ほどのカクテル取得APIのOASをHTMLとして出力するとこんな感じになります。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/919921/2ef9cccd-769c-fec3-de3a-395353021e3d.png)
yamlで記載されていた暗号文の状態より見違えるようにわかりやすくなりました。
この状態であればAPI定義ドキュメントとして成立するかなと思っています。

### スタブ自動生成

OASから実際のAPIのスタブを生成する方法です。

今回は[OpenAPI Generator](https://openapi-generator.tech/)というツールを使用します。
公式が提供しているSwaggerCodegenでも出力可能ですが、
現状、最新のOASv3への対応言語がOpenAPI Generatorの方が圧倒的に多いという点から、基本的にOpenAPI Generatorを使用することをお勧めします。

ちなみに対応言語の比較はこちらのサイトにわかりやすく纏まっています。
[Swagger Codegen と OpenAPI generatorの比較(2020/02版)](https://blog.rhyztech.net/swagger_codegen_v2_vs_v3/)

#### OASの用意

静的HTML生成時に使用したものを同じものを使用します。

#### OpenAPI Generatorの使用

こちらもCLIが提供されており[様々なインストール方法](https://openapi-generator.tech/docs/installation)が用意されていますが、今回はdocker imageを使用してソースの自動生成を行います。
以下のコマンドで生成が始まります。

``` bash
docker run --rm \
  -v $ { PWD } ：/ local openapitools / openapi-generator-cli generate \
  -i /local/openapi.yaml \
  -g aspnetcore \
  -o /local/aspnetcore
```

| option | 概要 |
|:-:|:-:|
|-i|OASを指定します。|
|-g|生成したいスタブの言語を指定します。|
|-o|出力先を指定します。生成したコードを出力する場所は事前に作っておいたほうが良いです。|
|-c|今回は使用していませんが、[コンフィグファイル](https://openapi-generator.tech/docs/generators)を選択できます。|

成功すると以下のようなソースが自動生成されます。
![MicrosoftTeams-image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/919921/fbce1cf3-7bee-31cf-9bd1-16693bdae214.png)
OASで定義したエンドポイントとモデルが生成されていることが確認できます。
この自動生成されたコードにロジックをがりがり実装していくことで、エンドポイント周りの実装が統一されたソースにすることができます。

## まとめ

社内のプロジェクトで初めてSwaggerに出会い、分担しながらではありますが2000行以上のyamlを何本も脳を溶かしながら書いていたころは、まさか自分がSwaggerについての記事を書くとは思ってもいませんでした。今となっては良い？思い出です。

他のプロジェクトや個人で作っているものでもSwaggerを書いてみて、小規模開発ではAPIを自動生成したり記載を統一できるメリットよりyamlを書く労力の方が重いような気がしているので、中規模～大規模プロジェクトで真価を発揮する技術なのかなとは思いました。個人で作っているものはドキュメント残す必要ないですしね。。。

今後は実際のOASの記載法や自動生成ソースをライブラリ登録する方法などを記事にしたいと考えています。

ここまで拙い長文にお付き合いいただきありがとうございます。
この記事が誰かの役に立つことを願っています。

おしまいです。

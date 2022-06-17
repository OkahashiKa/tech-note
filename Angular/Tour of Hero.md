# Tour of Hero

- Angularはリソースに変更があった場合に再ビルドを行自動更新する。
  - バインドが行われた変数に変更が加わった場合にも自動更新が行われるのか？（）
    > ng serveコマンドはアプリケーションをビルド、開発用サーバーを起動し、ソースファイルを監視します。 あなたが監視されているファイルに変更を行ったときには、変更があったファイルに対し再ビルドを行います。
- Angularのモデルバインディングはコンポーメントクラスで定義された変数をHTML側で{{}}で囲んで入力することで実現できる。
- src/style.cssにcssを記載することによりプロジェクト全体共通のスタイルを適応できる。
    > ほとんどのアプリケーションは、アプリケーション全体で一貫した見た目を目指しています。 CLIはこの目的のために、空のstyles.cssを生成しました。 アプリケーション全体に適用するスタイルをそこに記述してください。
- コンポーネントの作成

  ```　bash
  ng generate component $COMPONENT_NAME
  ```

- AngularのintarfaseクラスはC#のモデルクラスのような振る舞いをする。コンポーネントクラスのプロパティにHero型をリファクタリングすることでobject型のプロパティを定義できる。
- [(ngModel)]でコンポーネントクラスプロパティと画面との双方向バインディングが行える。

    ``` ts
    // src/app/heroes/heroes.component.html
    <input [(ngModel)]="hero.name"/>
    ```

- すべてのコンポーネントは、src/app/app.module.tsのNgModuleで宣言される必要がある。（AngularCLIからコンポーネントを作成した場合は自動インポートされる。）
- コンポーネント.htmlには*ngFor=""で反復処理を追加することができる。記載方法はC#のforeachとほぼ同じ。

    ``` ts
    /// *ngFor="let 変数名 of 配列名"
    *ngFor="let hero of heroes"
    ```

- *ngIf は指定したプロパティが存在しない場合は非表示とする。

    ``` ts
    <div *ngIf="selectedHero"> ~ </div>
    ```

- htmlタグ内に条件付きバインディングを追加できる。

    ``` ts
    [class.selected]="hero === selectedHero"
    ```

- クリック発火の処理はhtml内でonClickではなく(click)="onSelect(hero)"と記載する。
- 子コンポーネントの呼び出し時には引数を設定できる。

    ``` ts
    <app-hero-detail [hero]="selectedHero"></app-hero-detail>
    ```

- サービスの作成

    ``` ts
    ng generate service <サービス名>
    ```

- コンポーネント内では直接データの取得や保存を行うべきではないため個別でServiceを生成しDIする。
- ng generate serviceではデフォルトのスコープがrootに設定してある。rootに設定した場合プロジェクトで単一のインスタンスを各コンポーネントに提供する。

    ``` ts
    @Injectable({
        providedIn: 'root',
    })
    ```

- コンストラクタ内ではプロパティ定義や初期化を以外は記載するべきではないため。コンポーネント内の常に取得する値の取得等はngOnInit ライフサイクルフック内で呼び出す。

    ``` ts
    ngOnInit() {
        this.getHeroes();
    }
    ```

- コンストラクタでDIしたServiceのアクセス修飾子をpublicにすると対応するHTML内でバインドすることが可能。
- (click)はクラス設定の後にスペースを開けずに記載する。半角スペースを記載すると反応しなくなる。

    ``` ts
    <button class="clear"(click)="messageService.clear()">clear</button>
    ```

- AppRoutingModule は アプリにルーティング機能を持たせることができる。
- ルートは、ユーザーがリンクをクリックしたとき、またはURLをブラウザのアドレスバーに貼り付けたときに、 どのビューを表示したらよいかをルーターに伝えます。典型的なAngularのRouteはふたつのプロパティを持っています。

1. path：ブラウザのアドレスバーにある URL にマッチする文字列
2. component：そのルートに遷移するときにルーターが作成すべきコンポーネント

- ルーティングしたコンポーネントはrouter-outlet タグの箇所にパスに対応するコンポーネントが表示される。

    ``` html
    <router-outlet></router-outlet>
    ```

- routoerLink属性はapp-routing.module.tsで設定したパスへのリンクを設定を実装できる。

    ``` html
    <nav>
        <a routerLink="/heroes">Heroes</a>
    </nav>
    ```

- router-outletの箇所はルートを設定していない場合は空白となるため、リダイレクト先を設定する必要がある。

    ``` ts
    { path: '', redirectTo: '/dashboard', pathMatch: 'full' },
    ```

- route.snapshotは、コンポーネントが作成された直後のルート情報の静的イメージ。
- paramMapは、URL から抽出されたルートパラメータ値の辞書であり "id"キーは、フェッチするヒーローのidを返す。

    ``` ts
    const id = +this.route.snapshot.paramMap.get('id');
    ```

- TODO: Observableについての理解が足りない。
- catchError()オペレーターは失敗したObservableに割り込みます。 そうするとオペレーターはエラーをエラーハンドリング関数に渡します。

    ``` ts
    getHeroes(): Observable<Hero[]> {
        return this.http.get<Hero[]>(this.heroesUrl)
            .pipe(
                catchError(this.handleError<Hero[]>('getHeroes', []))
            );
        }
    ```

- 変数にof()を付けるとobservableに変換される。
- Angularのテンプレート内に参照変数を
- id: User pass: P@ssword
- formControlとdesableは共存できないため、Conponent内でFromControllをNewるする際にdesabled=trueを設定する。
- Angularにおいてお互いに参照しあうような構成にする場合、循環依存のWarningが発生する。意図した動作の場合はangular.jsonに以下の記載をして表示を抑制する。

    ``` json
    {
    "projects": {
      "my-project": {
        "architect": {
          "build": {
            "options": {
                "showCircularDependencies": false
            }
          }
        }
      }
    }
    ```

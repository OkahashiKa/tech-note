# Next.js App Setup

## Next.js

https://nextjs.org/

### 環境構築

https://nextjs.org/docs/getting-started

1. Next.js アプリケーションの作成

   ```bash
   yarn create next-app --typescript
   ```

   - この後、アプリ名の入力を求められるので入力する。
   - --ts, --typescript オプションで TypeScript で開発を行える。

2. 開発サーバの起動

   ```bash
   yarn dev
   ```

   デフォルトは 3000 番ポートで起動するが、使用済みの場合は 3001, 3002 とインクリメントされていく。

### Absolute Imports

https://nextjs.org/docs/advanced-features/module-path-aliases

tsconfig.json 内に baseUrl と Path Aliases を設定し、以下の絶対パスの形式で inport を行う。

```json
{
  "baseUrl": ".",
  "paths": {
    "@/*": ["src/*"]
  }
}
```

```ts
// importサンプル
import { Button } from "@/components/atoms/button";
```

## ESLint

- Next.js は ESLint がデフォルトでインストールされているため導入不要。

### ESLint の実行

```bash
yarn lint
```

## Prettier

### Setup

1. インストール

   ```bash
   yarn add --dev eslint-config-prettier
   ```

1. eslintrc.json に prettier を追記する。

   ```json
   {
     "extends": ["next", "prettier"]
   }
   ```

1. package.json 内の scripts に pritter のコマンドを定義する。

   ```json
   "scripts": {
       "prettier": "prettier --write 'src/**/*.{ts,tsx,json,md}'"
   },
   ```

### 使い方

```bash
yarn prettier
```

src 内の全ての ts, tsx, json, md ファイルが自動フォーマットされる。

### VSCode に導入

1. 拡張機能「Prettier - Code formatter」のインストール。
2. Format On Save を有効にする。
3. Default Formatter を Prettier に設定する。

## Storybook

https://storybook.js.org/

### Setup

1. storybook の導入

   ```bash
   npx sb init
   ```

   - package.json の中身から Next.js のプロジェクトだと判別する。賢い。
   - 途中で以下以下の内容を聞かれるが、 ESLint は導入済みのため N を入力する。

     ```bash
     Do you want to run the 'eslintPlugin' fix on your project?
     ```

1. main.js に path alias の設定を記載する。

   ```ts
   const path = require("path");

   module.exports = {
     stories: [
       "../src/**/*.stories.mdx",
       "../src/**/*.stories.@(js|jsx|ts|tsx)",
     ],
     addons: ["@storybook/addon-links", "@storybook/addon-essentials"],
     framework: "@storybook/react",
     webpackFinal: async (config) => {
       config.resolve.alias = {
         ...config.resolve.alias,
         "@": path.resolve(__dirname, "/src"),
       };
       return config;
     },
   };
   ```

   この設定を加えると.stories.tsx からもエイリアス絶対パスで import ができるようになる。

   ```ts
   import { Button } from "@/components/atoms/button";
   ```

1. 各ストーリーを src/stories/\*\*/に配置する。

### Storybook の実行

```bash
yarn storybook
```

### Addon

### @storybook/addon-essentials

初期から導入されている公式アドオンオールインパッケージ。
Docs とか actions とか便利なものが入っている。

### @storybook/addon-knobs

storybook のコンソール上から props を編集できるようになる。便利。

```bash
export const SampleButton: ComponentStory<typeof Button> = () => (
  <Button label={text('label', 'サンプルボタン')} onClick={() => {}} />
);
```

## Firebase

https://firebase.google.com

### Setup

https://firebase.google.com/docs/web/setup

1. Firebase プロジェクトを作成する。

   - [Firebase コンソール](https://console.firebase.google.com/)

2. アプリケーションをの登録を行う。

   - アプリを登録した際に表示される Config 情報はコピーしておく。

3. FirebaseSDK のインストール

   ```bash
   yarn add firebase
   ```

### FireStore

https://firebase.google.com/docs/firestore/quickstart?hl=ja

1. 任意のディレクトリに FirebaseClient を作成する。

   ```ts
   import { initializeApp } from "firebase/app";
   import { getFirestore } from "firebase/firestore";

   // TODO: Replace the following with your app's Firebase project configuration
   // See: https://firebase.google.com/docs/web/learn-more#config-object
   const firebaseConfig = {
     // ...
   };

   // Initialize Firebase
   const app = initializeApp(firebaseConfig);

   // Initialize Cloud Firestore and get a reference to the service
   const db = getFirestore(app);
   ```

   firebaseConfig には ApiKey や projectId など firebase との通信に必要な情報を記載する。
   `initializeApp()`で Firebase、`getFirestore()`で FireStore の初期化を行う。

### StyledFirebaseAuth

https://github.com/firebase/firebaseui-web-react

1. インストール

   ```bash
   yarn add react-firebaseui
   ```

2. ログイン画面の実装を行う。

   ```ts
   // Import FirebaseAuth and firebase.
   import React from "react";
   import StyledFirebaseAuth from "react-firebaseui/StyledFirebaseAuth";
   import firebase from "firebase/compat/app";
   import "firebase/compat/auth";

   // Configure Firebase.
   const config = {
     apiKey: "AIzaSyAeue-AsYu76MMQlTOM-KlbYBlusW9c1FM",
     authDomain: "myproject-1234.firebaseapp.com",
     // ...
   };
   firebase.initializeApp(config);

   // Configure FirebaseUI.
   const uiConfig = {
     // Popup signin flow rather than redirect flow.
     signInFlow: "popup",
     // Redirect to /signedIn after sign in is successful. Alternatively you can provide a callbacks.signInSuccess function.
     signInSuccessUrl: "/signedIn",
     // We will display Google and Facebook as auth providers.
     signInOptions: [
       firebase.auth.GoogleAuthProvider.PROVIDER_ID,
       firebase.auth.FacebookAuthProvider.PROVIDER_ID,
     ],
   };

   function SignInScreen() {
     return (
       <div>
         <h1>My App</h1>
         <p>Please sign-in:</p>
         <StyledFirebaseAuth
           uiConfig={uiConfig}
           firebaseAuth={firebase.auth()}
         />
       </div>
     );
   }

   export default SignInScreen;
   ```

3. Firebase コンソールから Authentication を選択し、ログイン方法を有効化する。

### デプロイ先ドメイン承認

以下のメッセージが表示され認証が通らない場合は、Firebase 側でデプロイ先ドメインを承認済みのドメインに追加する。

> Firebase: This domain is not authorized for OAuth operations for your Firebase project. Edit the list of authorized domains from the Firebase console. (auth/unauthorized-domain)

![](image/2022-03-27-16-34-29.png)

## Atomic Design

今回の Project のディレクトリ構造として以下の観点から Atomic Design を採用する。

1. コンポーネント開発を Storybook を用いて行うため、親和性が高い
1. コンポーネントの責務がより明確になる
1. 見た目の粒度だけでなく、ロジックの責務も明確にできる
1. 開発を進める中で、粒度が合わない場合は templates と organisms を統合/削除するなどして対応する。

### 参考

- [食べログでの Atomic Design 〜どう分類しているか編〜](https://note.com/tabelog_frontend/n/n4b8bcb44294c)
- [Atomic Design をやめてディレクトリ構造を見直した話](https://note.com/tabelog_frontend/n/n07b4077f5cf3)

## CSS in JS

### styled-components と css prop の違い

#### styled-components

- スタイルの適応されたコンポーネントを作成する。

#### css prop

- コンポーネントに css prop を記載してスタイリングを行う。

```ts
// styled-components の記法
export const StyledComponent: FC = () => {
  return (
    <Wrapper>
      <IconWrapper>
        <BellIcon />
      </IconWrapper>
      <MainText>お知らせ</MainText>
      <RightText>10件</RightText>
    </Wrapper>
  );

  const Wrapper = styled.p`
    background-color: #eee;
    font-size: 20px;
    padding: 15px;
  `;
};

// css propによる記法
export const CssProp: FC = () => {
  return (
    <div css={wrapperStyle}>
      <div css={iconWrapperStyle}>
        <BellIcon />
      </div>
      <div css={mainTextStyle}>お知らせ</div>
      <div css={rightTextStyle}>10件</div>
    </div>
  );

  const wrapperStyle = css({
    backgroundColor: "#eee",
    fontSize: "20px",
    padding: "15px",
  });
};
```

## Emotion

https://emotion.sh

- Atomic Design と親和性の高い CSS in JS を採用し、css props の使用できる Emotion を採用する。
- emotion/styled を import すると、styled-components の一部機能が使える
- MUIv5 の内部ライブラリとして採用されている

### Setup

1. インストール

   毎回、JSX Pragma を記載するのは面倒なため、babel-plugin を使用する。

   ```bash
   yarn add @emotion/react @emotion/babel-plugin
   ```

1. basel の設定

   1. next.js のトップディレクトリに.babelrc (babel の設定ファイル)を作成する。
   2. .babelrc にインストールした@emotion/babel-plugin を記載する。

   ```json
   {
     "presets": [
       [
         "next/babel",
         {
           "preset-react": {
             "runtime": "automatic",
             "importSource": "@emotion/react"
           }
         }
       ]
     ],
     "plugins": ["@emotion/babel-plugin"]
   }
   ```

1. 型定義ファイルの読み込み

   TypeScript で Emotion を使用する場合は型定義が必要なため、tsconfig.json 内に以下の記載を追記する。

   ```json
   {
     "compilerOptions": {
       "types": ["@emotion/react/types/css-prop"]
     }
   }
   ```

### 使用方法

1. @emorion/react の css 関数を inport する。

   ```ts
   import { css } from "@emotion/react";
   ```

1. css プロパティを記載する。

   ```ts
   // オブジェクト記法
   const testCss = css({
     color: "red",
   });

   // タグ付きテンプレート記法
   const testCss = css`
     coler: red;
   `;
   ```

   タグ付きテンプレート記法は普段の CSS の記法でそのまま記載できるが、シンタックスハイライトや静的解析が使えないためオブジェクト記法を使用する。

1. JSX のタグ内で css プロパティを指定する。

   ```ts
   return (
     <>
       <div css={testCss}>Login seccsess!!</div>
     </>
   );
   ```

### 参考

- [emotion を使うメリット](https://qiita.com/Sotq_17/items/91760691081db50b1f03)
- [【Next.js & TypeScript】Emotion の導入が大変だったので手順をまとめておく](https://zenn.dev/iwakin999/articles/7a5e11e62ba668)

## Material UI v5

https://mui.com

### Setup

<https://mui.com/guides/server-rendering/>
<https://github.com/mui/material-ui/tree/master/examples/nextjs-with-typescript>

1. インストール

   1. MUI のインストール

      ```bash
      yarn add @mui/material
      ```

   1. Emotion のインストール

      ```bash
      yarn add @emotion/react @emotion/styled @emotion/cache @emotion/server
      ```

      - 内部で Emotion を使用しているため、Emotion の install も必要となる。
      - styled-components にも対応しているが、今回はアプリ側でも CSS ライブラリとして Emotion を使用するため、デフォルトの Emotion を使用する。
      - @emotion/react @emotion/styled は Emotion 導入の際にインストール済みであれば不要。
      - SSR 構成の表示制御で使用するため @emotion/cache @emotion/server もインストールする。

   1. 必要であればマテリアルアイコンをインストールする。

      <https://mui.com/components/material-icons/>

      ```bash
      yarn add @mui/icons-material
      ```

2. src/lib/ に mui-theme.ts を作成し、サイト全体に適応する MUI テーマを設定する

   ```ts
   import { createTheme } from "@mui/material/styles";
   import { red } from "@mui/material/colors";

   const muiTheme = createTheme({
     palette: {
       primary: {
         main: red[400],
       },
       secondary: {
         main: red[200],
       },
       error: {
         main: red.A400,
       },
     },
   });

   export default muiTheme;
   ```

3. src/lib/に createEmotionCache.ts を作成し、キャッシュ周りの設定を記載する。

   ```ts
   import createCache from "@emotion/cache";

   // prepend: true moves MUI styles to the top of the <head> so they're loaded first.
   // It allows developers to easily override MUI styles with other styling solutions, like CSS modules.
   export default function createEmotionCache() {
     return createCache({ key: "css", prepend: true });
   }
   ```

4. src/pages/\_app.ts を編集する。

   ```ts
   import type { AppProps } from "next/app";
   import { useEffect } from "react";
   import { getAuth, onAuthStateChanged } from "firebase/auth";
   import { firebaseApp } from "@/libs/firebase/firebase";
   import * as React from "react";
   import Head from "next/head";
   import { ThemeProvider } from "@mui/material/styles";
   import CssBaseline from "@mui/material/CssBaseline";
   import { CacheProvider, EmotionCache } from "@emotion/react";
   import { muiTheme } from "@/libs/material-ui/mui-theme";
   import { createEmotionCache } from "@/libs/material-ui/createEmotionCache";

   // Client-side cache, shared for the whole session of the user in the browser.
   const clientSideEmotionCache = createEmotionCache();

   interface MyAppProps extends AppProps {
     emotionCache?: EmotionCache;
   }

   function MyApp(props: MyAppProps) {
     const {
       Component,
       emotionCache = clientSideEmotionCache,
       pageProps,
       router,
     } = props;
     useEffect(() => {
       const auth = getAuth(firebaseApp);
       onAuthStateChanged(auth, (user) => {
         if (!user) {
           router.push("/sign-in");
         }
       });
     }, [router.pathname]);

     return (
       <CacheProvider value={emotionCache}>
         <Head>
           <meta
             name="viewport"
             content="initial-scale=1, width=device-width"
           />
         </Head>
         <ThemeProvider theme={muiTheme}>
           {/* CssBaseline kickstart an elegant, consistent, and simple baseline to build upon. */}
           <CssBaseline />
           <Component {...pageProps} />
         </ThemeProvider>
       </CacheProvider>
     );
   }

   export default MyApp;
   ```

5. src/pages/\_document.tsx を作成し、サイト全体の HTML 出力関する設定と表示タイミングの制御を行う際のサーバサイド側の処理を記載する。

   ```ts
   import * as React from "react";
   import Document, { Html, Head, Main, NextScript } from "next/document";
   import createEmotionServer from "@emotion/server/create-instance";
   import { muiTheme } from "@/libs/material-ui/mui-theme";
   import { createEmotionCache } from "@/libs/material-ui/createEmotionCache";

   export default class MyDocument extends Document {
     render() {
       return (
         <Html lang="en">
           <Head>
             {/* PWA primary color */}
             <meta name="theme-color" content={muiTheme.palette.primary.main} />
             <link rel="shortcut icon" href="/static/favicon.ico" />
             <link
               rel="stylesheet"
               href="https://fonts.googleapis.com/css?family=Roboto:300,400,500,700&display=swap"
             />
             {/* Inject MUI styles first to match with the prepend: true configuration. */}
             {(this.props as any).emotionStyleTags}
           </Head>
           <body>
             <Main />
             <NextScript />
           </body>
         </Html>
       );
     }
   }

   // `getInitialProps` belongs to `_document` (instead of `_app`),
   // it's compatible with static-site generation (SSG).
   MyDocument.getInitialProps = async (ctx) => {
     // Resolution order
     //
     // On the server:
     // 1. app.getInitialProps
     // 2. page.getInitialProps
     // 3. document.getInitialProps
     // 4. app.render
     // 5. page.render
     // 6. document.render
     //
     // On the server with error:
     // 1. document.getInitialProps
     // 2. app.render
     // 3. page.render
     // 4. document.render
     //
     // On the client
     // 1. app.getInitialProps
     // 2. page.getInitialProps
     // 3. app.render
     // 4. page.render

     const originalRenderPage = ctx.renderPage;

     // You can consider sharing the same emotion cache between all the SSR requests to speed up performance.
     // However, be aware that it can have global side effects.
     const cache = createEmotionCache();
     const { extractCriticalToChunks } = createEmotionServer(cache);

     ctx.renderPage = () =>
       originalRenderPage({
         enhanceApp: (App: any) =>
           function EnhanceApp(props) {
             return <App emotionCache={cache} {...props} />;
           },
       });

     const initialProps = await Document.getInitialProps(ctx);
     // This is important. It prevents emotion to render invalid HTML.
     // See https://github.com/mui/material-ui/issues/26561#issuecomment-855286153
     const emotionStyles = extractCriticalToChunks(initialProps.html);
     const emotionStyleTags = emotionStyles.styles.map((style) => (
       <style
         data-emotion={`${style.key} ${style.ids.join(" ")}`}
         key={style.key}
         // eslint-disable-next-line react/no-danger
         dangerouslySetInnerHTML={{ __html: style.css }}
       />
     ));

     return {
       ...initialProps,
       emotionStyleTags,
     };
   };
   ```

### 参考

- [Next.js に Material UI を組み込んだ環境を作る](https://zenn.dev/ttani/articles/next-materialui-setup)
- [Next.js に新しくなった MUI(Material-UI v5)と Emotion を導入して新機能を試す](https://zuma-lab.com/posts/next-mui-emotion-settings)

### 使い方

css props のオブジェクト記法でスタイルを記載する場合は、@mui/material/\*\*にスタイルのプロパティが定義されており、JSDoc にサンプルも記載されているので参考にしながら記載する。

![@mui/material/colorsのJSDoc](image/2022-02-19-23-54-49.png)

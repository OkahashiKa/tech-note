# Learn07 TypeScript から外部ライブラリにアクセスする

## P3 　モジュール コンポーネントをエクスポートおよびインポートする

- export には named ecport と default export があり、諸説あるが基本的には named export が推奨されている。

  ```ts
  export function returnGreeting(greeting: string) {
    let greetingLength = getLength(greeting);
    console.log(
      `The message from GreetingsLength_module is ${greeting}. It is ${greetingLength} characters long.`
    );
  }

  // @note: このモジュール内でしか使わない場合は、privateでよいのでは？
  function getLength(message: string): number {
    return message.length;
  }
  ```

## P5 外部タイプ ライブラリにアクセスする

- dependencies は本番用のパッケージを記載、devDependencies は開発用のパッケージを記載している。

  ```bash
  ## dependenciesに追加だが、現在はデフォルトでdependenciesに追加されるため不要
  npm i -save

  ## devDependenciesに追加する
  npm i --save-dev
  ```

## P6 モジュール コンポーネントをエクスポートおよびインポートする

- named export されているものを複数 inport する際は \* as よりも{}内に複数記載することが多い。

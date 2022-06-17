# PlantUML

テキストベースでユースケース図、シーケンス図、ER図などのUMLが記載できるため、UMLをGit管理することができる。
VSCodeの拡張機能としても存在するため使い勝手が良い。

## Install

1. install graphviz
    PlantUMLはdot言語で記載されている、グラフ構造を任意の画像フォーマットに変換するgraphvizというツールを使用しているため、graphvizをインストールする。

    ``` bash
    brew install graphviz
    ```

2. install JDK
    PlantUMLはJava実行環境で動作しているため、JDKをインストールする。

    ``` bash
    brew install adoptopenjdk --cask 
    ```

3. install plantuml
    ようやく本体インストール。

    ``` bash
    brew install plantuml
    ```

## PlantUML for VSCode

PlantUMLのVSCode拡張機能。

- [PlantUML - Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=jebbs.plantuml)

## Markdown Preview Enhanced

mdの中に埋め込まれたPlantUMLをプレビュー表示できるようになる拡張機能。
PlantUMLを埋め込む際は、以下のようにコードブロックとして挿入する。

``` plantuml
@startuml
entity Entity01 {
    * identifying_attribute
    --
    * mandatory_attribute
    optional_attribute
}
@enduml
```

- [Markdown Preview Enhanced - Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=shd101wyy.markdown-preview-enhanced)

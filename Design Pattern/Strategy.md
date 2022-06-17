# Strategy Puttern

Strategy Putternはアルゴリズム部分を意図的に他のソースから隔離することで、実行時にアルゴリズムを選択できる。
またアルゴリズムを修正する際も他の部分への影響が少ない。
アプリケーションで使用されるアルゴリズムを動的に切り替える必要がある際に有用である。
Strategyパターンは、Strategy（抽象戦略）とConcreteStrategy（具体戦略）とContext（文脈）の３つで構成されています。

## Reference

- [デザインパターン ～Strategy～](https://qiita.com/i-tanaka730/items/4d00c884b7ce1594f42a)
  - じゃんけんで分かりやすい

# LINQ

## LINQ to Entities

- LINQ to Entities はメソッドの使用できない式ツリーに変換を行うため拡張メソッドは使用できない。
  - 回避策としては AsEnumerable()や ToList()を用いてローカルで編集可能な値に変換する必要がある。

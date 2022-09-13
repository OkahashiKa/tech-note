# LINQ

## LINQ to Entities

- LINQ to SQL が SQLServeer のデータ操作を行うのに対して、LINQ to Entities はその他の DB に対してもデータ操作が行える。
- LINQ to Entities はメソッドの使用できない式ツリーに変換を行うため拡張メソッドは使用できない。
  - 回避策としては AsEnumerable()や ToList()を用いてローカルで編集可能な値に変換する必要がある。

## エンティティの状態

エンティティの状態には，Unchanged, Added, Deleted, Detached, Modified という 5 つの状態が存在します． それぞれの状態の意味は以下の通りです．

- Unchanged 状態
  - DB にデータが存在していて，全く更新が加えられてないときの状態です． DB のデータが Context にアタッチされた（読み出された）直後や，SaveChanges 直後は Unchanged 状態になります．
- Added 状態
  - Context に Entity がトラッキングされた状態で，かつ DB にデータが存在しない場合は Added 状態になります． SaveChanges を呼び出すと，DB には Added 状態の Entity の Insert 文が発行されます． SaveChanegs を呼び出した後は Unchanged 状態になります．
- Deleted 状態
  - DB にデータが存在していて，これから削除しようとしている場合は Deleted 状態となります． SaveChanges を呼び出すと，DELETE 文が DB に対して発行されます． その後，Entity は Detached 状態になります．
- Detached 状態
  - Detached 状態は，オブジェクトは存在しているけれど，DbContext によって状態がトラッキングされていない状態です．
- Modified 状態
  - Modified はオブジェクトのプロパティの一部が変更されていて，まだ SaveChanges が呼び出されていない状態です． SaveChanges を呼び出すと，UPDATE 文が DB に対して発行されます． SaveChanges を呼び出した後は Unchanged 状態になります．

## Remove

LINQ to Entitties でデータ削除を行う場合は対象のエンティティを取得したのち Remove で削除を行う。
Remove を実行した時点では、DB のレコードは削除されず、SaveChanges をおこなった時点で DELETE 分が DB に対して実行される。

```C#
var deleteUser = _context.User
  .Where(x => x.Id == user.Id)
  .FirstOrDefault();

_context.User.Remove(deleteUser);
_context.SaveChanges();
```

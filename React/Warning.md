# warning

## Input 要素の Value が State で管理されていない

表示 warning

```bash
Warning: Select elements must be either controlled or uncontrolled (specify either the value prop, or the defaultValue prop, but not both). Decide between using a controlled or uncontrolled select element and remove one of these props. More info:
```

### 解決法

Input 要素の Value の参照を State にし、change イベントで setState してあげるように修正する。

# React Hook

## useEffect

- useRouter().query.id の取得よりも useEffect()が先に実行されるため。useEffect 内でクエリパラメータを取得したい場合は、以下のように実装する。

```tsx
const router useRouter();
useEffect(() => {
if(router.isReady){
    const query = router.query.id;
}
}, [query, router])
```

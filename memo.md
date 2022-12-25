# Docker 　コンテナ内で Next から Nest の API にアクセスする

```yml:docker-compose.yml
version: "3"
services:
  backend:
    hostname: api #const res = await axios.get('http://api:3000/api/endpoint');
```

とすることで Next の getServerSideProps からアクセスできる

```ts
export const getServerSideProps: GetServerSideProps<Props> = async () => {
  const res = await fetch("http://api:4000");
  const a = await res.text();
  console.log(a, "in getServerSideProps");
  return {
    props: { text: a },
  };
};
```

なお`useEffect`からは以下のようにアクセスする。

```ts
useEffect(() => {
  const main = async () => {
    const res = await fetch("http://localhost:4000");
    const a = await res.text();
    console.log(a, "in useEffect");
  };
  main();
}, []);
```

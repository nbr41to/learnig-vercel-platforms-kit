# Vercel の Platforms Starter Kit をさわる

ついでに Nextjs UI もさわりたい

[document](https://vercel.com/guides/nextjs-multi-tenant-application)

## Clone する

```
npx create-next-app --example https://github.com/vercel/platforms/tree/main [project-name]
```

## PlanetScale の準備

1. アカウントの作成
   GitHub のアカウントで作成
2. データベースの作成
   `platforms`という名前で作成
3. データベースの設定を変更
   `Automatically copy migration data`を`Prisma`に変更
4. データベースの branch を作成
   `staging`と`shadow`を`main`から作成
5. それぞれ起動
   `pscale connect platforms main --port 3309`
   `pscale connect platforms main --port 3310`

## データテーブルの作成

`.env.sample`をコピーして`.env`を作成

```
npx prisma migrate dev --name init
```

app.localhost:3000 にアクセスするとログインページがある

planetScale で main branch を`Promote to production branch`を実行しておく

```
pscale deploy-request create platforms staging
```

## Next Auth の設定

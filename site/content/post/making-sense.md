---
title: Netlify memo
date: 07/10/2017 7:04 AM
description: This is a memo for myself.
image: /img/スクリーンショット%202017-07-09%2017.28.36.png
---
静的サイトHostingサービス。

- 無料でもけっこう機能もりもり
- ハイパフォーマンス
- HTTPSもいける
- CDN(cloudfront)
- 別ブランチをサブドメインに割り当てられる
- アクセス制御もできる（無料では出来ない

tsukuruba 産の静的サイトにも使えるんじゃないか？と思ったりしつつ、
とりあえず個人趣味的に試してみた記録。

## Pricing

<https://www.netlify.com/pricing/>

Bronze(Free) < Silver < Gold < Platinum

けっこう無料で出来ちゃう。ありがたいが、大丈夫か。
$2.1M も出資受けてるから大丈夫か、そのうち値上がりするのかも。
<https://techcrunch.com/2016/08/17/netlify-a-sevice-for-quickly-rolling-out-static-websites-raises-2-1m/>

## Domain

最初は、Project 単位で、`dermatologist-monkey-67732` とか謎のコードが割り振られ、
`dermatologist-monkey-67732.netlify.com` になるが、コードを変更することも出来るし、
カスタムドメインにすることも可能。（無料でおｋ
https://in-progress.work/

カスタムドメインじゃなければ↓
https://dermatologist-monkey-67732.netlify.com/

### Branches
ブランチに対して、サブドメインをマッピング可能。
https://develop.in-progress.work/
↑developブランチ

https://develop--dermatologist-monkey-67732.netlify.com/


## Env

`netlify.toml` という設定ファイルを通じて（or  管理画面でぽちぽち）変数を渡せる。

```toml
[build]
  command = "npm run build"
  publish = "public"

[context.production.environment]
  NODE_ENV = "production"

[context.deploy-preview.environment]
  NODE_ENV = "development"
```

なので、develop ではログを吐くけど、production ではビルドで消す、とか可能。

## HTTPS

ボタンを押してぼんやりしていれば、Let's Encrypt による HTTPS 化がなされる。
HTTP/2 もサポートしているが、CDN経由のAssetファイルへの対応はまだ実験中っぽい。
連絡するとテスト対象にしてくれる雰囲気はある。

## Deploys
- GitHub プッシュで自動デプロイが標準
- Test 通ったらデプロイ、したければ、恐らく `netlify-cli` を使えばいける
- `dermatologist-monkey-67732.netlify.com` にはなるが、いろんなブランチ単位でデプロイされる

### 例: favicon ブランチ

特にサブドメインを設定していないが、カスタムドメインじゃない方で確認可能。
https://deploy-preview-2--dermatologist-monkey-67732.netlify.com/

## Notifications

管理画面での通知設定。
![image](https://user-images.githubusercontent.com/2628239/27992414-325cdf56-64cf-11e7-85b7-8078a4b8ba30.png)

Slack
<https://api.netlify.com/build_hooks/5961ed328ebdd92e25252f40>

Slack に通知される様子。
![image](https://user-images.githubusercontent.com/2628239/27992612-cb866e64-64d3-11e7-80f9-2e4f21656795.png)


## Access Control 

Password での制御と、 Role-based の制御があるが、
どちらも、Bronze ではできない。

Password プロテクションは Silver Plan から。  
<https://www.netlify.com/docs/visitor-access-control/#password-protection>

Role-based  は、Gold Plan から。  
<https://www.netlify.com/docs/visitor-access-control/#role-based-access-controls-with-jwt-tokens>

## Prerendering

[prerender.io](https://prerender.io/) を利用して、SPA の pre-rendering してくれるらしい。
試してはいない。

## CMS
[Netlify CMS](https://github.com/netlify/netlify-cms) なるものがある。試してない。

## 余談

- 大した中身ではないが、[ITS 検診機関一覧](http://www.its-kenpo.or.jp/kanri/keiyaku/ichiran/)の地図View である
- `in-progress.work` のドメインは 10円だった



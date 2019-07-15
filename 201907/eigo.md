# @eigobluesnow

## 軽い自己紹介
どうも、@eigobluesnowです。TwitterIDも同じです。
普段は自社のバックエンドサービス開発のPMをやっています。
経歴としてはこんな感じです。
Javaエンジニア
↓
色々エンジニア（VC++、VB、CakePHP1.3、2.3）
↓
Androidエンジニア
↓
iOS/Android開発PM
↓
Web開発PM（今ここ）

もくもく温泉は第6回くらいから参加しており、今回15回目なので、9回目くらいかなって感じです。


## 今回やること
今の仕事が6年ぶりのPHP、フレームワークがLaravelなので、改めてLaravel開発をイチから勉強しています。
今回は同僚から勧めらたLaravelの青い本を写経しています。
https://www.amazon.co.jp/dp/4798052582/ref=cm_sw_r_tw_dp_U_x_0NPkDbRQTX87B

写経をするにあたり、開発環境はDockerで構築しています。
docker-compose.ymlはこんな感じです。

```docker-compose.yml
version: '3'

services:
  php:
    container_name: php
    build: ./docker/php
    volumes:
    - ./server:/var/www

  nginx:
    image: nginx
    container_name: nginx
    ports:
    - 80:80
    volumes:
    - ./server:/var/www
    - ./docker/nginx/default.conf:/etc/nginx/conf.d/default.conf
    depends_on:
    - php

  db:
    image: mysql:5.7
    container_name: db-host
    environment:
      MYSQL_ROOT_PASSWORD: ****
      MYSQL_DATABASE: database
      MYSQL_USER: ****
      MYSQL_PASSWORD: ****
      TZ: 'Asia/Tokyo'
    command: mysqld --character-set-server=utf8mb4 --collation-server=utf8mb4_unicode_ci
    volumes:
    - ./docker/db/data:/var/lib/mysql
    - ./docker/db/my.cnf:/etc/mysql/conf.d/my.cnf
    - ./docker/db/sql:/docker-entrypoint-initdb.d
    ports:
    - 3306:3306
```

もともとChapter4まで進めており、今回はChapter5から進めます。
Chapter5からいよいよDBに繋いでテーブルからレコードを取って画面に表示するフェーズになります。

## 今回の成果
### Dockerがちょっとわかった。
Dockerでちょっとハマりました。
LavavelではDBの設定をconfig/database.phpと.envにそれぞれ定義するのですが、
.env のDB_HOSTにdockerのサービス名を定義しなければならないのがわからなかったです。
私の場合は、'''DB_HOST=db'''でした。

### 写経をGit導入してPR運用してみたら、PR駆動開発になって楽しかった。
実は今までプライベートでもGitを使うことはあんまりなかったのですが、今回写経でもGit管理してみることにしました。
というのも、写経をやっていると書いたコードを修正しなければならないことが多かったのでちょっともったいなかったのと、
記録をつけないと今までやってみたことが身につかないと感じていたので、今回写経コードもGit管理してみました。

やってみるとバシバシ書いてバシバシPR出しバシバシapproveするので結構それが楽しく感じました。
写経する時もGit運用するのおすすめです。

## 今回のもくもく会
伊東に初めてマイカーで来ました。
３連休は流石に熱海周辺が大渋滞していたので、小田原厚木道路→箱根新道→伊豆スカイラインで来ました。
霧で前が見えなかったのでヒヤヒヤでした^^;

着いてからほぼ旅館にこもって開発していたので、伊東の写真は特にないです。
スミマセン。。。

最後に旅館で取った写真をあげて終わりにしたいと思います。
ありがとうございました。

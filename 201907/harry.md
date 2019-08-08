# Just Do It
2019/7/14

## やることチェックリスト  
-[x] 報告が来たバグの修正
-[x] ずっと解決できていないApacheの修正

## 報告が来たバグの修正
- MongoDBに、ブランクのデータが挿入される  
csvでデータを投入するよう設定していたので、ブランクのデータを事前に削除して解決
- MongoDBから取得するデータが、ソートされていない  
mongooseでデータを取得する際、ソートキーを指定して解決  

before
```javascript
Model.find({})
```
after
```javascript
Model.find({}, {}, { sort: { sort_key: 1 } })
```
[参考](https://qiita.com/n0bisuke/items/6db3ca0bc4fb7fcbd442)

## ずっと解決できなかったApacheの修正
### 目的
VueのSPAで構築した静的ファイルがあり、それをapacheにて配信したい  
- 配信はサブディレクトリで行う
- SPAにてルーティングを行いたい

### 問題
.htaccessにてルーティングをさせたいが、キャッチできない

### 解決
以下のように.htaccessを設定することで解決
```.htaccess
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteBase /sub_dir
RewriteRule (.*) index.html [L,QSA]
```

- RewriteBaseにてサブディレクトリ配信の設定をする
- RewriteRuleにて、全てのアクセスをindex.htmlに飛ばすよう設定

### 参考
- [静的なサイトに JavaScript のルーターを導入する](https://qiita.com/masakielastic/items/2d43829edbac51ea366c)

### 謝辞
ほぼほぼ、[なかひこ君](https://twitter.com/takanakahiko)に助けてもらいました！  
まじでありがとう！！！！！

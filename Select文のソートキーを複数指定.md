# Select文のソートキーを複数指定する

これは正解できた。

```
select
distinct
count(id) as count_products_types,
producer
from products
group by producer
order by count_products_types DESC, producer ASC
```

order by による並べ替えは2種類のカラムを指定して実行することができる。
2つのカラムをキーにして並べ替えを実行するとどうなるのか？

![image](https://user-images.githubusercontent.com/18514297/90946517-878b3380-e468-11ea-8c90-848a002dfb85.png)

https://dev.grapecity.co.jp/support/powernews/column/how_to_database/006/page02.htm

上記によると、最初に指定したソートキーで並べ替えを実行後、次のソートキーで並べ替えを行う処理になるようだ。

![image](https://user-images.githubusercontent.com/18514297/90946577-1d26c300-e469-11ea-8ffc-07f0168273a6.png)


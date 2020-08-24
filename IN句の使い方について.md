# IN句の使い方2選

本日の問題はこちら。

![image](https://user-images.githubusercontent.com/18514297/91058779-d81ab080-e663-11ea-8a67-7d79f348c649.png)

そして、正解はこちらのコードになる。

```
select
id,
name
from departments
where id in
(
  select
  department_id
  from sales
  where price >= 98
)
```

![image](https://user-images.githubusercontent.com/18514297/91058945-0ef0c680-e664-11ea-9952-ef91706540b3.png)

回答を導き出すのに参考になったサイトは以下になる。

https://qiita.com/ponsuke0531/items/fdfa8a4b1df8715917cb

要はWhere句の発展形で、列に対して行うフィルター条件の詳細な指定方法である。
主な指定の仕方は以下の2点となる。

１．列に値を直接指定する

```
select * from {テーブル名} where {列名} IN ({値1}[, {値n}...]);
```

```
例：select * from country where country in ('Japan','Zambia');
```

こうすることで通常は1つのカラムに1つの条件しか設定できないところ、複数の条件を指定することができるようになる。


２．値を副問合せで指定

直接の指定からの発展形で副問合せを利用して、条件を指定することが可能。

```
select * from {テーブル名1} where {列名} IN (select {列名1にヒットさせたい列名2} from {テーブル名2} [where ...]);
```

要は覚えるべき構文は Where ～ in ～といったところである。
今回の正解パターンは後者の副問合せで値を指定するパターンとなる。


ちなみに、応用として、複数のカラムに複数の条件を指定するといったことも可能らしい。

```
select * from country where (country_id,country) in ((50,'Japan'),(110,'Zambia'));
```

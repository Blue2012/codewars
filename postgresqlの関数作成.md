# 3つの引数を与えて割り切れるかどうかをチェックするpostgresqlで関数を作成する

まず、こんな問題だった。

![image](https://user-images.githubusercontent.com/18514297/90948903-4dc52780-e47e-11ea-8222-8184a0746c18.png)

で、以下のコードで正解となった。

```
CREATE OR REPLACE FUNCTION check_numbers(n INTEGER,x INTEGER,y INTEGER) RETURNS BOOLEAN AS $$
DECLARE
BEGIN
IF (n % x) = '0' and (n % y) = '0' THEN
RETURN 'true';
ELSE
RETURN 'false';
END IF;
RETURN 0;
END;
$$ LANGUAGE plpgsql;

select
id,
check_numbers(n,x,y) as res
from kata
```

分かったことと、ポイントを以下に列記する。

１．上から下に処理が流れるので、Select文内で自分で作成した関数を利用する場合、上に定義を記載する必要がある
　　※でないとエラーが発生する

![image](https://user-images.githubusercontent.com/18514297/90948935-bdd3ad80-e47e-11ea-91a8-aa2daa82dc9d.png)

２．関数の書式

どうやら、以下が決まりのよう。※日本語にしている部分以外、すべて定型文（書式）となる。

CREATE OR REPLACE FUNCTION 関数名(引数名1 データ型,引数名2 データ型,引数名3 データ型,…) RETURNS 戻り値のデータ型 AS $$
DECLARE
BEGIN
＜処理の内容＞
END IF;
RETURN 0;
END;
$$ LANGUAGE plpgsql;

逆に言うと、日本語の部分だけ変更すれば良いってこと。
RETURNというのは処理を終了して、指定した値を返すという役目を持っているらしい。

https://www.postgresql.jp/document/9.1/html/plpgsql-control-structures.html

BEGINとENDは間違いなく、処理部分を定義するために利用している（処理の開始、終了の定義）

３．今回の問題について

今回の問題は変数nが変数x,yで割り切れる場合は「true」、割り切れない場合は「false」を返せって問題。
割り切れるかどうかの条件は定石で「剰余の値が0」っていうことになるので。

```
IF (n % x) = '0' and (n % y) = '0' THEN
```

上記の処理を入れて、それ以外はelseに突っ込んで、return句でfalseを返すって形で書いてみたら、正解となった。

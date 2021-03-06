# PHPのおさらい

## echo

### PHPの書き方


PHPはHTMLに埋め込んで使う。`<?php 〜 ?>`の中にPHPの命令を書いていく。`<?php 〜 ?>`の部分がHTMlに変換された上で表示される。


### PHPの文法


PHPでは文末にセミコロン「;」を使って文を区切る。セミコロンを忘れるとエラーが起きるので注意する。また、「//」から行末まではコメントになる。動作には関係しない情報で、主にメモなどに用いる。




```php:index.php
<?php
  // この行はコメントです
  echo 'こんにちは';
  echo 'PHPを学ぼう';
?>
```




### 文字列の出力


「echo」は文字列などを出力するための命令。文字列を出力する場合はシングルクォーテーション「\`」かダブルクォーテーション「\"」で囲む。


```php:index.php
<?php echo 'Hello, World!'; ?>
```


結果

    Hello, World!


### 計算をする


PHPも一般的なプログラミング言語と同じように計算させることができる。足し算は「\+」、引き算は「\-」、掛け算は「\*」、割り算は「\/」で表す。PHPでは割り算の余りを計算することもでき、「\%」で表す。


```php:index.php
echo 7 + 3;   //結果：10
echo 10 - 4;   //結果：6
echo 3 * 6;   //結果：18
echo 9 / 3;   //結果：3
echo 5 % 2;   //結果：1
```


## データの種類

### データの種類


PHPには、「文字列」や「数値」等のデータがある。「'Hello'」「'a'」などは文字列、「1」「3.14」などは数値となる。


## if文

### if文

if文を使うと、条件に応じて処理を分岐することができる。if文は以下のように書くことができる。条件が成り立つ場合、{}の中の処理が実行される。条件が成り立たない場合は処理が実行されない。



```php:index.php
<?php

$x = 20;
if($x > 10){
  echo '$xは10より大きい';
}

?>
```


結果

    $xは10より大きい


```php:index.php
<?php

$x = 20;
if($x > 30){
  echo '$xは10より大きい';
}

?>
```


結果

                  （← ※条件式が成り立たないため処理が実行されない）





### if文と真偽値


比較演算子を用いて比較した結果はtrueかfalseになる。trueとfalseは真偽値と呼ばれる。真偽値は文字列や数値といったデータの種類の1つである。真偽値はtrueとfalseの2つしかない。if文は、条件式がtrueの場合if文の中身が実行され、falseの場合は実行されない。



```php:index.php
<?php

if(true){
  echo '条件は true です';
}

?>

//結果：条件は　true　です。
```


```php:index.php
<?php
$x = 20;
if($x > 30){
  echo '$xは30より大きい';
}
 // ↑処理は実行されない
if($x > 10){
  echo '$xは10より大きい';
}
 // ↑処理が実行される
?>
```

### else, elseif文

#### else


ifと組み合わせてelseを使うと、「もし〜だったら・・・、そうでなければ・・・」といった条件分岐が可能になる。if文の条件が「false」であった場合、elseの中の処理が実行される。


```php:index.php
<?php
$x = 20;
if($x == 30){
  echo '$xは30です';
  // ↑処理は実行されない
}else{
  echo '$xは30ではありません';
}
 // ↑処理が実行される
?>
```


### \&\&, ||

#### 複数の条件式を組み合わせる


「\&\&」「||」は論理演算子と呼ばれ、複数の条件を1つにまとめるときに使う。\&\&（かつ）は左右の四季がともに「true」の場合、全体も「true」になりる。||（または）は左右の四季のどちらか、または両方が「true」の場合、全体も「true」になる。



```php:index.php
<php?
$x = 20;
if ($x > 10 && $x < 30){
  echo '$xは10よりおおきい、かつ30より小さい';
}
if ($x < 10$ || $x >30){
  echo '$xは10より小さい、または30より大きい';
}
//  結果：$xは10より大きい、かつ30より小さい
?>
```


#### 条件の否定

「!」も論理演算子の1つであり、条件の否定ができる。式が「真」であれば「偽」に、「偽」であれば「真」になる。


```php:index.php
<?php
  $x = 20;
  if (!($x == 30)){
    echo '$xは30ではない';
  }
//結果：$xは30ではない
?>
```


### switch文

#### switch文

if, elseifによる分岐が多く複雑な場合、switch文で書き換えるとシンプルで読みやすいコードにでる。switch(式)の(式)がcaseの値と一致したとき、そのブロックが実行。caseのどれにも一致しなかった時、defaultのブロックが実行される。


if文を用いた条件分岐


```php:index.php
<?php
  if ($coin == 0){
    echo '表';
  }elseif ($coin == 1){
    echo '裏';
  }else {
    echo 'エラー';
}
?>
```

switch文を用いた条件分岐


```php:index.php
<?php
  switch ($coin){
  case 0:
    echo '表';
    break;
  case 1:
    echo '裏';
    break;
  default:
    echo 'エラー';
    break;
}
?>
```


#### switch文 \- break

caseブロックの最後にはbreak命令を指定する。break命令は現在のブロックから脱出するための命令である。break命令がないと、後ろに続くcaseブロックが続けて実行されてしまう。


```php:index.php
<?php
  //$coin == 0 のとき
  
  switch ($coin){
  case 0:
    echo '表'; // 実行される
              // ←break命令がない 
  case 1:
    echo '裏'; // 実行される
    break;
  default:
    echo 'エラー';
    break;
}
// 結果：表裏
// ↑break命令がないため、条件が成立しない。次のcaseブロックも実行されてしまう。
?>
```



### 配列

#### 配列とは？


これまでの変数が一つしか値を扱えなかったのに対し、配列を用いると複数の値をまとめて保存することができる。配列は仕切りのある箱のようなもので、それぞれのスペースにデータが入っており、0, 1, 2...というインデックス番号によってスペースの名前が付けられている。


#### 配列の操作

配列の基本構文は「$配列名 = array(値１, 値2, ・・・);」のようになっている。配列のデータには先頭から0, 1, 2, ・・・と順に「インデックス番号」が割り振られていき、配列のデータを取り出すには「インデックス番号」を用いて $配列名\[インデックス番号\] といった具合で記述する。


配列の定義の仕方

```php:index.php
<?php
  $names = array('John','Kate','Bob');
// インデックス# [0] [1] [2]
?>
```


配列の取り出し方

```php:index.php
<?php
echo $names[0];
// 結果：John

echo $names[1];
// 結果：Kate
?>
```

#### 値の追加、上書き


配列の末尾に値を追加するときは「$配列名\[\] = 値;」とする。また、すでに存在するインデックス番号を指定すると、配列の値を上書きすることもできる。


```php:index.php
<?php
$names = $array('John','Kate','Bob');

$names[] = 'Mary';  // ←配列の末尾に値を追加

echo $names[3]; //結果：Mary

$names[1] = 'Jane'  //←値の上書き

echo $names[1]; //結果：Jane
?>

```


### 連想配列

#### 連想配列の操作


連想配列は、配列と同じく複数のデータをまとめて管理するのに用いられる。配列との違いは、個々の要素を管理するのにインデックス番号ではなく、「キー」と呼ばれる文字列などの値を指定することができる点である。  
連想配列では「$配列名 = array('キー名' => '値１', ・・・);」といったように、「=>」を用いてキーと値をセットする。


```php:index.php
<?php 
$user = array{
//↑連想配列名
        'name' => 'わんこ',
        'age' => 14,
        'gender' => 'male'
        //↑キー       ↑値
};
?>

```


連想配列の値を取り出すには、対応する「キー」を用いて 「配列名\[キー\] 」のようにする。  
「配列名\[キー\] = 値;」のようにすることで、連想配列にデータを追加することができる。



連想配列／値の取り出し方
```php:index.php
<?php 
$user = array(
        'name' => 'わんこ',
        'age' => 14,
        );
echo $user['name']; //結果：わんこ
?>
```


連想配列／値の追加方法

```php:index.php
<?php 
$user['level'] = 'beginner';
//    ↑追加するキー   ↑追加する値
?>

```


### for文
#### 繰り返し処理


1から100までの数値を出力するときのように、繰り返しで何かを行いたいときには繰り返し文を用いる。  繰り返し文を使うことで、繰り返しの処理（ループ処理）を以下のようにたった数行で書くことが可能。


１〜１００まで出力したい場合
```php:index.php
<?php 
echo 1;
echo 2;
echo 3;

//   ︙

echo 100;
?>
```


for文を使った繰り返し処理

```php:index.php
<?php 
for ($i = 1; $i <= 100; $i++){
 echo $i;
}
?>
```

#### for文
for文を用いることで繰り返し処理を行うことができる。以下では、変数\$iに1を初期値として与え、「echo \$i;」を行っている。その後はループの条件を満たさなくなるまで値の更新「$i++」と、「echo $i;」を繰り返し行う。


for文を使った繰り返し処理
```php:index.php
<?php 
//    ①初期化 ②ループの条件 ④変数の更新
for ($i = 1; $i <= 100; $i++){
 echo $i;
//③繰り返し処理
}
?>

```

繰り返し処理の流れ
```
　 ①変数の初期化
　  ↓
┌ →②ループの条件
│ 　↓
↑ 　③繰り返す処理
│ 　↓
└ ←④変数の更新

```



### while文

#### while文とは


while文もfor文と同様に、繰り返し処理の一つ。  
条件式を指定し、それがtrueの間、処理が繰り返し実行される。  
for文の時のように変数\$iが自動的に増えていかないため、ここではループのたびに「\$i ++;」を行っている。

while文を使った繰り返し処理

```php:index.php
<?php
$i = 1; //①初期化
while ($i <= 100){  //②ループの条件
echo $i;  //③繰り返す処理
$i++  //④変数の更新
}

?>

```


繰り返し処理の流れ
```
　 ①変数の初期化
　  ↓
┌ →②ループの条件
│ 　↓
↑ 　③繰り返す処理
│ 　↓
└ ←④変数の更新

```


#### 無限ループ

無限ループは条件式が何周してもtrueのままで、永遠に終了しないループのことを指す。無限ループはコンピューターに極端な負担を与えてしまうため、ループ処理を記述する際は条件式がどこかでfalseになるように気をつけなければならない。


無限ループ

```php:index.php
<?php
$i = 1;
while ($i <= 100){  
//条件式が常にtrueになるため、無限にループが続く
echo $i;

}

?>
```


### break文

#### break文とは

break文は現在のループを強制的に中断する命令である。for, while, foreachなどの繰り返し文の中で利用でき、break文はif文などの条件文と組み合わせて利用するのが一般的。


break文 - ループを強制的に中断する


```php:index.php
<?php
for ($i = 1; $i <= 10; $i++){
  if($i > 5){
   break;
   }
  echo $i;
}
//結果：12345
?>
```




### continue文

#### continue とは

ループそのものを完全に抜けてしまうbreak文に対して、continue文は現在の周だけをスキップし、ループそのものは継続して実行する。  
continue文もfor, while, foreachなどの繰り返し文の中で利用可能。


continue文 - 現在のループをスキップ



```php:index.php
<?php
for ($i = 1; $i <= 10; $i++){
  if($i % 3 == 0){  //$iの値が３の倍数の時、その周のループを終了し、次のループを実行
   continue;
   }
  echo $i;
}
//結果：124547810（3の倍数以外）
?>
```



### foreach文

#### foreach文とは


foreach文とは、配列または連想配列に対して、先頭のデータから順に繰り返し処理を行うための命令である。  
以下のように配列のデータを１つずつ取り出して処理を行うことが出来る。  
「as」の後ろの変数に、ループの度にデータが先頭から順に代入されていく。



```php:index.php
<?php
$data = array('東京','大阪','京都');
//            1回目  2回目  3回目
foreach ($data as $value) {
  echo $value;
}
//結果：東京 大阪 京都
?>
```


#### foreachの書き方（１）


foreach文では、配列内のデータが順次「キー変数」、「値変数」に代入され、それに対して処理が繰り返し適用される。  
「キー変数」には、配列のときはインデックス番号が、連想配列のときはキーが代入される。  
ただし、「キー変数」の部分は省略可能。

```php:index.php
<?php
foreach (配列または連想配列 as 値変数) {
  繰り返したい処理 ;
}
foreach (配列または連想配列 as キー変数 => 値変数) {
  繰り返したい処理 ;
}

?>
```


#### foreachの書き方（２） 


foreach文は理解しにくいので少し例を見てみることとする。 図の配列は、果物の名前を「キー」として、その色を「値」として保持している連想配列である。 

1周目のループでは\$keyに'Apple'、\$valueに'Red'が、２周目のループでは\$keyに'Banana'、\$valueに'Yellow'が入っている。


```php:index.php
<?php
$colors = array(
            'Apple' => 'Red', //１周目のループでは、
            'Banana' => 'Yellow', //$key = 'Apple'
            'Grape' => 'Purple' //$value = 'Red'となる
              );
foreach ($colors as $key => $value) {
  echo $key,':',$value;
}
//結果Apple:Red Banana:Yellow Grape:Purple
?>
```


### 関数
#### 関数の使い方
関数とは、あるまとまった処理を行い、値を返すものである。 PHPには便利な関数がもとから組み込まれていて、それらは組み込み関数と呼ばれる。  
「strlen」は組み込み関数の1つで、文字列の文字数を返す。  
ここで、()の中に与える値を「引数」という。


```php:index.php
<?php

echo strlen('PhpPlactice');

//結果：11
?>
```



```php:index.php
<?php
$language = 'PHP';
echo strlen($language);

//結果：3
?>
```


他の組み込み関数についても確認したい。「count」は配列の要素の数を返す関数である。「rand」は１つ目の引数と、２つ目の引数の間のランダムな整数を返す。 他にもPHPの組み込み関数は多数あるが、覚える必要はあまりない。目的に沿ってその都度便利な組み込みメソッドがないか検索するとよい。


count - 配列の要素の数を返す関数
```php:index.php
<?php
$data = array('東京','大阪','京都');
echo count($data);

//結果：3
?>
```


rand - ランダムな整数を返す関数
```php:index.php
<?php
echo rand(1, 4);

?>
```

### 関数を自作する
### 戻り値

### formタグ
### テキストボックス
### \$\_POST
### セレクトボックス
### フォームを完成させる


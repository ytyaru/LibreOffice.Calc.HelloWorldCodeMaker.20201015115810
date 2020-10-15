# CalcでHelloWorldコード生成する

　プルダウンメニューから選択した言語のコードを表示する。

<!-- more -->

# 成果物

* [github](https://github.com/ytyaru/LibreOffice.Calc.HelloWorldCodeMaker.20201015115810)

![0](https://github.com/ytyaru/LibreOffice.Calc.HelloWorldCodeMaker.20201015115810/blob/master/doc/0.png?raw=true)
![1](https://github.com/ytyaru/LibreOffice.Calc.HelloWorldCodeMaker.20201015115810/blob/master/doc/1.png?raw=true)
![2](https://github.com/ytyaru/LibreOffice.Calc.HelloWorldCodeMaker.20201015115810/blob/master/doc/2.png?raw=true)

# 手順

1. 文書を作成する
2. 使ってみる

# 1. 文書を作成する

## 文書

項目|値
----|--
ファイル名|`hello_world_code_maker.ods`
シート名|`maker`, `codes`

## セル範囲名

名前|参照範囲または数式
----|------------------
`Languages`|`OFFSET($codes.$B$2,0,0,COUNTA($codes.$B:$codes.$B))`
`Codes`|`OFFSET($codes.$C$2,0,0,COUNTA($codes.$C:$codes.$C))`

* `OFFSET(参照; 行数; 列数; 縦; 横)`
* `COUNTA(値1; 値2; … 値30)`

## `maker`シート

セル|値|入力規則
----|--|
`B2`||`セルの範囲`。`Languages`
`B3`|`=INDEX(Codes,MATCH($B$2,Languages,0),0)`|

* `INDEX(範囲, 行, 列)`
* `MATCH(検索基準, 検査範囲, タイプ)`

## `codes`シート

```csv
Group,Language,Code
Programming,C,"#include <stdio.h>

main( )
{
  printf(""hello, world\n"");
}"
Programming,C++,"#include <iostream>

using namespace std;

int main(){
  cout << ""Hello world."" << endl;
  return 0;
}"
Programming,Rust,"fn main() {
    // 世界よ、こんにちは
    Println!(""Hello, world!"");
}"
Programming,C#,"using System;

public class Hello{
  public static void Main(){
    Console.WriteLine(""hello world!"");
  }
}"
Programming,Java,"class HelloWorld {
 public static void main(String[] args) {
 System.out.println(""Hello, world."");
 }
}"
Script,Python,"print(""Hello world!"")"
Script,Ruby,"print ""Hello World"""
,Go,"package main

import ""fmt""

func main() {
  fmt.Printf(""Hello world\n"")
}"
DomainSpecific,Bash,echo ‘Hello World’
DomainSpecific,SQL,"create table T(id int primary key);
insert into T values(0),(1),(2);
select * from T where id=0;"
Markup,HTML,"<!doctype html>
<html>
<head>
  <meta charset=""utf-8"">
  <title></title>
  <link rel=""stylesheet"" href=""css/main.css"">
  <script src=""js/main.js""></script>
</head>
<body>
</body>
</html>"
Markup,Markdown,# Hello world
```

1. 上記テキストをコピーする
1. セル`A1`にフォーカスする
1. `Ctrl`+`V`キーを押下してペーストする
1. `区切りのオプション`の`コンマ`にチェックを入れる
1. `OK`ボタンをクリックする

# 2. 使ってみる

1. `maker`シートのセル`B2`のプルダウンメニューから任意の言語を選ぶ
1. セル`B3`にコードが表示される

# 問題

* プルダウンメニューだけ操作できるようにしたいができない
	* シート保護するとプルダウンメニューまで操作できなくなる
* プルダウンメニューを変更したとき、コード内容をクリップボードにコピーしたいができない
	* 入力規則のイベントはキャッチできないと思われる
		* 他に方法はあるのか不明
	* クリップボードにコピーできるか不明
		* マクロならできるのか不明
		* イベントキャッチしてマクロと連動させる方法はあるのか不明

# 所感

　調べるとヘルプにはないフォームコントロールとかXFormsなどというキーワードを見つけた。イジって解析するしかないか……。

# 対象環境

* <time datetime="2020-10-15T11:20:45+0900" title="実施日">2020-10-15</time>
* [Raspbierry pi](https://ja.wikipedia.org/wiki/Raspberry_Pi) 4 Model B
* [Raspberry Pi OS](https://ja.wikipedia.org/wiki/Raspbian) buster 10.0 2020-08-20 [※](http://ytyaru.hatenablog.com/entry/2020/10/06/111111)
* [bash](https://ja.wikipedia.org/wiki/Bash) 5.0.3(1)-release
* LibreOffice 6.1.5.2 [※](http://ytyaru.hatenablog.com/entry/2022/07/16/000000) [※](http://ytyaru.hatenablog.com/entry/2022/08/09/000000) [Help](http://ytyaru.hatenablog.com/entry/2022/08/16/000000)

```sh
$ uname -a
Linux raspberrypi 5.4.51-v7l+ #1333 SMP Mon Aug 10 16:51:40 BST 2020 armv7l GNU/Linux
```

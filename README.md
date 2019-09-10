# Oreore-Basic

Oreore-Basicは[Oreore-OS](https://github.com/kousoz80/oreore-OS)上で動作する
Basic処理系です。

![enter image description here](https://imgur.com/wqStfS8.jpg)


![enter image description here](https://imgur.com/3IJi7Rt.jpg)



■使用できるBASICコマンド、関数

(1) ラベル

ラベルはgoto文やgosub文の飛び先を指定するために用いられます。

ラベルは先頭に"@"をつけた任意の英数字で表現されます

<例>

@loop1:

@exit2:

※１行に2つ以上のラベルを記述すると最初のラベルしか認識されないので注意すること

コマンド(キーワードは英数小文字でしか受け付けません)

・new

・end

・list

・load

・save

・run

・edit
エディタを起動してプログラムを編集します
使用方法はOS付属のエディタと同じです。

・make
・make "ファイル名"
BASICプログラムをoregengo-Rプログラムに変換して
ファイルに出力します。
ファイル名が省略されると"bas_out.r"という名前のファイルが作られます。
また生成されたプログラムをコンパイルするためには
OSのコマンドモードで以下のコマンドを打ち込んで下さい。
 $ orc stdio.rh basic.rh ソースファイル名.r
 $ asm asm.s 実行ファイル名.efi
 
 (例)
 $ orc stdio.rh basic.rh bas_out.r
 $ asm asm.s test.efi
 
 
・bye

BASICを終了してOSに復帰します

・ print

・ print #

ファイルやネットワークにデータを出力する

・ input

・ input #

ファイルから変数にデータを入力する

(ネットワークでの利用は不可、input$またはrecv関数を使うこと)

・ goto

<例>

goto @loop1

・ for

・ next

・ gosub

<例>

gosub @sub1

・ return

・ if

<例>

if a>0 then print a

if a<0 then @label1

if a=1 then print a else @label2

・ dim

・ open

ファイルを開く
<例>
open "test.txt" for input as#1
open "test.txt" for output as#1

・ close

ファイルを閉じる

<例>

close #1

close

・ clear

・ cls

・ locate

・ pset( x , y ), c

座標(x, y)に点を打つ

cは色コードで&hrrggbb

rr：赤成分(00~ff)

gg：緑〃

bb：青〃

・ line(x1, y1)-(x2, y2), c

座標(x1,y1)、(x2,y2)間に線を引く、ｃは色コード

・ box(x1,y1)-(x2,y2), c

座標(x1,y1)、(x2,y2)を対角とした長方形を描く

・ boxf(x1, y1)-(x2, y2),c

座標(x1,y1)、(x2,y2)を対角とした塗りつぶした長方形を描く

・ circle(x1, y1)-(x2,y2),c

box(x1,y1)-(x2,y2), cで描かれる長方形に内接する楕円を描く

・ circlef(x1, y1)-(x2,y2),c

box(x1,y1)-(x2,y2), cで描かれる長方形に内接する塗りつぶした楕円を描く


・ image(x, y),"画像ファイル名"

座標(x, y)に画像※を表示する


・ exec "コマンド"

コマンドをOSに発行して実行する

execコマンドはプログラムの実行を一時停止して、起動したプロセスの終了待ちをおこなう

・ wait x

x(ミリ秒)プログラムを一時停止させる

(3) 関数(関数名は英数小文字でしか受け付けません)

・ abs(x)

・ point(x,y)
画面に指定された座標の色コードを返す


・ chr$(c)

・ asc(x)

・ mid＄(a＄,x,y)

・ left＄(a$,x)

・ right＄(a＄,x)

・ len(a＄)

・ sin(x)

・ cos(x)

・ tan(x)

・ atn(x)

・ exp(x)

・ log(x)

・ input＄(x)・・・コンソール入力

 ・ input＄(x,y)・・・ファイル入力

ファイルやコンソールから指定文字数の文字列を受けとる

<例>

a＄=input＄(1,2)

※ただしファイルの終わりに達した場合、キャラクタコードの255番に相当する特殊な文字列を返す

・ inkey$

リアルタイムでのキー入力を得る

<例>
a＄=inkey＄
print inkey＄

・ str$

・ val

・ len

・ instr


(4) 変数

変数の型は数値(実数)型と文字列型だけです。

変数名の末尾に"$"をつけるとその変数は文字列型であると解釈されます。

なお文字列型変数に格納できる文字列は511文字までです。

また配列変数の次元は10次元まで宣言できます。例えば

dim aa(10,20)

とするとaa(0,0)からaa(10,20)までの11x 21個の配列要素が設定されます。


■コンパイル・実行
ソースコードファイル"oreore_basic001.prj"をコンパイルするためには"ObjectEditor"という開発環境およびoregengo_Rコンパイラが必要となります。
詳細については以下のリンクを参照して下さい。
https://github.com/kousoz80/ObjectEditor
  
https://github.com/kousoz80/oregengo_R

コンパイル手順は
ObjectEditorを起動してソースコードファイルを開いてコンパイルボタンをクリックすればコンパイルが始まります。


![enter image description here](https://imgur.com/ROyaXIc.jpg)

コンパイルが終了したら、出来上がったUEFIアプリケーションファイルをOreore-OSの起動USBメモリにコピーしてパソコンを起動すればBasicが使用可能になります。



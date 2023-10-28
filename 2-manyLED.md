- [GND共通で複数個使う](#gnd共通で複数個使う)
  - [必要なもの](#必要なもの)
  - [ちょっとレベル高い機能を使う](#ちょっとレベル高い機能を使う)
  - [演習](#演習)
- [アノードコモンの場合](#アノードコモンの場合)
  - [配線](#配線)
  - [**一々digitalWriteを2つ書くのがダルい**](#一々digitalwriteを2つ書くのがダルい)
- [3つ以上に増やす](#3つ以上に増やす)
  - [ピン変更しやすくする](#ピン変更しやすくする)
    - [マクロ定義](#マクロ定義)
    - [グローバル変数で宣言する](#グローバル変数で宣言する)
  - [2つ以上に増やすときに問題となる点](#2つ以上に増やすときに問題となる点)
  - [initializer関数を作る](#initializer関数を作る)
  - [busout関数を書き換える](#busout関数を書き換える)
  - [クラスでまとめる](#クラスでまとめる)
    - [説明　ポインタ渡し](#説明ポインタ渡し)
    - [説明　オペレーターオーバーロード](#説明オペレーターオーバーロード)


# GND共通で複数個使う
複数個Lチカをする

## 必要なもの
2つのLEDと2つ抵抗を容易し、15番ピンと14番ピンにそれぞれのアノード側をつなげる。

```cpp

```

## ちょっとレベル高い機能を使う
配列でピン番号を保存する

## 演習
片方だけ見ると1s間隔で点滅し（1Hzの意）、もう片方と交互に点滅するようにする。

# アノードコモンの場合
ローサイドスイッチを学ぶ、BusOutを作る

2sc1815というNPNトランジスタと100Rぐらいの抵抗を2つずつ用意する。
## 配線
抵抗を介して、マイコンから供給する5Vと各LEDのアノードをつなげる。
LEDのカソードと1815のコレクタをそれぞれ繋げる
1815のエミッタはGNDに繋げ、ベースは約100Rを介して15番と14番に繋げる。（↑の演習をそのまま使いたい）

## **一々digitalWriteを2つ書くのがダルい**

ということで関数を書こう。
[参考](https://atcoder.jp/contests/apg4b/tasks/APG4b_p)

書いて欲しい関数は、1つの整数値を引数とし（値範囲は0〜3）、0なら全消灯、1なら14番ピンのみ点灯、2なら15番ピンのみ点灯、3なら全点灯。

# 3つ以上に増やす
↑で書いた関数の問題点は次の2つが挙げられる。
* あそらく2つしか対応していない
* ピン変更のときクソだるい

## ピン変更しやすくする
### マクロ定義

```cpp
#define pin_l1 15
#define pin_l2 14
#define pin_l3 13
```

### グローバル変数で宣言する
```cpp
constexpr int pin_l1 = 15;
constexpr int pin_l2 = 14;
constexpr int pin_l3 = 13;
```

このときのプログラムの構造
図はむずかった。コードもめんどくさくなった
```cpp
#include <Arduino.h>

constexpr int LEDpin[3] = {15, 14, 13};

void user_main(){
    pinMode(LEDpin[0], OUTPUT);
    pinMode(LEDpin[1], OUTPUT);
    pinMode(LEDpin[2], OUTPUT);

    while(1){
        busout(0x11);
        delay(500);
        busout(0x00);
        delay(500);
    }
}

void setup(){
    user_main();
}

void loop(){}
```

## 2つ以上に増やすときに問題となる点
pinMode、digitalWriteが足りない

解決策のヒントとしてLEDをN（任意の自然数）回だけ点滅させるプログラムを書く。
for文、while文両方で書けるように

```cpp
int num_flash = 3; //点滅回数

void user_main(){
    pinMode(LEDpin, OUTPUT);

    for(int i = 0; i < num_flash; i++){
        digitalWrite(LEDpin, HIGH);
        delay(500);
        digitalWrite(LEDpin, LOW);
        delay(500);
    }
}
```

```cpp
int num_flash = 3; //点滅回数

void user_main(){
    pinMode(LEDpin, OUTPUT);

    int i = 0;
    while(i < 3){
        digitalWrite(LEDpin, HIGH);
        delay(500);
        digitalWrite(LEDpin, LOW);
        delay(500);

        i++;
    }
}
```

## initializer関数を作る
ピン数を指定する変数を用意し、for文でpinModeする
```cpp
int num_pin = 3; //ピン数

void user_main(){
    for(int i = 0; i < num_pin; i++){
        pinMode(LEDpin[i], OUTPUT);
    }

    ~~~    
}
```

## busout関数を書き換える
ピン数を指定する変数から、for文といい感じにビット振り分けする演算を実装する

むずい

## クラスでまとめる

動作確認はしてないが多分行ける。

```cpp
class BusOut{ // the number of gpio pin is limited to 8 pins.
private:
    int LEDpins[8];

    BusOut(int* _LEDpins, int _num_pins){
        for(int i = 0; i < 8; i++){
            pinMode(*(_LEDpins + i), OUTPUT);
        }
    }

    void operator = (int value){
        bool bit[8] = {
            value / 128,
            value % 128 / 64,
            value % 128 % 64 / 32,
            value % 128 % 64 % 32 / 16,
            value % 128 % 64 % 32 % 16 / 8,
            value % 128 % 64 % 32 % 16 % 8 / 4,
            value % 128 % 64 % 32 % 16 % 8 % 4 / 2,
            value % 128 % 64 % 32 % 16 % 8 % 4 % 2,
        }

        for(int i = 0; i < 8; i++){
            digitalOut(*(_LEDpins + i), bit[i]);
        }
    }
};
```

### 説明　ポインタ渡し

変数を関数の呼び出しの（）内に書くことによって、関数に値を入れることが出来る。
しかし、同じような引数がいっぱいあり、関数の呼び出しの（）内にいっぱい書くのが面倒なことがある。GPIOピンがいっぱいとか、そんなときに使える記法。

まず変数は、パソコンの構成部品の一つである、**メモリ**に保存されている。そしてプログラムを実行するパソコンのシステムは、その変数を読み込むとき、変数のメモリ上の住所を見て読み込む。この住所をアドレスという。

ポインタとは、変数が保存されているアドレスのことである。つまり、アドレスを直接考えることで変数のあれこれを考える方法である。

**使い方**
1. 同じような変数を配列でまとめる。こうすると、今回の場合LEDpins[0]とLEDpins[1]とはアドレスが連続し、&LEDpins[0] + 1 == &LEDpins[1] はtrueとなる。
2. 配列の一番最初、今回ならLEDpins[0]のアドレスを渡す。
3. 1で説明した性質を利用しfor文とかで回して参照する。

### 説明　オペレーターオーバーロード
[mbedのBusOut](https://os.mbed.com/users/okini3939/notebook/BusOut_jp/)を真似したかったのでつかった。出力出来るようになる
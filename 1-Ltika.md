# やること

# 部品説明

# ただのLチカ
コピペ用
```Arduino
#include <Arduino.h>

constexpr int pin = 13;

void setup(){
    pinMode(pin, OUTPUT);
}

void loop(){
    digitalWrite(pin, HIGH);
    delay(500);
    digitalWrite(pin, LOW);
    delay(500);
}
```
## プログラム説明
### #include <>
### int
### void setup(){}
### void loop(){}
### pinMode(pinNumber, Mode);
### digitalWrite(pinNumber, State);

# ボタン押したら光る。回路のみ

# ボタン押したら光る。マイコン介して
## if elseを用いる1
```Arudino
void loop(){
    bool pinstate;
    pinstate = digitalRead();
    if( pinstate == true ){
        digitalWrite(,HIGH);
    } else{
        digitalWrite(,LOW);
    }
}
```

## if elseを用いる2
```Arduino
void loop(){
    if( digitalRead() == true ){
        digitalWrite(,HIGH);
    } else{
        digitalWrite(,LOW);
    }
}
```

## if elseを用いる3

```Arduino
if(digitalRead()){
    ~
}
```

## 三項演算子「（条件式）? (真のときの処理) : (偽のときの処理);」を用いる
書いて


# これはなに？
JA1YNXの技術継承資料兼全国のマイコン工作をする中高生に向けた資料です（願望）
そして、これはリポジトリ名にある通り、ESP32での開発に限った資料となっています。他のマイコンと重複する内容もあるが、出来る限り丁寧に解説します。

この演習全体の目標は「マイコンを用いて様々なことが、誰から見てもわかりやすいコードで開発できること」

# 特徴
様々な状況に対応出来るように基本的な中身の話を多く盛り込んでいます。
また、c++の知識は読んでいれば一通りつきます。
そして、取得したい知識を選択出来るように、進め方を選択できるようにしています。もちろん最終的にはすべての知識を得られるようなコース分けをしています。

# 注意
**このような技術系資料には必ず書かれていますが、この記事を参考にして起こった事故などの責任は負うことが出来ません。すべて自己責任で開発してください**
**また、わからないことがあったら適宜ググってください。一つのサイトに頼るのはとても危険です。様々なサイトを見て、正しい知識を得て、そのサイト主の工夫などがわかるようになってください。**個人的にはc++の構文についてはオンラインプログラム塾のページがわかりやすいと思います。その他の知識は「Qiita　>>　個人サイト　>=　わかりやすい公式ドキュメント　>= tera teil >>>> Microsoft公式ドキュメント」みたいな感じなので、とりあえずQiitaと個人サイトを見漁りましょう。

# 目次
## 超じっくり中身を着実に知っていくコース（次点で推奨その２）
- [講座0　環境構築ーwindows ver.]()
- [講座0.0　環境構築ーmac ver.]()
- [講座0.1　環境構築ーLinuxとは〜インストール]()
- [講座0.2　環境構築ーLinux基本コマンドなど慣れるためのページ]()

- [講座1　Lチカ](https://github.com/JA1YNX/Exercises_for_ESP32/blob/main/1-Ltika.md)
- [講座1.1　様々なLチカ、可読性について](https://github.com/JA1YNX/Exercises_for_ESP32/blob/main/1.1-Ltikas.md)
- [講座1.2　Lチカをするまでの難しさ1ーコンパイラ]()
- [講座1.3　Lチカをするまでの難しさ2ーエディタ]()
- [講座1.4　マイコンってなんだよ1ーハードウェア説明（流石にめちゃめちゃ詳しいのは書けない）]()
- [講座1.5　マイコンってなんだよ2ーソフトウェア説明（流石にめちゃめちゃ詳しいのは書けない）]()
- [講座1.6　というかパソコンってなんだよ1ーハードウェア説明（流石にめちゃめちゃ詳しいのは書けない）]()
- [講座1.7　というかパソコンってなんだよ2ーソフトウェア説明（流石にめちゃめちゃ詳しいのは書けない）]()
- [講座1.8　というかパソコンってなんだよ3ー仮想環境とは、wsl、utm、docker（流石にめちゃめちゃ詳しいのは書けない）]()

- [講座2　LEDたくさん](https://github.com/JA1YNX/Exercises_for_ESP32/blob/main/2-manyLED.md)
- [講座2.1　そういえばLEDとは]()
- [講座2.2　いつも使う液晶、ELはなんなの]()

- [講座3　楽に扱いたいー関数、クラス、構造体など]()
- [講座3.1　thisポインタ、オーバーロード、テンプレートなどの機能]()
- [講座3.2　LEDマトリックスに文字を流す]()
- [講座3.3　LEDマトリックスに映像を流す1]()
- [講座3.4　LEDマトリックスに映像を流す2]()

- [講座4　アナログ入力]()
- [講座4.1　分解能、〜]()

- [講座5　各種通信ーパラレル、UART、BT、i2c、spi、CAN、Wifi]()
- [講座5.1　UARTプロトコル]()
- [講座5.2　Bluetoothプロトコルなど]()
- [講座5.3　i2cプロトコル]()
- [講座5.4　spiプロトコル]()
- [講座5.5　CANプロトコル]()
- [講座5.5　EtherNet]()
- [講座5.6　RS232]()
- [講座5.7　EtherCAN]()

- [講座6.0　アクチュエータ類ー種類、各種とりあえず動かせるように]()
- [講座6.1　エアシリ電磁弁の中身]()
- [講座6.2　MDの中身]()
- 
- [講座7.0　センシング概論]()
- [講座7.1　電圧、電流]()
- [講座7.2　温度、湿度]()
- [講座7.3　IMU9軸分]()
- [講座7.4　ロータリーエンコーダ](https://github.com/JA1YNX/Exercises_for_ESP32/blob/main/7.4-RotaryEncoder.md)
- [講座8.0　制御ーPID](https://github.com/JA1YNX/Exercises_for_ESP32/blob/main/8-PID.md)

## 早く使いたいけど自分でデバック出来ないと困るコース（推奨）
## とりあえず早く使いたいコース（次点で推奨）

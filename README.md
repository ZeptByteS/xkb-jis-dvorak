## JIS Dvorak


![](https://github.com/ZeptByteS/xkb-jis-dvorak/blob/master/pictures/jis_dvorak_en.png)


Custom keyboard layout for JIS keyboards based on the Dvorak


Ubuntu Gnome 16.04上で作成した,JIS配列キーボード用の設定ファイルです.


---
xkb/geometryファイルについては,下記を参照してください.


https://github.com/ZeptByteS/xkb-geometry-jis


---
AltGr(Level3_Shiftキー)とMetaキーを使ってひとつのキーに最大で6種類の機能を割り当てられるこのレイアウトは,ホームポジションと上下2段の30個のキーを使ってアルファベット, 数字, 記号, カーソルキー, Home, End, PageUp, PageDown, Ctrl+Z, X, C, V へのリダイレクトを入力できます.

左手親指に割り当てられたShiftキーは, "どちらの手の小指でShiftを押すかを判断し,届く指で入力したいキーを押す" という一連の動作を簡略化し,より素早く大文字を入力できます.


xkb/keycodes/evdevは,ScrollLockとNumLockのインジケータの位置を入れ替え,テンキーの無い91キーボードでNumLockを使用しやすくします.キーボードのScrollLock用のLEDがNumLockと連動して光ります.


この設定ファイルは```xkb/symbols/pc```(日本語,英語のどのレイアウトを選択していても読み込まれる修飾キーなどの配置を決めるファイル)とデフォルトのDvorak配列を上書きします.


このレイアウトを有効にするには,```/usr/share/X11/xkb/``` 以下にファイルを上書きもしくは追加し,再ログインします.


---

### AltGr / NumLock+Shift / NumLock+AltGr
![](https://github.com/ZeptByteS/xkb-jis-dvorak/blob/master/pictures/level3_numlock%2Bshift_numlock%2Blevel3.png)

---

### AltGr+Shift / NumLock / NumLock+AltGr+Shift
![](https://github.com/ZeptByteS/xkb-jis-dvorak/blob/master/pictures/level3%2Bshift_numlock_numlock%2Blevel3%2Bshift.png)

---

### Meta
![](https://github.com/ZeptByteS/xkb-jis-dvorak/blob/master/pictures/meta.png)

---

### Japanese Dvorak
![](https://github.com/ZeptByteS/xkb-jis-dvorak/blob/master/pictures/jis_dvorak_jp.png)

---


### カスタマイズ

xkb/symbols/us(dvorak)の設定は下記のような構造になっています.

```c
key <AD08> {
    symbols[Group1]=
                  // Level1       Level2          Level3        Level4          Level5
                  //   Base        Shift           AltGr             -     AltGr+Shift
             [            c,           C,      braceleft,           Up,      braceleft ],
    actions[Group1]= 
             [   NoAction(),  NoAction(),     NoAction(),   NoAction(),     NoAction(),
             
                       RedirectKey(key=<UP>, clearmods=Lock+Mod3),  //  Level6  Meta
                       RedirectKey(key=<UP>, clearmods=Lock+Mod3) ] //  Level7  Meta+Shift
    };
```     
    
Level4はkeyboard layout chartを見やすくするために用意した実際には使われないシンボルです.


MetaキーにはMod3を割り当ててあります.

xkb/symbols/us内のbasicセクション(QWERTY配列)やデフォルトのDvorak配列のシンボルを参考にし,お使いの言語に合わせてLevel3~Level7のシンボルもしくはアクションを編集してください. カーソルキー,修飾キー付きの動作,および数字キーの入力は,RedirectKeyを使ったほうがちゃんと動きます.


### キーがリピートしない場合


Metaキーを使用してリダイレクトさせるキーがリピートしない場合は,```~/.bashrc```に以下のコマンドを追加してください


    xset r 30 # <AD07> = G Home
    xset r 31 # <AD08> = C Up
    xset r 32 # <AD09> = R End
    xset r 33 # <AD10> = L PageUp
    
    xset r 44 # <AC07> = H Left
    xset r 45 # <AC08> = T Down
    xset r 46 # <AC09> = N Right
    xset r 47 # <AC10> = S PageDown
    
    xset r 52 # <AB01> = ; ctrl+Z
    xset r 53 # <AB02> = Q ctrl+X
    xset r 54 # <AB03> = J ctrl+C
    xset r 55 # <AB04> = K ctrl+V

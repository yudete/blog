---
title: Visual Studio Code を使ってC言語を書く
date: '2020/10/08 15:47'
categories:
  - Visual Studio Code
  - MinGW
  - gcc
  - C
author: yude
---
この記事では、主に Windows での手順を説明します。

<!--more-->
# Visual Studio Code 何？
Visual Studio Code は、Microsoft が作ったコードエディターです。

## Eclipse とどう違うの？
Eclipse には、最初からプログラミング言語を操るツールが付属しています。一般的にこれらのソフトウェアを「統合開発環境 (IDE)」と言います。  
対して Visual Studio Code は「エディター」です。__初期状態では__ビルドを実行したり、間違いを警告したりする機能が付いていません。この記事では、それらの機能を追加する手順も解説します。  

# 導入
## 目次
ステップ 1. MinGW のインストール  
ステップ 2. Visual Studio Code のインストール  
ステップ 3. Visual Studio Code の設定  
ステップ 4. 簡単にコンパイルできるようにする  
ステップ 5. コンパイルした `exe` ファイルを実行する

## ステップ 1. MinGW のインストール
まず、[](https://ja.osdn.net/projects/mingw/downloads/68260/mingw-get-setup.exe/) を開いて、「MinGW-Get」というソフトウェアをダウンロードします。
![](../assets/images/how2vscode/1.png)  
`Install` をクリックして、インストールを始めます。  
![](../assets/images/how2vscode/2.png)
この画面では、特に何もいじらず `Continue` をクリックすればOKです。
![](../assets/images/how2vscode/3.png)
ダウンロードが始まりました。少し待てば終わります。  
![](../assets/images/how2vscode/4.png)
⬆終わるとこんな感じになるので、`Continue` をクリックしましょう。  
![MinGW Installation Manager](../assets/images/how2vscode/5.png)  
さっきの画面から一転、何やらゴチャゴチャしたウィンドウが開きます。ここから MinGW をインストールできる訳です。  
`mingw32-base-bin` と `mingw32-gcc-g++-bin` のチェックボックスをクリックして、下の画像のように操作します。  
![](../assets/images/how2vscode/6.png)  
その後、メニューバーから `Installation` をクリックして、`Apply Changes` をクリックします。  
![](../assets/images/how2vscode/7.png)  
すると... 確認画面が現れます。`Apply` をクリックするとインストールが始まります。  
![](../assets/images/how2vscode/8.png)
![](../assets/images/how2vscode/9.png)
終わると下のような表示になります。これで `MinGW Installation Manager` でやる作業は終わりなので、閉じてください。  
![All changes were applied successfully](../assets/images/how2vscode/10.png)

## ステップ 2. Visual Studio Code のインストール
まず、[Download Visual Studio Code - Mac, Linux, Windows](https://code.visualstudio.com/download) からVisual Studio Codeをダウンロードします。  
サイトは英語ですが、Visual Studio Code 自体は日本語化できるので安心してください。
![ココ](../assets/images/how2vscode/11.png)  
ここですね。  

適当にインストールしていきましょう。
![](../assets/images/how2vscode/12.png)  
下の画面で、  
* エクスプローラーのファイル コンテキスト メニューに [Code で開く] アクションを追加する
* エクスプローラーのディレクトリ コンテキスト メニューに [Code で開く] アクションを追加する  

にチェックを入れておくと便利です。
![](../assets/images/how2vscode/13.png)  

## ステップ 3. Visual Studio Code の設定
Visual Studio Code では、「拡張機能」というものをインストールして自由にカスタマイズすることができます。  
今回は以下の拡張機能を導入します。  
* C/C++  
C言語を書いたときに "シンタックスハイライト" というものを効かせ、コードを見やすくすることができます。また、構文が間違っている際に指摘してくれます。
* Japanese Language Pack for Visual Studio Code  
Visual Studio Code を日本語化します。  

手順  
1. 「拡張機能」のタブを開きます。Japanese Language Pack の導入前だと英語で表示されるかもしれませんが、アイコンなどで判断してください。  
![](../assets/images/how2vscode/14.png)  
そして、ここに導入したい拡張機能の名前を入力し、Enter を押すと検索が始まります。  
![](../assets/images/how2vscode/15.png)  
上で示した拡張機能を見つけ、「インストール」または「Install」をクリックします。  
![](../assets/images/how2vscode/16.png)  

以上で拡張機能のインストールができたはずです。

## ステップ 4. 簡単にコンパイルできるようにする
このままの状態では、度々 コマンド プロンプト を呼び出してコマンドを実行する必要があります。面倒なので、ショートカットキーでコンパイルできるようにしてしまいましょう。  

1. 作業フォルダの作成
まず、書いたコードを設置するフォルダを作成します。今回は `src` とします。  
![](../assets/images/how2vscode/17.png)

2. 作成したフォルダを Visual Studio Code で開く
![](../assets/images/how2vscode/18.png)  
メニューから選んで、フォルダを指定すればよいです。

3. コンパイルするための設定ファイルを作成する  
まず、左のパネルを右クリックし、新規ファイルを作成、名前を `(適当に決める).c` とします。  
![](../assets/images/how2vscode/19.png)  
そして、以下のコードをコピー & ペーストしてください。
    {% codeblock lang:c %}
    #include <stdio.h>
    int main(void){
      printf("Hello world!\n");
    }
    {% endcodeblock %}
    `Ctrl` + `S` で保存した後、`Ctrl` + `Shift` + `B` を押します。
    ![](../assets/images/how2vscode/20.png)  
    このような画面が現れるはずなので、画像の歯車をクリックします。  
    **歯車が存在せず、`C/C++: gcc.exe build active file` だけが表示されている場合は以下の手順は不要です。そのまま Enter を押すとビルドができるので、ステップ 5 まで飛ばしてください。**  
    まず、選んでいる項目が `C/C++: gcc.exe build active file` となっていることを確認してください。  
    すると、以下のようなファイルが生成されるはずです。(細部は異なることがあるかもしれません。)  
    これで完了です。  
    ![](../assets/images/how2vscode/21.png)  
4. コンパイルしてみる  
    さて、ようやくコンパイルします。先程作った `(適当に決める).c` に戻って、`Ctrl` + `Shift` + `B` を押します。  
    表示のようにメニューが表示されたことを確認して、`Enter` を押します。  
    ![](../assets/images/how2vscode/22.png)  
    すると、コンパイルが始まり、少し待つと同じディレクトリに `exe` ファイルが生成されるはずです。  

## ステップ 5. コンパイルした `exe` ファイルを実行する
C言語のソースファイルを開いた状態で、`Ctrl` + `Shift` + `@` を押すと、下に「ターミナル」が現れるはずです。**既にターミナルが現れている場合は不要です。**  
![](../assets/images/how2vscode/23.png)  
ここで、`.\(ファイル名)` と入力して Enter を押すと、実行されます。  
![](../assets/images/how2vscode/24.png)  
ファイル名について: ソースコードのファイル名が例えば `test.c` だった場合、入力するのは `.\test.exe` となります。

## 注意点・トラブルシューティング 等
### 文字化けを解消する
ターミナルで `chcp 65001` と入力した後、Enter を押してください。

### プログラムの実行を途中で中止する
ターミナルの部分をクリックした後、`Ctrl` + `C` というショートカットキーを入力すると中断できます。

# 終わり
以上で Visual Studio Code を C 言語の開発に使う方法の説明を終わります。  
不明な点があった場合、[Twitter](https://twitter.com/yudejp) または Discord (`yude#3205`) までリプライや DM を送ってもらえれば、可能な範囲でお答えします。  

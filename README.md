# 1. madever
[Evernote for Mac](http://evernote.com/)で[Markdown](http://daringfireball.net/projects/markdown/)を利用できるようにするAppleScript。

Markdown文書からEvernoteのリッチテキストに変換したり、EvernoteのリッチテキストからMarkdown文書に変換したりといったことができる。

![](/Users/sandai/dev/sandai/madever/sample/img02.png)

このように、Evernoteクライアント上で構造化されたデザイン文書を作成することが可能で、デザインは自分でカスタマイズできる。


# 2. installing

	cd ~/Library
	mkdir Scripts
	cd Scripts
	git clone git://github.com/sandai/madever.git

gitを利用していなければ下記のURLから普通にダウンロード。

[https://github.com/sandai/madever/downloads](https://github.com/sandai/madever/downloads)

madeverディレクトリをダウンロードできたら、

	~/Library/Scripts
	
に配置。`~/Library`はOS X Lion以降であれば隠しフォルダになっていると思うので、[こちら](http://macfan.jp/guide/2011/07/26/lion_2.html)を参考にして見つける。

madeverディレクトリは`~/Library/Scripts`以下に置かなければ**正しく動作しない**ので注意。

最終的に、`~/Library/Scripts/madever`のようなディレクトリ構造になっていれば問題ない。なお、`~/Library/Scripts`ディレクトリが存在しなければ自分で作成する。

## 2.1. Pandoc

madeverではmarkdownやリッチテキストの変換処理を[Pandoc](http://johnmacfarlane.net/pandoc/)というコンバータを利用してるので、それを別途インストールする必要がある。その方法を以下に2つ挙げる。

### 2.1.1. Homebrew

	% brew install haskell-platform
	% cabal update
	% cabal install pandoc

次に.zshrcにパスを通す。(madeverはパスが通っていなくても問題はない)

	PATH=$HOME/.cabal/bin:$PATH			

### 2.1.2. Installer

[http://code.google.com/p/pandoc/downloads/list](http://code.google.com/p/pandoc/downloads/list)
	
Hombrewなどパッケージ管理システムを利用していなければインストーラを利用すると良い。

### 2.1.3. 上記以外の方法でインストールしている場合

madever側のスクリプトでは`~/.cabal/bin/pandoc`と`/usr/local/bin/pandoc`のpandocは自動で利用できるようにしているが、それ以外のパスであれば対応できていない。

その場合は自分でパスを設定する必要がある。`madever/madever.scpt`をAppleScriptエディタで開いて、

![](/Users/sandai/dev/sandai/madever/sample/img01.png)

任意のパスを記述してほしい。

# 4. Use
Evernoteでmarkdownやリッチテキストを変換するにはmadeverディレクトリにある`madever/madever.scpt`を実行する。実行方法はいくつかあるが最も基本的だと思われる方法を以下に3挙げる。

個人的には3つ目の[Spark](http://www.shadowlab.org/softwares/spark.php)を推奨する。

## 4.1. メニューバーから実行

AppleScriptエディタ.appを開いて環境設定画面のチェックを画像のように入れる。

![](/Users/sandai/dev/sandai/madever/sample/img03.png)

するとメニューバーにスクリプトのアイコンが表示されるのでそこからmadeverが実行できる。

![](/Users/sandai/dev/sandai/madever/sample/img04.png)

## 4.2. Alfredから実行
[Alfred](http://www.alfredapp.com/)はランチャーアプリ。[appstore](http://itunes.apple.com/jp/app/alfred/id405843582)からインストールできる。インストールしたらメニュバーの「Preferences…」を次のように設定する。

![](/Users/sandai/dev/sandai/madever/sample/img05.png)

あとはホットキーを押して下の画像のように呼び出すと実行できる。

![](/Users/sandai/dev/sandai/madever/sample/img06.png)


### 4.2.1. Alfredで利用できない場合

Alfredはspotlightのインデックスを利用している。よって、`~/Library`がspotlightの対象外であればサーチにひっかからず呼び出せない。この現象はOS X Lionで確認済みだが以前のバージョンでも同じかもしれない。

その場合ホームディレクトリなどspotlightの対象に該当する適当な場所にmadeverディレクトリを置いて、シンボリックリンクを`~/Library/Scripts/madever`に張るようにすれば良い。

	ln -s ~/madever ~/Library/Scripts/madever


## 4.3. Sparkから実行(推奨)
[Spark](http://www.shadowlab.org/softwares/spark.php)はホットキーアプリ。これを利用すればショートカットでスクリプトを実行することが可能となるので、スクリプトを意識せずに**ネイティブな機能のように変換**することができる。個人的にはこの方法を推奨する。

- 導入の参考ページ
	- [MacでキーボードショートカットからAppleScriptを起動する](http://d.hatena.ne.jp/foldrr/20111102/p1)

### 4.3.1. 導入例

ショートカットを`⌘R`に設定して`madever.scpt`を選択すれば、Evernote上で `⌘R`を押すと実行できるようになる。

![](/Users/sandai/dev/sandai/madever/sample/img07.png)

### 4.3.2. SparkでLibraryディレクトリが見つからない場合

OS X Lion以降であれば下の画像のようにLibraryディレクトリがSparkで表示されていないかもしれない。

![](/Users/sandai/dev/sandai/madever/sample/img08.png)

その場合は、[こちら](http://macfan.jp/guide/2011/07/26/lion_2.html)の方法でまずFinderでLibraryディレクトリを表示して、ScriptsディレクトリをDrag&DropでSparkのウィンドウに持っていけばmadeverディレクトリが表示される。

![](/Users/sandai/dev/sandai/madever/sample/img09.png)


## 4.4 madeverの操作

上記のいずれかの方法で`madever.scpt`を実行すると、下の画像のように文書をmarkdownにするかhtml(リッチテキスト)にするかダイアログが表示されるので、どちらかを選択すればあとは自動で全て行われる。

![](/Users/sandai/dev/sandai/madever/sample/img12.png)

# 5. theme

madeverでは自分で文書のデザインをCSSによって作成することができる。作成したはテーマは`madever/themes`以下にテキスト形式で保存し、`loadteheme.scpt`を編集することで利用できるようになる。

## 5.1. テーマの作成

`madever/themes/template.txt`をコピーして名前を変更し適当なエディタで編集する。

![](/Users/sandai/dev/sandai/madever/sample/img14.png)

事前に利用できるセレクタは限られているので、テンプレートの通りにセレクタを利用しプロパティを設定しなければならない。

![](/Users/sandai/dev/sandai/madever/sample/img10.png)

## 5.1.1. 書式

基本的にはCSSと代わりないが独自の書式形式で記述する。形としては次のような形式となるが、よくわからなければ他のテーマの記述を参考にすると良い。

	body
	property 1
	property 2
	
	h1
	property 1
	property 2
	property 3
	
	h2
	property 1
	property 2
	property 3
	property 4


上記のような形で記述する必要がある。

- **あらかじめきめられたセレクタだけを利用する**
- **セレクタの上は1行だけ開ける**
- **プロパティ同士は離さない**
- **コメントを入れない**

これらのことを守れば問題はない。

なお、`madever/template.txt`には最初の段階で以下のような形でコメントが書かれているが、

	--このようなコメントがあるのでそれらは削除すること

最終的には全て削除して保存してほしい。

## 5.1.2. テーマの保存
作成したテーマは`madever/themes/`以下に保存する。ファイル形式は他のテーマでも`.txt`になっているがテキストファイルとして扱えるなら何でも構わない。


## 5.2. テーマの変更

テーマを変更するには`madever/loadtheme.scpt`をAppleScriptエディタでを開き`property filename: ""`に変更したいテーマのファイル名を指定して保存すれば変更される。

![](/Users/sandai/dev/sandai/madever/sample/img11.png)


## 5.3. 作成したテーマを利用する前に

テーマを作成した後は`madever/test/test.md`のテキストをEvernoteにコピーして試してみると良い。

# 6. Markdown Guide of madever

madeverで利用できるMarkdown記法は基本的に通常の記法と違いはないが、Pandocに依存しているためいくつか異なる部分があること、そして、画像の扱いはMarkdown記法を使う必要がない部分で異なる。

## 6.1. PandocのMarkdown記法

コンバータのPandocに依存しているため通常のMarkdown記法とはいくつか異なる部分がある。

### 6.1.1. 改行がバックスラッシュ
[http://johnmacfarlane.net/pandoc/README.html#paragraphs](http://johnmacfarlane.net/pandoc/README.html#paragraphs)

通常Markdown記法は**行末に2つ以上スペース**を入れることで改行が行われるようになっている。Pandocでもそれは同じだが、バックスラッシュ(`\`)でも行われるようになっている。

~~~
行末にバックスラッシュ\
をいれると改行になる。
~~~

リッチテキストからmarkdownに変換した場合に改行はバックスラッシュ(`\`)で表示されているので注意してほしい。

### 6.1.2. リストに行が空く

[http://johnmacfarlane.net/pandoc/README.html#compact-and-loose-lists](http://johnmacfarlane.net/pandoc/README.html#compact-and-loose-lists)

たとえば、

~~~
- list 1
- list 2
 	- list 2 - 1
 	- list 2 - 2
 		- list 2 - 2 - 1
 		- list 2 - 2 - 2
 	- list 2 - 3
 	- list 2 - 4
- list 3
- list 4
~~~

のように書いてリッチテキストに変換したあと、再度markdownに変換したときに、

~~~
- list 1
- list 2
    - list 2 - 1
    - list 2 - 2
        - list 2 - 2 - 1
        - list 2 - 2 - 2

    - list 2 - 3
    - list 2 - 4

- list 3
- list 4
~~~~

このような形で変換される。

### 6.1.3. 引用のネスト
[http://johnmacfarlane.net/pandoc/README.html#block-quotations](http://johnmacfarlane.net/pandoc/README.html#block-quotations)

~~~
> 文章
>
> > ネストされた引用を扱うためには上に一行あけるようにする
~~~

少し通常と書き方が異なるので注意。詳しくは上記URL先を参照。

### 6.1.4. tableのalign

リッチテキストからmarkdownに戻したときにalign属性が無効となる。そもそもmarkdownで表を書くのはおすすめしないので、あまり問題はないと思われるが。

## 6.2. 画像はそのまま挿入できる

Markdown記法では画像を挿入する場合以下のように記述する。

	![](image.png)

madeverでもこの記述に対応しているが、Drag&Dropで挿入した画像でも問題なく扱えるようになっている。

以下の画像のようにmarkdownの文書でも画像はDrag&Dropして文書に挿入すれば、リッチテキストに変換してもそのまま表示されるようになっている。

![](/Users/sandai/dev/sandai/madever/sample/img13.png)

## 6.3. 結局どうすればいいか

- 文末のバックスラッシュ(`\`)は改行であること
- リストは空行ができること
- 引用のネストは通常と異なること
- 画像はMarkdown記法で挿入しなくても良いこと

これらのことがわかればあとは基本的に問題ない。

# Contact

[https://twitter.com/sandai](https://twitter.com/sandai)

<sandai310@gmail.com>

# History

21/06/2012 公開
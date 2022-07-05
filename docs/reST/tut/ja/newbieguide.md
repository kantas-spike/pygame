# Pygameの初心者向けガイド

<div class="title" markdown="1">

A Newbie Guide to pygame

</div>

## Pygameの初心者向けガイド

もしくは、 **私が試行錯誤の末に学んだ、あなたがする必要のないこと、**

もしくは、 **私が学んだ、心配するのをやめて、blit を好きになる方法**

[Pygame](https://www.pygame.org/) は [SDL](http://libsdl.org)
のpythonラッパーです。 Pete Shinners によって作成されました。 pygame
を使うと、ゲームや他のマルチメディア アプリケーションを Python で書け、
SDLがサポートする Windows や Linux, Mac などの
プラットフォームでそのまま動作することを意味します。

Pygame は学習しやすいかもしれませんが、
グラフィックプログラミングの世界は初心者には、かなりわかりにくいものです。
過去1年の間、pygameとその前身のPySDLに取り組む中で、
私が得た実用的な知識を抽出しようと思い、これを書きました。
注意事項を重要度の高い準に並べましたが、
どのヒントがどの程度重要かは、あなたの経歴やプロジェクトの詳細に依存します。

### Pythonでの作業を快適にする

もっとも重要な事は、自身をもってPythonを使えるようになることです。
グラフィックプログラミングのような複雑なものを学ぶには、
使用する言語にも慣れていなければ、本当に大変な作業となります。
テキストファイルを解析するような、小さなノングラフィカルナプログラムや、
推理ゲームや日記を書くプログラムなどをPythonで書きましょう。
文字列やリストの操作に慣れましょう。文字列やリストの split、slice や
結合方法を学びましょう。 `import`
の仕組みについて知りましょう。複数のソースファイルにまたがるプログラムを書いてみましょう。
自分で関数を書いて、数値や文字の操作を練習しましょう。両者の変換方法を学びましょう。
リストや辞書を使うための構文が自然に身につくようにしましょう。
リストをsliceしたり、キーのセットをソートしたりする必要があるときに、
いちいちドキュメントにアクセスする必要はないでしょう。
ファイルパスの使い方に慣れておくと、後でアセットのロードやセーブファイルの作成に便利です。

トラブルに見舞われたとき、ネットで直接助けを求める誘惑に負けないようにしましょう。
その代わりに、インタプリタを起動して数時間問題と格闘したり、
print文やデバッグツールを使ってコードのどこが問題なのかを調べたりしてください。
公式の [Python documentation](https://docs.python.org/3/) を調べたり、
エラーメッセージをググってその意味を理解したりする習慣を身につけましょう。

とてつもなく退屈に聞こえるかもしれませんが、pythonに慣れることで得られる自信は、
ゲームを書くときに素晴しい効果を発揮します。
pythonのコードを自然なものにするために費やす時間は、
実際のコードを書くときに節約できる時間に比べたら、たいしたことはないでしょう。

### pygameのどの部分が本当に必要か認識しましょう

Pygameのドキュメントのインデックスの一番上にある、ごちゃごちゃしたクラスを見ていると、混乱するかもしれません。
重要なのは、関数のごく一部で多くのことができるということを認識することです。
多くのクラスはほとんど使うことはないでしょう。私は一年間で、`Channel`,
`Joystick`, `cursors`, `surfarray` や `version`
関数を触ったことがありません。

### サーフェスが何か知りましょう

pygameの最重要な部分はサーフェスです。サーフェスは、白紙の紙切れと思えばいいんです。
サーフェスを使って沢山のことができます。線を描いたり、色を塗ったり、
イメージをコピーしたり、個別のピクセルを読み書きしたりなどえす。
サーフェスはどんなサイズ(無理のない範囲で)でもよく、いくつでも(これも無理のない範囲で)持つことができます。
`pygame.display.set_mode()` で作成するサーフェスは特別です。
この「ディスプレイサーフェス」は画面を表します。あなたの行うことはすべて、このユーザー画面に表示されます。

それでは、どうやってサーフェスを作るのでしょうか?
既に言及していますが、特別な\`ディスプレイサーフェス\`は
`pygame.display.set_mode()` で作成します。
イメージを持つサーフェスは、`pygame.image.load()` で作成できます。
そして、テキストを持つサーフェスは、 `pygame.font.Font.render()`
で作成できます。 何も持たないサーフェスさえも `pygame.Surface()`
で作成できます。

ほとんどのサーフェス関数はあまり重要ではありません。
学ぶべきは、`.Surface.blit()`, `.Surface.fill()`, `.Surface.set_at()` と
`.Surface.get_at()` です。 これらを覚えれば大丈夫です。

### Surface.convert() を使いましょう

最初に `.Surface.convert()` のドキュメントを読んだとき、
心配するようなことはないと思いました。
「私はPNGを使うだけなので、すべて同じフォーマットになるから、
`convert()` する必要はありません」と。
私はとても、とても間違っていたとわかりました。

`convert()` が参照する'フォーマット'とは、 PNGやJPEG、GIFのような
*ファイル* フォーマットではありません。
そのフォーマットは、\`pixelフォーマット\`と呼ばれるものです。
これは、サーフェスが特定のピクセル内の個別の色を記録する特殊な方法を示すものです。
もし、サーフェスフォーマットがディスプレイフォーマットと同じでない場合、
blit
の度に、SDLはオンザフライで変換する必要があります。これはかなり時間のかかる処理です。
この説明について心配しすぎる必要はありません。blitの時にスピードが必要な場合は、
`convert()` が必要であると、ただ覚えてください。

どのように convert を使うのでしょうか? `.image.load()`
関数でサーフェスを作成した後に、 ただconvertを呼びだしましょう。
以下を呼び出す代りに、

> surface = pygame.image.load('foo.png')

以下を呼び出します。

> surface = pygame.image.load('foo.png').convert()

簡単です。イメージをディスクからロードした時に、サーフェスごとに一度だけ呼び出すだけです。
`convert()`
の呼び出しにより、blitの速度が約6倍になりました。この結果に満足するでしょう。

`convert()`
を使いたくない唯一の場面は、画像の内部形式を完全に制御する必要がある場合だけです。
例えば、画像変換プログラムなどを書いていて、
出力ファイルのピクセルフォーマットが入力ファイルと同じであることを確認する必要がある場合です。
もし、ゲームを書いていて、スピードが必要なら、`convert()`
を使いましょう。

### 時代遅れだったり、陳腐化したり、必須でないアドバイスには注意が必要です

Pygame は 2000年代初頭から存在しており、そこから大きく変化しています。
フレームワーク自体も、広大なコンピューティング環境全体もです。
このガイドも含め、あなたが読んだ資料の日付を必ず確認していください。
古いアドバイスはうのみにしないでください。
ここでは、わたしに刺さった一般的なアドバイスを紹介します。

**ダーティ Rect と パフォーマンストリック**

Pygameの古いドキュメントやオンラインガイドを読むと、パフォーマンスのために、
画面のダーティな部分のみ更新すること強調しているのを見ることがあります。
(この文脈のダーティは、前のフレームが描画された後に、領域が変更されたことを意味します。)

一般に、スクロールする背景を持たない場合、あるいは、
pygameが処理できないため画面の背景色を毎フレーム描画できない場合に、
`pygame.display.flip()` の代りに、矩形のリストとともに
`pygame.display.update()` を呼び出すことができます。
pygameのいくつかはAPIはこのパラダイムをサポートするようにデザインされています。
(例えば、`pygame.sprite.RenderUpdates`)
これはpygameの初期にはとても意味のあることでした。

2022年現在では、ほとんどのデスクトップコンピュータが
60FPS以上でディスプレイをリフレッシュできるほど高性能になっています。
カメラが動いたり、背景が動いたりしても、ゲームが60FPSで、まったく問題なく動作します。
現在では、CPUの性能も上り、安心して `display.flip()` を利用できます。

とはいえ、この古いテクニックが、数FPS余計に引き出すのに有効な場合もあります。
例えば、アステロイドやスペースインベーダーのようなシングルスクリーンのゲームです。
以下は、その大まかな手順になります:

スクリーンのフレーム全体を毎回アップデートする代りに、最後のフレームから変更された部分のみ更新します。
これは、更新された矩形をリストで管理し、 フレーム終了時に
`update(the_dirty_rectangles)` を呼び出すことで実現します。
動くスプライトの詳細は以下:

-   スプライトを消去するために、スプライトの現在位置上に背景を転送します。
-   スプライトの現在位置の矩形を dirty_rects に追加します。
-   スプライトを移動します。
-   スプライトを新しい位置に描画します。
-   スプライトの新しい位置の矩形を dirty_rects に追加します。
-   `display.update(dirty_rects)` を呼び出します。

このテクニックは、最近のCPUでパフォーマンスの高い2Dゲームを作るために必須ではありませんが、
それでも、知っておくと便利です。
また、最適化されていないレンダリングロジックで誤ってゲームパフォーマンスを低下させるやり方は
まだたくさんあります。
例えば、最新のハードウェアでも、ディスプレイサーフェスのピクセルごとに
`set_at` を呼びだすのは遅すぎるでしょう。
パフォーマンスに気を配ることは、今でも必要なことです。

ただ、「コードのパフォーマンスを修正する1つの巧妙なトリック」というものはそれほど多くありません。
全てのゲームに違いがあり、それぞれのタイプのゲームで、
異なる問題とそれを解決するための異なるアルゴリズムがあります。
2Dゲームのコードが適切なフレームレートを達成できない場合、
その根本的な原因は、アルゴリズムが悪いか、
基本的なゲームデザインパターンを誤解していることが判明することがほとんどです。

パフォーマンスに問題がある場合、まず、ゲームループ内でファイルを繰り返しロードしていないか確認してください。
次に、コードのプロファイリングを行うオプション利用し、最も時間を消費しているものを見つけます。
ゲームが遅い原因について、ある程度の知識を得たら、
インターネット(google経由)や pygame
コミュニティーに、もっと良いアルゴリズムがないか聞いてみてください。

**HWSURFACE と DOUBLEBUF**

`.display.set_mode()` の HWSURFACE
フラグは、pygameのバージョン2.0.0以降、何もしません!
(信じられないなら、ドキュメントチェックしてください。)

使う理由はありません。 pygameのバージョン1 でさえ、
その効果はかなり微妙で、ほとんどの pygameユーザーが誤解しています。
不幸にも、このフラグは決して魔法のスピードアップフラグではありませんでした。

DOUBLEBUF
フラグはまだ使い道がありますが、こちらも魔法の高速化フラグではありません。

**スプライトクラス**

もし、使いたくなければ、組み込みの `.Sprite` や `.Group`
クラスを使う必要はありません。 多くのチュートリアルで、 `Sprite` は
pygameの基本的な "GameObject"であり、
他の全てのオブジェクトはそこから派生するように見えるかもしれません。
しかし、実際には 追加の便利メソッドを持つ `Rect` と `Surface`
のラッパーにすぎません。
スプライトよりも、ゲームのコアロジックとクラスをゼロから書いた方が直感的で楽しいと思うかもしれません。

### 6つのルールはありません

### 副次的な問題に気を取られてはいけません

新米のゲームプログラマは、ゲームの成功にそれほど重要でない問題を心配することに時間をかけすぎです。
二次的な問題を正しく解決したいという気持は理解できますが、
ゲーム制作の初期段階では、重要な問題が何なのか、どのような答えを選べばいいのか、それすらもわかりません。
その結果、無駄な手間が多くなってしまいます。

例えば、画像ファイルをどのように整理するかという問題を考えましょう。
フレームごとにグラフィックファイルを持つべきでしょうか?
それとも、スプライトごとに持つべきでしょうか?
それとも、すべての1つのアーカイブにまとめるべきでしょうか?
多くのプロジェクトで、このような質問をメーリングリストに投げかけ、
その答えを議論し、プロファイリングし、などなど、多くの時間を浪費してきました。
これは二次的な問題です。議論している暇があったら、実際のゲームコーディングに費やすべきでした。

ここでの洞察は、書ききれなかった完璧なソリューションよりも、
実際に実装された「かなり良い」ソリューションの方がはるかに良いということです。

### Rectはあなたの友達です

Pete Shinners'
のラッパーは、クールなアルファ効果と速いブリット速度を備えているかもしれませんが、
私がpygameで好きな部分はローレベルの `.Rect` クラスです。
Rectはただの四角形です。左上の頂点の位置と、幅、高さだけで定義されます。
多くのpygame
関数は、引数にrectを指定できます。rectと同じ値をもつシーケンスである
<span class="title-ref">rectstyles</span> も引数にとります。 もし、10,20
と 40,50の間に定義され、矩形が必要な場合は、以下のように作成できます:

    rect = pygame.Rect(10, 20, 30, 30)
    rect = pygame.Rect((10, 20, 30, 30))
    rect = pygame.Rect((10, 20), (30, 30))
    rect = (10, 20, 30, 30)
    rect = ((10, 20, 30, 30))

もし、最初の3つの方式を使えば、Restのユーティリティ関数も利用できます。
ユーティリティ関数には、move、shrink や inflate や、
2つのrectの和をみつける関数や、各種衝突判定関数が含まれます。

例えば、(x,y)地点を含む全てのスプライトのリスト取得したいとします。
ここでいう(x,y)はたぶんプレーヤーのクリック位置や弾の現在位置になります。
もし、スプライトが .rect
メンバーを持っていれば簡単です。ただ以下のようになります:

> sprites_clicked = \[sprite for sprite in all_my_sprites_list if
> sprite.rect.collidepoint(x, y)\]

rectは、引数に指定できるということ以外は、サーフェスやグラフィックスの関数と何も関係がありません。
グラフィックとは関係ないが、四角形として定義する必要がある場所で、rectを使えます。
プロジェクトの度に、私は、rectが必要になると思ってもいなかった場所に、
rectが使われていることを何度か発見します。

### ピクセル単位の完璧な衝突判定で悩まない

スプライトを動かし、互いにぶつかり合っているかを知る必要があります。
次のように書きたくなります。

-   rectが衝突しているかチェックします。もし衝突していなければ無視します。
-   重なり合う領域の各ピクセルについて、両方のスプライトの該当ピクセルが不透明であるか確認します。もし不透明なら、衝突しています。

スプライトマスクのAND処理など、他の方法もありますが、 pygame
ではどの方法であっても処理に時間がかかりすぎるでしょう。

ほとんどのゲームでは、'sub-rect collision'を行うのが良いでしょう。
実際の画像より小さいrectを各スプライトに作成し、それを衝突検知に使用します。
この方法はより速く、ほとんどのケースで、プレーヤーはその不正確さに気付かないでしょう。

### イベントサブシステムを管理する

pygameのイベントシステムはちょっとトリッキーです。
入力デバイス(キーボード、マウスやジョイスティック)が何をしているか知るには、
2つの異なる方法があります。

1つ目の方法は、デバイスの状態を直接確認する方法です。
これは、例えば、`pygame.mouse.get_pos()` や `pygame.key.get_pressed()`
を呼び出すことで行います。 これは、 *関数を呼んだ時点*
のデバイス状態を教えてくれます。

2つ目の方法は、SDLのイベントキューを使う方法です。
このキューはイベントのリストです。
イベントは検知された時にリストに追加され、読み取られるとキューから削除されます。

それぞれの方式にはメリットとデメリットがあります。状態チェック (方法1)
は正確です。 与えられたインプットが作成された時に知ることができます。
もし、 `mouse.get_pressed([0])` が 1 ならば、
マウスの左ボタンが今この瞬間に押されていることを意味します。
イベントキューは、過去のどこかでマウスが押されたことを、ただ知らせるだけです。
もし、キューのチェックが頻繁すると、良いのですが、
他のコードによって、キューのチェックが遅れると、入力待ちの時間が長くなります。

状態チェック方式のもう一つの利点は「コード化」を容易に検出できることです。
つまり、複数の状態が同時に検出できます。 例えば、 `t` と `f`
キーが同時に押されたかどうかを知りたければ、次のようにチェックします:

    if key.get_pressed[K_t] and key.get_pressed[K_f]:
        print("Yup!")

キュー方式の場合、各キー押下イベントが完全に分けられたイベントとしてキューに到着します。
そのため、 `t` キーが押されて、 `f` キーがまだ出てきいないことを、 `f`
キーをチェックしながら、覚えておく必要があります。すこし複雑ですね。

しかし、状態チェック方式には、大きな1つの欠点があります。
この方式は、関数が呼ばれた瞬間のデバイスの状態を通知するだけです。
もし、 `mouse.get_pressed()`
を呼ぶ直前にユーザーがマウスボタンを押して、ボタンを離した場合、
マウスボタンは0を返します。 `get_pressed()`
は完全にボタン押下を見逃します。 `MOUSEBUTTONDOWN` と `MOUSEBUTTONUP`
の2つのイベントは、まだイベントキューには残っているでしょう。
イベントの取得と処理を待っている状態です。

教訓は、「自分の要求を満す方式を選ぶこと」です。
もし、ループ内であまり多くのことが行われていない場合、 例えば、
`while True` のループ内で入力を待っているだけの場合は、 `get_pressed()`
や 他のステート関数を使用すると、遅延が小さくなります。
一方、すべてのキー入力が重要だが、遅延はそれほど重要でない場合、
例えば、ユーザーがエディットボックスになにかを入力している場合は、イベントキューを使用します。
キー入力のタイミングが多少遅れるかもしれませんが、少なくともすべてのキー入力を取得することができます。

`event.poll()` vs. `wait()` についての注意
入力を待っている間、プログラムがブロックされないので、 `poll()`
の方が良く見えるかもしれません。 `wait()`
はイベントを受けとるまで、プログラムを一時停止します。 しかし、 `poll()`
は利用できるCPU時間を100%消費してしまいます。 そして、イベントキューを
`NOEVENTS` でいっぱいにします。
関心のあるイベントタイプのみ選択するために、 `set_blocked()`
を使いましょう。 キューがより管理しやすくなります。

イベントキューについてのもう1つの注意
イベントキューを使用しない場合でも、ユーザーがキーを押したり、マウスでウィンドウを操作すると、
バックグラウンドでイベントがいっぱいになってしまうので、定期的にクリアする必要があります。
Windowsの場合、キューをクリアせずに、長時間ゲームを続けると、
オペレーティングシステムがフリーズしたと判断し、
「アプリケーションが応答していません」というメッセージがが表示されます。

`event.get()` を繰り返すか、フレームごとに一度だけ、 `event.clear()`
を呼び出すことで回避できます。

### カラーキー vs. アルファ

この2つの技術には多くの混乱があり、その多くは用語に起因しています。

'Colorkey blitting' は pygame にある画像の特定色の全てのピクセルを、
特定色が何色であったとしても透明にするように指示します。
画像の残りの部分が描画された時に、これらの透明なピクセルは描画されないので、
背景が隠れることはありません。
これは、長方形でないスプライトを作る方法です。 単純に、
`.Surface.set_colorkey()` を呼びだし、引数に RGBのタプルを渡します。
例えば (0,0,0)を渡した場合、元画像の黒色の全ピクセルが透明になります。

'Alpha' は別物です。2つの意味があります。 'Image
alpha'は画像全体に適用されます。おそらくあなたが望むものでしょう。
正しくは「半透明」として知られていますが、
アルファは元画像の各ピクセルを *部分的に* 不透明化させます。
例えば、サーフェスのアルファを192に設定し、それを背景の上に描画するとします。
各ピクセルの色の3/4が元画像から、1/4が背景から来ることになります。
アルファは255から0まであり、0は完全に透明で、255は完全に不透明になります。
カラーキーとアルファを描画時に組み合せて、
一部は完全に透明で、他の部分は半透明の画像を作成することができます。

'Per-pixel alpha'はもう1つの種類のアルファです。これはより複雑です。
基本的に、元画像の各ピクセルは0から255までの独自のアルファ値を持ちます。
したがって、各ピクセルは背景の上に描画されたときに、異なる不透明度を持つことができます。
このタイプのアルファは、カラーキーと混ぜることはできません。
画像ごとのアルファ値よりも優先されます。
ピクセル単位のアルファはゲームではほんとど使われません。
使うためには元画像をグラフィックエディタで *特別なアルファチャンネル*
で保存する必要があります。 複雑なので、まだ使わないでください。

### ソフトウェアアーキテクチャ、デザインパターンとゲーム

コードに書くことに慣れ、複雑な問題でも手助けなしで解決できるようになり、
pygameのほとんどのモジュールの使い方を理解できるようになったのに、
大きなプロジェクトに取り組むと、時間が立つにつれて常に混乱し、維持するのが難しくなることがあります。
これは様々な形で現われます。
例えば、ある場所のバグを修正すると、いつも、別の場所に新しいバグが発生するように見えます。
コードの行き先を決めるのが大変になる。
新しいものを追加すると、他の多くのコードを書き直さなければならないことが頻繁にあります。などです。
最終的に、このままではいけないと思い、新しいことを始めることになります。

これはよくある問題で、イライラさせられるとおもあります。
プログラミングのスキルは向上しているのに、漠然とした組織的な問題で、ゲームを完成させることができません。

そこで、ソフトウェアアーキテクチャとデザインパターンという考え方に行き着きます。
pygameの "標準"
ベーステンプレート(これと同等のバリエーションは沢山あるので、
細かいことはあまり気にしないでください)はよくご存知でしょう。:

    import pygame

    pygame.init()

    screen = pygame.display.set_mode((1280,720))

    clock = pygame.time.Clock()

    while True:
        # Process player inputs.
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                pygame.quit()
                raise SystemExit

        # Do logical updates here.
        # ...

        screen.fill("purple")  # Fill the display with a solid color

        # Render the graphics here.
        # ...

        pygame.display.flip()  # Refresh on-screen display
        clock.tick(60)         # wait until next frame (at 60 FPS)

初期設定を行い、ループを開始します。そして、入力を収集し、ゲームのロジックを処理し、現在のフレームを描画します。
これをプログラムが終了するまで繰り返します。
ここで示した、更新、描画、ループの待機は、
実は、ほとんどのゲームの骨組として機能するデザインパターンです。
簡潔で、整理されて、上手く動くからこそ、多くで利用されています。
(また、ゲームロジックとレンダリングルーチンを厳密に分けるという、重要だが見逃しがちな設計上の特徴もあります。
この決定により、オブジェクトの更新とレンダリングの並行実行に起因する
潜在的なバグの可能性を全て防ぐことができます。これは素晴しいことです。)

このようなデザインパターンは、ゲームやソフトウェア開発全般で頻繁に使用されることがわかっています。
ゲームに特化した素晴らしいリソースとしては、 'Game Programming Patterns'
という短い無料の電子書籍がおすすめです。
この本では、便利なパターンとそれを採用したくなるような具体的なシチュエーションを沢山とりあげています。
この本を読めばすぐに優れたコーダーになるわけではありませんが、
ソフトウェアアーキテクチャに関する理論を学ぶことは、
停滞期を脱し、より大きなプロジェクトに自信を持って取り組む上で大きな助けとなります。

### pythonのやり方で物事に取り組みましょう

最後のノートです。(これは、最も重要なことではなく、ただ最後に出てきただけです。)
pygame は SDLをかなり軽量にしたラッパーです。
SDLはさらに、あなたのネイティブOSのグラフィックス呼び出し用の軽量ラッパーです。
もし、あなたのコードがまだ遅くて、上述したようなことを対処済みなら、
問題はPythonでデータを扱う方法にある可能性はかなり高いです。
ある種のイディオムを使うと、何をやってもPythonでは遅くなります。
幸いなことに、pythonは非常に明快な言語です。
もし、コードの一部が不恰好に見えたり、扱いにくかったりしたら、その速度も改善できる可能性があります。
pygameが他のフレームワークやエンジンよりも遅いと思われる理由と、
それが実際に何を意味するかについての深い洞察は、 [Why Pygame is
Slow](https://blubberquark.tumblr.com/post/630054903238262784/why-pygame-is-slow)
を読んでください。
また、本当にパフォーマンスの問題で困っているのであれば、
[cProfile](https://docs.python.org/3/library/profile.html)
(またはcProfile用のビジュアライザーである
[SnakeViz](https://jiffyclub.github.io/snakeviz/))
のようなプロファイラが
ボトルネックの特定に役立ちます。(コードのどの部分の実行に最も長い時間がかかっているかを教えてくれます)。
とはいえ、早まった最適化は諸悪の根源です。すでに十分な速度が出てるのであれば、
より速くしようとコードを苦しめる必要はありません。
十分速いのなら、そのままにしておけばいいのです。:)

さあ、どうぞ。これで私が知っているpygameの使い方は、実質的にすべてわかったことになります。
さあ、ゲームを書きましょう!!

------------------------------------------------------------------------

*David Clark は熱心なpygameユーザーであり、Pygame
Codeの編集者でもあります。コミュニティーが投稿したPythonゲームコードのショーケースである
Pygame Code Repository のエディタです。彼はまた、 Twitch
という全く平均的な pygame アーケードゲームの作者でもあります。*

*このガイドは2022年に大幅に改訂を行いました。*
.. TUTORIAL: David Clark's Newbie Guide To Pygame

.. include:: common.txt

.. comment
    **************************
    Newbie Guide to Pygame
    **************************

**************************
  Pygameの初心者向けガイド
**************************

.. title:: A Newbie Guide to pygame

.. comment
    A Newbie Guide to pygame
    ========================

Pygameの初心者向けガイド
========================

.. comment
    or **Things I learned by trial and error so you don't have to,**

    or **How I learned to stop worrying and love the blit.**


もしくは、 **私が試行錯誤の末に学んだ、あなたがする必要のないこと、**

もしくは、 **私が学んだ、心配するのをやめて、blit を好きになる方法**

.. comment
    Pygame_ is a python wrapper for SDL_, written by Pete Shinners.  What this
    means is that, using pygame, you can write games or other multimedia
    applications in Python that will run unaltered on any of SDL's supported
    platforms (Windows, Linux, Mac, and others).

Pygame_ は SDL_ のpythonラッパーです。 Pete Shinners によって作成されました。
pygame を使うと、ゲームや他のマルチメディア アプリケーションを Python で書け、
SDLがサポートする Windows や Linux, Mac などの プラットフォームでそのまま動作することを意味します。

.. comment
    Pygame may be easy to learn, but the world of graphics programming can be
    pretty confusing to the newcomer.  I wrote this to try to distill the practical
    knowledge I've gained over the past year or so of working with pygame, and its
    predecessor, PySDL.  I've tried to rank these suggestions in order of
    importance, but how relevant any particular hint is will depend on your own
    background and the details of your project.

Pygame は学習しやすいかもしれませんが、
グラフィックプログラミングの世界は初心者には、かなりわかりにくいものです。
過去1年の間、pygameとその前身のPySDLに取り組む中で、
私が得た実用的な知識を抽出しようと思い、これを書きました。
注意事項を重要度の高い準に並べましたが、
どのヒントがどの程度重要かは、あなたの経歴やプロジェクトの詳細に依存します。

.. comment
    Get comfortable working in Python.
    ----------------------------------

Pythonでの作業を快適にする
----------------------------------

.. comment
    The most important thing is to feel confident using python. Learning something
    as potentially complicated as graphics programming will be a real chore if
    you're also unfamiliar with the language you're using. Write a few sizable
    non-graphical programs in python -- parse some text files, write a guessing
    game or a journal-entry program or something. Get comfortable with string and
    list manipulation -- know how to split, slice and combine strings and lists.
    Know how ``import`` works -- try writing a program that is spread across
    several source files.  Write your own functions, and practice manipulating
    numbers and characters; know how to convert between the two.  Get to the point
    where the syntax for using lists and dictionaries is second-nature -- you don't
    want to have to run to the documentation every time you need to slice a list or
    sort a set of keys.  Get comfortable using file paths -- this will come in handy
    later when you start loading assets and creating save files.

もっとも重要な事は、自身をもってPythonを使えるようになることです。
グラフィックプログラミングのような複雑なものを学ぶには、
使用する言語にも慣れていなければ、本当に大変な作業となります。
テキストファイルを解析するような、小さなノングラフィカルナプログラムや、
推理ゲームや日記を書くプログラムなどをPythonで書きましょう。
文字列やリストの操作に慣れましょう。文字列やリストの split、slice や 結合方法を学びましょう。
``import`` の仕組みについて知りましょう。複数のソースファイルにまたがるプログラムを書いてみましょう。
自分で関数を書いて、数値や文字の操作を練習しましょう。両者の変換方法を学びましょう。
リストや辞書を使うための構文が自然に身につくようにしましょう。
リストをsliceしたり、キーのセットをソートしたりする必要があるときに、
いちいちドキュメントにアクセスする必要はないでしょう。
ファイルパスの使い方に慣れておくと、後でアセットのロードやセーブファイルの作成に便利です。

.. comment
    Resist the temptation to ask for direct help online when
    you run into trouble.  Instead, fire up the interpreter and play with the
    problem for a few hours, or use print statements and debugging tools to find out
    what's going wrong in your code.  Get into the habit of looking things up in the
    official `Python documentation`_, and Googling error messages to figure out what
    they mean.

トラブルに見舞われたとき、ネットで直接助けを求める誘惑に負けないようにしましょう。
その代わりに、インタプリタを起動して数時間問題と格闘したり、
print文やデバッグツールを使ってコードのどこが問題なのかを調べたりしてください。
公式の `Python documentation`_ を調べたり、
エラーメッセージをググってその意味を理解したりする習慣を身につけましょう。

.. comment
    This may sound incredibly dull, but the confidence you'll gain through your
    familiarity with python will work wonders when it comes time to write your
    game.  The time you spend making python code second-nature will be nothing
    compared to the time you'll save when you're writing real code.

とてつもなく退屈に聞こえるかもしれませんが、pythonに慣れることで得られる自信は、
ゲームを書くときに素晴しい効果を発揮します。
pythonのコードを自然なものにするために費やす時間は、
実際のコードを書くときに節約できる時間に比べたら、たいしたことはないでしょう。

.. comment
    Recognize which parts of pygame you really need.
    ------------------------------------------------

pygameのどの部分が本当に必要か認識しましょう
------------------------------------------------

.. comment
    Looking at the jumble of classes at the top of the pygame documentation index
    may be confusing.  The important thing is to realize that you can do a great
    deal with only a tiny subset of functions.  Many classes you'll probably never
    use -- in a year, I haven't touched the ``Channel``, ``Joystick``, ``cursors``,
    ``surfarray`` or ``version`` functions.

Pygameのドキュメントのインデックスの一番上にある、ごちゃごちゃしたクラスを見ていると、混乱するかもしれません。
重要なのは、関数のごく一部で多くのことができるということを認識することです。
多くのクラスはほとんど使うことはないでしょう。私は一年間で、``Channel``, ``Joystick``, ``cursors``,
``surfarray`` や ``version`` 関数を触ったことがありません。

.. comment
    Know what a surface is.
    -----------------------

サーフェスが何か知りましょう
------------------------------

.. comment
    The most important part of pygame is the surface.  Just think of a surface as a
    blank piece of paper.  You can do a lot of things with a surface -- you can
    draw lines on it, fill parts of it with color, copy images to and from it, and
    set or read individual pixel colors on it.  A surface can be any size (within
    reason) and you can have as many of them as you like (again, within reason).
    One surface is special -- the one you create with
    :func:`pygame.display.set_mode()`.  This 'display surface' represents the screen;
    whatever you do to it will appear on the user's screen.

pygameの最重要な部分はサーフェスです。サーフェスは、白紙の紙切れと思えばいいんです。
サーフェスを使って沢山のことができます。線を描いたり、色を塗ったり、
イメージをコピーしたり、個別のピクセルを読み書きしたりなどえす。
サーフェスはどんなサイズ(無理のない範囲で)でもよく、いくつでも(これも無理のない範囲で)持つことができます。
:func:`pygame.display.set_mode()` で作成するサーフェスは特別です。
この「ディスプレイサーフェス」は画面を表します。あなたの行うことはすべて、このユーザー画面に表示されます。

.. comment
    So how do you create surfaces?  As mentioned above, you create the special
    'display surface' with ``pygame.display.set_mode()``.  You can create a surface
    that contains an image by using :func:`pygame.image.load()`, or you can make a surface
    that contains text with :func:`pygame.font.Font.render()`.  You can even create a surface that
    contains nothing at all with :func:`pygame.Surface()`.

それでは、どうやってサーフェスを作るのでしょうか?
既に言及していますが、特別な`ディスプレイサーフェス`は ``pygame.display.set_mode()`` で作成します。
イメージを持つサーフェスは、:func:`pygame.image.load()` で作成できます。
そして、テキストを持つサーフェスは、 :func:`pygame.font.Font.render()` で作成できます。
何も持たないサーフェスさえも :func:`pygame.Surface()` で作成できます。

.. comment
    Most of the surface functions are not critical. Just learn :meth:`.Surface.blit()`,
    :meth:`.Surface.fill()`, :meth:`.Surface.set_at()` and :meth:`.Surface.get_at()`, and you'll be fine.

ほとんどのサーフェス関数はあまり重要ではありません。
学ぶべきは、:meth:`.Surface.blit()`, :meth:`.Surface.fill()`,
:meth:`.Surface.set_at()` と :meth:`.Surface.get_at()` です。
これらを覚えれば大丈夫です。

.. comment
    Use Surface.convert().
    ----------------------

Surface.convert() を使いましょう
--------------------------------

.. comment
    When I first read the documentation for :meth:`.Surface.convert()`, I didn't think
    it was something I had to worry about. 'I only use PNGs, therefore everything I
    do will be in the same format. So I don't need ``convert()``';. It turns out I
    was very, very wrong.

最初に :meth:`.Surface.convert()` のドキュメントを読んだとき、
心配するようなことはないと思いました。
「私はPNGを使うだけなので、すべて同じフォーマットになるから、 ``convert()`` する必要はありません」と。
私はとても、とても間違っていたとわかりました。

.. comment
The 'format' that ``convert()`` refers to isn't the *file* format (i.e. PNG,
JPEG, GIF), it's what's called the 'pixel format'.  This refers to the
particular way that a surface records individual colors in a specific pixel.
If the surface format isn't the same as the display format, SDL will have to
convert it on-the-fly for every blit -- a fairly time-consuming process.  Don't
worry too much about the explanation; just note that ``convert()`` is necessary
if you want to get any kind of speed out of your blits.

``convert()`` が参照する'フォーマット'とは、
PNGやJPEG、GIFのような *ファイル* フォーマットではありません。
そのフォーマットは、`pixelフォーマット`と呼ばれるものです。
これは、サーフェスが特定のピクセル内の個別の色を記録する特殊な方法を示すものです。
もし、サーフェスフォーマットがディスプレイフォーマットと同じでない場合、
blit の度に、SDLはオンザフライで変換する必要があります。これはかなり時間のかかる処理です。
この説明について心配しすぎる必要はありません。blitの時にスピードが必要な場合は、
`` convert()`` が必要であると、ただ覚えてください。

.. comment
    How do you use convert? Just call it after creating a surface with the
    :func:`.image.load()` function. Instead of just doing::

        surface = pygame.image.load('foo.png')

    Do::

        surface = pygame.image.load('foo.png').convert()

どのように convert を使うのでしょうか?
:func:`.image.load()` 関数でサーフェスを作成した後に、 ただconvertを呼びだしましょう。
以下を呼び出す代りに、

    surface = pygame.image.load('foo.png')

以下を呼び出します。

    surface = pygame.image.load('foo.png').convert()

.. comment
    It's that easy. You just need to call it once per surface, when you load an
    image off the disk.  You'll be pleased with the results; I see about a 6x
    increase in blitting speed by calling ``convert()``.

簡単です。イメージをディスクからロードした時に、サーフェスごとに一度だけ呼び出すだけです。
``convert()`` の呼び出しにより、blitの速度が約6倍になりました。この結果に満足するでしょう。

.. comment
    The only times you don't want to use ``convert()`` is when you really need to
    have absolute control over an image's internal format -- say you were writing
    an image conversion program or something, and you needed to ensure that the
    output file had the same pixel format as the input file.  If you're writing a
    game, you need speed.  Use ``convert()``.

``convert()`` を使いたくない唯一の場面は、画像の内部形式を完全に制御する必要がある場合だけです。
例えば、画像変換プログラムなどを書いていて、
出力ファイルのピクセルフォーマットが入力ファイルと同じであることを確認する必要がある場合です。
もし、ゲームを書いていて、スピードが必要なら、``convert()`` を使いましょう。

.. comment
    Be wary of outdated, obsolete, and optional advice.
    ---------------------------------------------------

時代遅れだったり、陳腐化したり、必須でないアドバイスには注意が必要です
----------------------------------------------------------------------

.. comment
    Pygame has been around since the early 2000s, and a lot has changed since then --
    both within the framework itself and within the broader computing landscape as a
    whole. Make sure to check the dates on materials you read (including this guide!),
    and take older advice with a grain of salt. Here are some common things that
    stick out to me:

Pygame は 2000年代初頭から存在しており、そこから大きく変化しています。
フレームワーク自体も、広大なコンピューティング環境全体もです。
このガイドも含め、あなたが読んだ資料の日付を必ず確認していください。
古いアドバイスはうのみにしないでください。
ここでは、わたしに刺さった一般的なアドバイスを紹介します。

.. comment
    **Dirty Rects & performance 'tricks'**

**ダーティ Rect と パフォーマンストリック**

.. comment
    When you read older bits of pygame documentation or guides online, you may see
    some emphasis on only updating portions of the screen that are dirty, for the
    sake of performance (in this context, "dirty" means the region has changed since
    the previous frame was drawn).

Pygameの古いドキュメントやオンラインガイドを読むと、パフォーマンスのために、
画面のダーティな部分のみ更新すること強調しているのを見ることがあります。
(この文脈のダーティは、前のフレームが描画された後に、領域が変更されたことを意味します。)

.. comment
    Generally this entails calling :func:`pygame.display.update()` (with a list of
    rects) instead of :func:`pygame.display.flip()`, not having scrolling backgrounds,
    or even not filling the screen with a background color every frame because pygame
    supposedly can't handle it.  Some of pygame's API is designed to support this
    paradigm as well (e.g. :func:`pygame.sprite.RenderUpdates`), which made a lot of
    sense in the early years of pygame.

一般に、スクロールする背景を持たない場合、あるいは、
pygameが処理できないため画面の背景色を毎フレーム描画できない場合に、
:func:`pygame.display.flip()` の代りに、矩形のリストとともに :func:`pygame.display.update()` を呼び出すことができます。
pygameのいくつかはAPIはこのパラダイムをサポートするようにデザインされています。
(例えば、:func:`pygame.sprite.RenderUpdates`) これはpygameの初期にはとても意味のあることでした。

.. comment
    In the present day (2022) though, most modest desktop computers are powerful enough to
    refresh the entire display once per frame at 60 FPS and beyond.  You can have a moving
    camera, or dynamic backgrounds and your game should run totally fine at 60 FPS.  CPUs are
    more powerful nowadays, and you can use ``display.flip()`` without fear.

2022年現在では、ほとんどのデスクトップコンピュータが
60FPS以上でディスプレイをリフレッシュできるほど高性能になっています。
カメラが動いたり、背景が動いたりしても、ゲームが60FPSで、まったく問題なく動作します。
現在では、CPUの性能も上り、安心して ``display.flip()`` を利用できます。

.. comment
    That being said there are still some times when this old technique is still useful
    for squeezing out a few extra FPS. For example, with a single screen game like
    an Asteroids or Space Invaders. Here is the rough process for how it works:

とはいえ、この古いテクニックが、数FPS余計に引き出すのに有効な場合もあります。
例えば、アステロイドやスペースインベーダーのようなシングルスクリーンのゲームです。
以下は、その大まかな手順になります:

.. comment
    Instead of updating the whole screen every frame, only the parts that changed since
    the last frame are updated.  You do this by keeping track of those rectangles in a list,
    then calling ``update(the_dirty_rectangles)`` at the end of the frame.  In detail
    for a moving sprite:

スクリーンのフレーム全体を毎回アップデートする代りに、最後のフレームから変更された部分のみ更新します。
これは、更新された矩形をリストで管理し、
フレーム終了時に ``update(the_dirty_rectangles)`` を呼び出すことで実現します。
動くスプライトの詳細は以下:

.. comment
    * Blit a piece of the background over the sprite's current location, erasing it.
    * Append the sprite's current location rectangle to a list called dirty_rects.
    * Move the sprite.
    * Draw the sprite at its new location.
    * Append the sprite's new location to my dirty_rects list.
    * Call ``display.update(dirty_rects)``

* スプライトを消去するために、スプライトの現在位置上に背景を転送します。
* スプライトの現在位置の矩形を dirty_rects に追加します。
* スプライトを移動します。
* スプライトを新しい位置に描画します。
* スプライトの新しい位置の矩形を dirty_rects に追加します。
*  ``display.update(dirty_rects)`` を呼び出します。

.. comment
    Even though this technique is not required for making performant 2D games with
    modern CPUs, it is still useful to be aware of. There are also still plenty of other ways
    to accidentally tank your game's performance with poorly optimized rendering logic.
    For example, even on modern hardware it's probably too slow to call ``set_at`` once per pixel
    on the display surface. Being mindful of performance is still something you'll have to
    do.

このテクニックは、最近のCPUでパフォーマンスの高い2Dゲームを作るために必須ではありませんが、
それでも、知っておくと便利です。
また、最適化されていないレンダリングロジックで誤ってゲームパフォーマンスを低下させるやり方は
まだたくさんあります。
例えば、最新のハードウェアでも、ディスプレイサーフェスのピクセルごとに
``set_at`` を呼びだすのは遅すぎるでしょう。
パフォーマンスに気を配ることは、今でも必要なことです。

.. comment
    There just aren't that many 'one neat trick to fix your code performance' tips. Every game
    is different and there are different problems and different algorithms to solve them
    efficiently in each type of game. Pretty much every time your 2D game code is failing to hit a
    reasonable frame rate the underlying cause turns out to be bad algorithm or a misunderstanding
    of fundamental game design patterns.

ただ、「コードのパフォーマンスを修正する1つの巧妙なトリック」というものはそれほど多くありません。
全てのゲームに違いがあり、それぞれのタイプのゲームで、
異なる問題とそれを解決するための異なるアルゴリズムがあります。
2Dゲームのコードが適切なフレームレートを達成できない場合、
その根本的な原因は、アルゴリズムが悪いか、
基本的なゲームデザインパターンを誤解していることが判明することがほとんどです。

.. community
    If you are having performance problems, first make sure you aren't loading files repeatedly in your
    game loop, then use one of the many options for profiling your code to find out what is taking up the
    most time. Once you are armed with at least some knowledge on why your game is slow, try asking the
    internet (via google), or the pygame community if they've got some better algorithms to help you out.

パフォーマンスに問題がある場合、まず、ゲームループ内でファイルを繰り返しロードしていないか確認してください。
次に、コードのプロファイリングを行うオプション利用し、最も時間を消費しているものを見つけます。
ゲームが遅い原因について、ある程度の知識を得たら、
インターネット(google経由)や pygame コミュニティーに、もっと良いアルゴリズムがないか聞いてみてください。

.. comment
    **HWSURFACE and DOUBLEBUF**

**HWSURFACE と DOUBLEBUF**

.. comment
    The HWSURFACE :func:`.display.set_mode()` flag does nothing in pygame versions 2.0.0 and
    later (you can check the docs if you don't believe me)!  There's no reason to
    use it anymore.  Even in pygame 1, its effect is pretty nuanced and
    generally misunderstood by most pygame users.  It was never a magic speed-up
    flag, unfortunately.
    DOUBLEBUF still has some use, but is also not a magic speed up flag.

:func:`.display.set_mode()` の HWSURFACE フラグは、pygameのバージョン2.0.0以降、何もしません!
(信じられないなら、ドキュメントチェックしてください。)

使う理由はありません。 pygameのバージョン1 でさえ、
その効果はかなり微妙で、ほとんどの pygameユーザーが誤解しています。
不幸にも、このフラグは決して魔法のスピードアップフラグではありませんでした。

DOUBLEBUF フラグはまだ使い道がありますが、こちらも魔法の高速化フラグではありません。

.. comment
  **The Sprite class**

**スプライトクラス**

.. comment
    You don't need to use the built-in :class:`.Sprite` or :class:`.Group` classes
    if you don't want to.  In a lot of tutorials, it may seem like ``Sprite`` is the
    fundamental "GameObject" of pygame, from which all other objects must derive,
    but in reality it's pretty much just a wrapper around a ``Rect`` and a
    ``Surface``, with some additional convenience methods.  You may find it
    more intuitive (and fun) to write your game's core logic and classes from
    scratch.

もし、使いたくなければ、組み込みの :class:`.Sprite` や :class:`.Group` クラスを使う必要はありません。
多くのチュートリアルで、 ``Sprite`` は pygameの基本的な "GameObject"であり、
他の全てのオブジェクトはそこから派生するように見えるかもしれません。
しかし、実際には 追加の便利メソッドを持つ ``Rect`` と ``Surface`` のラッパーにすぎません。
スプライトよりも、ゲームのコアロジックとクラスをゼロから書いた方が直感的で楽しいと思うかもしれません。

.. comment
    There is NO rule six.
    ---------------------

6つのルールはありません
-----------------------

.. comment
    Don't get distracted by side issues.
    ------------------------------------

副次的な問題に気を取られてはいけません
--------------------------------------

.. comment
    Sometimes, new game programmers spend too much time worrying about issues that
    aren't really critical to their game's success.  The desire to get secondary
    issues 'right' is understandable, but early in the process of creating a game,
    you cannot even know what the important questions are, let alone what answers
    you should choose.  The result can be a lot of needless prevarication.

新米のゲームプログラマは、ゲームの成功にそれほど重要でない問題を心配することに時間をかけすぎです。
二次的な問題を正しく解決したいという気持は理解できますが、
ゲーム制作の初期段階では、重要な問題が何なのか、どのような答えを選べばいいのか、それすらもわかりません。
その結果、無駄な手間が多くなってしまいます。

.. comment
    For example, consider the question of how to organize your graphics files.
    Should each frame have its own graphics file, or each sprite?  Perhaps all the
    graphics should be zipped up into one archive?  A great deal of time has been
    wasted on a lot of projects, asking these questions on mailing lists, debating
    the answers, profiling, etc, etc.  This is a secondary issue; any time spent
    discussing it should have been spent coding the actual game.

例えば、画像ファイルをどのように整理するかという問題を考えましょう。
フレームごとにグラフィックファイルを持つべきでしょうか? それとも、スプライトごとに持つべきでしょうか?
それとも、すべての1つのアーカイブにまとめるべきでしょうか?
多くのプロジェクトで、このような質問をメーリングリストに投げかけ、
その答えを議論し、プロファイリングし、などなど、多くの時間を浪費してきました。
これは二次的な問題です。議論している暇があったら、実際のゲームコーディングに費やすべきでした。

.. comment
    The insight here is that it is far better to have a 'pretty good' solution that
    was actually implemented, than a perfect solution that you never got around to
    writing.

ここでの洞察は、書ききれなかった完璧なソリューションよりも、
実際に実装された「かなり良い」ソリューションの方がはるかに良いということです。

.. comment
    Rects are your friends.
    -----------------------

Rectはあなたの友達です
-----------------------

.. comment
    Pete Shinners' wrapper may have cool alpha effects and fast blitting speeds,
    but I have to admit my favorite part of pygame is the lowly :class:`.Rect` class.
    A rect is simply a rectangle -- defined only by the position of its top left
    corner, its width, and its height.  Many pygame functions take rects as
    arguments, and they also take 'rectstyles', a sequence that has the same values
    as a rect. So if I need a rectangle that defines the area between 10, 20 and
    40, 50, I can do any of the following::

Pete Shinners のラッパーは、クールなアルファ効果と速いブリット速度を備えているかもしれませんが、
私がpygameで好きな部分はローレベルの :class:`.Rect` クラスです。
Rectはただの四角形です。左上の頂点の位置と、幅、高さだけで定義されます。
多くのpygame 関数は、引数にrectを指定できます。rectと同じ値をもつシーケンスである
`rectstyles`も引数にとります。
もし、10,20 と 40,50の間に定義され、矩形が必要な場合は、以下のように作成できます::

    rect = pygame.Rect(10, 20, 30, 30)
    rect = pygame.Rect((10, 20, 30, 30))
    rect = pygame.Rect((10, 20), (30, 30))
    rect = (10, 20, 30, 30)
    rect = ((10, 20, 30, 30))

.. comment
    If you use any of the first three versions, however, you get access to Rect's
    utility functions.  These include functions to move, shrink and inflate rects,
    find the union of two rects, and a variety of collision-detection functions.

もし、最初の3つの方式を使えば、Restのユーティリティ関数も利用できます。
ユーティリティ関数には、move、shrink や inflate や、
2つのrectの和をみつける関数や、各種衝突判定関数が含まれます。

.. comment
    For example, suppose I'd like to get a list of all the sprites that contain a
    point (x, y) -- maybe the player clicked there, or maybe that's the current
    location of a bullet. It's simple if each sprite has a .rect member -- I just
    do::

例えば、(x,y)地点を含む全てのスプライトのリスト取得したいとします。
ここでいう(x,y)はたぶんプレーヤーのクリック位置や弾の現在位置になります。
もし、スプライトが .rect メンバーを持っていれば簡単です。ただ以下のようになります:

    sprites_clicked = [sprite for sprite in all_my_sprites_list if sprite.rect.collidepoint(x, y)]

.. comment
    Rects have no other relation to surfaces or graphics functions, other than the
    fact that you can use them as arguments.  You can also use them in places that
    have nothing to do with graphics, but still need to be defined as rectangles.
    Every project I discover a few new places to use rects where I never thought
    I'd need them.

rectは、引数に指定できるということ以外は、サーフェスやグラフィックスの関数と何も関係がありません。
グラフィックとは関係ないが、四角形として定義する必要がある場所で、rectを使えます。
プロジェクトの度に、私は、rectが必要になると思ってもいなかった場所に、
rectが使われていることを何度か発見します。

.. comment
    Don't bother with pixel-perfect collision detection.
    ----------------------------------------------------

ピクセル単位の完璧な衝突判定で悩まない
--------------------------------------

.. comment
    So you've got your sprites moving around, and you need to know whether or not
    they're bumping into one another. It's tempting to write something like the
    following:

スプライトを動かし、互いにぶつかり合っているかを知る必要があります。
次のように書きたくなります。

.. comment
 * Check to see if the rects are in collision. If they aren't, ignore them.
 * For each pixel in the overlapping area, see if the corresponding pixels from both sprites are opaque. If so, there's a collision.

* rectが衝突しているかチェックします。もし衝突していなければ無視します。
* 重なり合う領域の各ピクセルについて、両方のスプライトの該当ピクセルが不透明であるか確認します。もし不透明なら、衝突しています。

.. comment
    There are other ways to do this, with ANDing sprite masks and so on, but any
    way you do it in pygame, it's probably going to be too slow. For most games,
    it's probably better just to do 'sub-rect collision' -- create a rect for each
    sprite that's a little smaller than the actual image, and use that for
    collisions instead. It will be much faster, and in most cases the player won't
    notice the imprecision.

スプライトマスクのAND処理など、他の方法もありますが、
pygame ではどの方法であっても処理に時間がかかりすぎるでしょう。

ほとんどのゲームでは、'sub-rect collision'を行うのが良いでしょう。
実際の画像より小さいrectを各スプライトに作成し、それを衝突検知に使用します。
この方法はより速く、ほとんどのケースで、プレーヤーはその不正確さに気付かないでしょう。

.. comment
    Managing the event subsystem.
    -----------------------------

イベントサブシステムを管理する
-----------------------------

.. comment
    Pygame's event system is kind of tricky.  There are actually two different ways
    to find out what an input device (keyboard, mouse or joystick) is doing.

pygameのイベントシステムはちょっとトリッキーです。
入力デバイス(キーボード、マウスやジョイスティック)が何をしているか知るには、
2つの異なる方法があります。

.. comment
    The first is by directly checking the state of the device.  You do this by
    calling, say, :func:`pygame.mouse.get_pos()` or :func:`pygame.key.get_pressed()`.
    This will tell you the state of that device *at the moment you call the
    function.*

1つ目の方法は、デバイスの状態を直接確認する方法です。
これは、例えば、:func:`pygame.mouse.get_pos()` や :func:`pygame.key.get_pressed()` を呼び出すことで行います。
これは、 *関数を呼んだ時点* のデバイス状態を教えてくれます。

.. comment
    The second method uses the SDL event queue.  This queue is a list of events --
    events are added to the list as they're detected, and they're deleted from the
    queue as they're read off.

2つ目の方法は、SDLのイベントキューを使う方法です。
このキューはイベントのリストです。
イベントは検知された時にリストに追加され、読み取られるとキューから削除されます。

.. comment
    There are advantages and disadvantages to each system.  State-checking (system
    1) gives you precision -- you know exactly when a given input was made -- if
    ``mouse.get_pressed([0])`` is 1, that means that the left mouse button is
    down *right at this moment*.  The event queue merely reports that the
    mouse was down at some time in the past; if you check the queue fairly often,
    that can be ok, but if you're delayed from checking it by other code, input
    latency can grow.  Another advantage of the state-checking system is that it
    detects "chording" easily; that is, several states at the same time.  If you
    want to know whether the ``t`` and ``f`` keys are down at the same time, just
    check::

それぞれの方式にはメリットとデメリットがあります。状態チェック (方法1) は正確です。
与えられたインプットが作成された時に知ることができます。
もし、 ``mouse.get_pressed([0])`` が 1 ならば、
マウスの左ボタンが今この瞬間に押されていることを意味します。
イベントキューは、過去のどこかでマウスが押されたことを、ただ知らせるだけです。
もし、キューのチェックが頻繁すると、良いのですが、
他のコードによって、キューのチェックが遅れると、入力待ちの時間が長くなります。

状態チェック方式のもう一つの利点は「コード化」を容易に検出できることです。
つまり、複数の状態が同時に検出できます。
例えば、 ``t`` と ``f`` キーが同時に押されたかどうかを知りたければ、次のようにチェックします::

    if key.get_pressed[K_t] and key.get_pressed[K_f]:
        print("Yup!")

.. comment
    In the queue system, however, each keypress arrives in the queue as a
    completely separate event, so you'd need to remember that the ``t`` key was
    down, and hadn't come up yet, while checking for the ``f`` key.  A little more
    complicated.

キュー方式の場合、各キー押下イベントが完全に分けられたイベントとしてキューに到着します。
そのため、 ``t`` キーが押されて、 ``f`` キーがまだ出てきいないことを、
``f`` キーをチェックしながら、覚えておく必要があります。すこし複雑ですね。

.. comment
    The state system has one great weakness, however. It only reports what the
    state of the device is at the moment it's called; if the user hits a mouse
    button then releases it just before a call to ``mouse.get_pressed()``, the
    mouse button will return 0 -- ``get_pressed()`` missed the mouse button press
    completely.  The two events, ``MOUSEBUTTONDOWN`` and ``MOUSEBUTTONUP``, will
    still be sitting in the event queue, however, waiting to be retrieved and
    processed.

しかし、状態チェック方式には、大きな1つの欠点があります。
この方式は、関数が呼ばれた瞬間のデバイスの状態を通知するだけです。
もし、 ``mouse.get_pressed()`` を呼ぶ直前にユーザーがマウスボタンを押して、ボタンを離した場合、
マウスボタンは0を返します。 ``get_pressed()`` は完全にボタン押下を見逃します。
``MOUSEBUTTONDOWN`` と ``MOUSEBUTTONUP`` の2つのイベントは、まだイベントキューには残っているでしょう。
イベントの取得と処理を待っている状態です。

.. comment
    The lesson is: choose the system that meets your requirements.  If you don't
    have much going on in your loop -- say you're just sitting in a ``while True``
    loop, waiting for input, use ``get_pressed()`` or another state function; the
    latency will be lower.  On the other hand, if every keypress is crucial, but
    latency isn't as important -- say your user is typing something in an editbox,
    use the event queue.  Some key presses may be slightly late, but at least you'll
    get them all.

教訓は、「自分の要求を満す方式を選ぶこと」です。
もし、ループ内であまり多くのことが行われていない場合、
例えば、 ``while True`` のループ内で入力を待っているだけの場合は、
``get_pressed()`` や 他のステート関数を使用すると、遅延が小さくなります。
一方、すべてのキー入力が重要だが、遅延はそれほど重要でない場合、
例えば、ユーザーがエディットボックスになにかを入力している場合は、イベントキューを使用します。
キー入力のタイミングが多少遅れるかもしれませんが、少なくともすべてのキー入力を取得することができます。

.. comment
    A note about ``event.poll()`` vs. ``wait()`` -- ``poll()`` may seem better,
    since it doesn't block your program from doing anything while it's waiting for
    input -- ``wait()`` suspends the program until an event is received.
    However, ``poll()`` will consume 100% of available CPU time while it runs,
    and it will fill the event queue with ``NOEVENTS``.  Use ``set_blocked()`` to
    select just those event types you're interested in -- your queue will be much
    more manageable.

``event.poll()`` vs. ``wait()`` についての注意
入力を待っている間、プログラムがブロックされないので、 ``poll()`` の方が良く見えるかもしれません。
``wait()`` はイベントを受けとるまで、プログラムを一時停止します。
しかし、 ``poll()`` は利用できるCPU時間を100%消費してしまいます。
そして、イベントキューを ``NOEVENTS`` でいっぱいにします。
関心のあるイベントタイプのみ選択するために、 ``set_blocked()`` を使いましょう。
キューがより管理しやすくなります。

.. comment
    Another note about the event queue -- even if you don't want to use it, you must
    still clear it periodically because it's still going to be filling up with events
    in the background as the user presses keys and mouses over the window. On Windows,
    if your game goes too long without clearing the queue, the operating system will
    think it has frozen and show a "The application is not responding" message.
    Iterating over ``event.get()`` or simply calling ``event.clear()`` once per frame
    will avoid this.

イベントキューについてのもう1つの注意
イベントキューを使用しない場合でも、ユーザーがキーを押したり、マウスでウィンドウを操作すると、
バックグラウンドでイベントがいっぱいになってしまうので、定期的にクリアする必要があります。
Windowsの場合、キューをクリアせずに、長時間ゲームを続けると、
オペレーティングシステムがフリーズしたと判断し、
「アプリケーションが応答していません」というメッセージがが表示されます。

``event.get()`` を繰り返すか、フレームごとに一度だけ、 ``event.clear()`` を呼び出すことで回避できます。

.. comment
    Colorkey vs. Alpha.
    -------------------

カラーキー vs. アルファ
-----------------------

.. comment
    There's a lot of confusion around these two techniques, and much of it comes
    from the terminology used.

この2つの技術には多くの混乱があり、その多くは用語に起因しています。

.. comment
    'Colorkey blitting' involves telling pygame that all pixels of a certain color
    in a certain image are transparent instead of whatever color they happen to be.
    These transparent pixels are not blitted when the rest of the image is blitted,
    and so don't obscure the background.  This is how we make sprites that aren't
    rectangular in shape.  Simply call :meth:`.Surface.set_colorkey()`, and pass in
    an RGB tuple -- say (0,0,0). This would make every pixel in the source image
    transparent instead of black.

'Colorkey blitting'は pygame にある画像の特定色の全てのピクセルを、
特定色が何色であったとしても透明にするように指示します。
画像の残りの部分が描画された時に、これらの透明なピクセルは描画されないので、
背景が隠れることはありません。
これは、長方形でないスプライトを作る方法です。
単純に、 :meth:`.Surface.set_colorkey()` を呼びだし、引数に RGBのタプルを渡します。
例えば (0,0,0)を渡した場合、元画像の黒色の全ピクセルが透明になります。

.. comment
    'Alpha' is different, and it comes in two flavors. 'Image alpha' applies to the
    whole image, and is probably what you want.  Properly known as 'translucency',
    alpha causes each pixel in the source image to be only *partially* opaque.
    For example, if you set a surface's alpha to 192 and then blitted it onto a
    background, 3/4 of each pixel's color would come from the source image, and 1/4
    from the background.  Alpha is measured from 255 to 0, where 0 is completely
    transparent, and 255 is completely opaque.  Note that colorkey and alpha
    blitting can be combined -- this produces an image that is fully transparent in
    some spots, and semi-transparent in others.

'Alpha' は別物です。2つの意味があります。
'Image alpha'は画像全体に適用されます。おそらくあなたが望むものでしょう。
正しくは「半透明」として知られていますが、
アルファは元画像の各ピクセルを *部分的に* 不透明化させます。
例えば、サーフェスのアルファを192に設定し、それを背景の上に描画するとします。
各ピクセルの色の3/4が元画像から、1/4が背景から来ることになります。
アルファは255から0まであり、0は完全に透明で、255は完全に不透明になります。
カラーキーとアルファを描画時に組み合せて、
一部は完全に透明で、他の部分は半透明の画像を作成することができます。

.. comment
    'Per-pixel alpha' is the other flavor of alpha, and it's more complicated.
    Basically, each pixel in the source image has its own alpha value, from 0 to
    255.  Each pixel, therefore, can have a different opacity when blitted onto a
    background.  This type of alpha can't be mixed with colorkey blitting,
    and it overrides per-image alpha.  Per-pixel alpha is rarely used in
    games, and to use it you have to save your source image in a graphic
    editor with a special *alpha channel*.  It's complicated -- don't use it
    yet.

'Per-pixel alpha'はもう1つの種類のアルファです。これはより複雑です。
基本的に、元画像の各ピクセルは0から255までの独自のアルファ値を持ちます。
したがって、各ピクセルは背景の上に描画されたときに、異なる不透明度を持つことができます。
このタイプのアルファは、カラーキーと混ぜることはできません。
画像ごとのアルファ値よりも優先されます。
ピクセル単位のアルファはゲームではほんとど使われません。
使うためには元画像をグラフィックエディタで *特別なアルファチャンネル* で保存する必要があります。
複雑なので、まだ使わないでください。

.. comment
    Software architecture, design patterns, and games.
    --------------------------------------------------

ソフトウェアアーキテクチャ、デザインパターンとゲーム
----------------------------------------------------

.. comment
    You may reach a point where you're comfortable writing code, you're able to solve
    complex problems without assistance, you understand how to use most of pygame's
    modules, and yet, as you work on larger projects they always seem to get messier
    and harder to maintain as time goes on.  This can manifest in many ways -- for
    example, fixing bugs in one place might always seem to create new bugs elsewhere,
    figuring out *where* code should go might become a challenge, adding new
    things might frequently require you to rewrite many other things, and so on.
    Finally, you decide to cut your losses and start fresh on something new.

コードに書くことに慣れ、複雑な問題でも手助けなしで解決できるようになり、
pygameのほとんどのモジュールの使い方を理解できるようになったのに、
大きなプロジェクトに取り組むと、時間が立つにつれて常に混乱し、維持するのが難しくなることがあります。
これは様々な形で現われます。
例えば、ある場所のバグを修正すると、いつも、別の場所に新しいバグが発生するように見えます。
コードの行き先を決めるのが大変になる。
新しいものを追加すると、他の多くのコードを書き直さなければならないことが頻繁にあります。などです。
最終的に、このままではいけないと思い、新しいことを始めることになります。

.. comment
    This is a common issue and it can be frustrating -- on the one hand, your
    programming skills are improving, and yet you aren't able to finish the games
    you start due to somewhat nebulous organizational problems.

これはよくある問題で、イライラさせられるとおもあります。
プログラミングのスキルは向上しているのに、漠然とした組織的な問題で、ゲームを完成させることができません。

.. comment
    This brings us to the concept of software architecture and design patterns. You
    may be familiar with pygame's "standard" base template (there are many equivalent
    variations of this, so don't stress about the small details too much)::

そこで、ソフトウェアアーキテクチャとデザインパターンという考え方に行き着きます。
pygameの "標準" ベーステンプレート(これと同等のバリエーションは沢山あるので、
細かいことはあまり気にしないでください)はよくご存知でしょう。::

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

.. comment
    It does some initial setup, starts a loop, and then proceeds to repeatedly
    collect input, handle the game's logic, and draw the current frame forever until
    the program ends.  The update, render, wait loop shown here is actually a design
    pattern that serves as the skeleton of most games -- it's prolific because it's
    clean, it's organized, and it works.  (There's also an important but easy-to-miss
    design feature here in the form of a strict division between the game's logic
    and rendering routines.  This decision alone prevents a whole category of potential
    bugs related to objects updating and rendering concurrently, which is nice).

初期設定を行い、ループを開始します。そして、入力を収集し、ゲームのロジックを処理し、現在のフレームを描画します。
これをプログラムが終了するまで繰り返します。
ここで示した、更新、描画、ループの待機は、
実は、ほとんどのゲームの骨組として機能するデザインパターンです。
簡潔で、整理されて、上手く動くからこそ、多くで利用されています。
(また、ゲームロジックとレンダリングルーチンを厳密に分けるという、重要だが見逃しがちな設計上の特徴もあります。
この決定により、オブジェクトの更新とレンダリングの並行実行に起因する
潜在的なバグの可能性を全て防ぐことができます。これは素晴しいことです。)

.. comment
    It turns out that there are many design patterns like this that are used frequently
    in games and in software development at large.  For a great resource on this
    specifically for games, I highly recommend `Game Programming Patterns`_, a short
    free, e-book on the topic.  It covers a bunch of useful patterns and concrete situations
    where you might want to employ them.  It won't instantly make you a better coder,
    but learning some theory about software architecture can go a long way towards
    helping you escape plateaus and tackle larger projects more confidently.

このようなデザインパターンは、ゲームやソフトウェア開発全般で頻繁に使用されることがわかっています。
ゲームに特化した素晴らしいリソースとしては、
'Game Programming Patterns' という短い無料の電子書籍がおすすめです。
この本では、便利なパターンとそれを採用したくなるような具体的なシチュエーションを沢山とりあげています。
この本を読めばすぐに優れたコーダーになるわけではありませんが、
ソフトウェアアーキテクチャに関する理論を学ぶことは、
停滞期を脱し、より大きなプロジェクトに自信を持って取り組む上で大きな助けとなります。

.. comment
    Do things the pythony way.
    --------------------------

pythonのやり方で物事に取り組みましょう
---------------------------------------

.. comment
    A final note (this isn't the least important one; it just comes at the end).
    Pygame is a pretty lightweight wrapper around SDL, which is in turn a pretty
    lightweight wrapper around your native OS graphics calls.  Chances are pretty
    good that if your code is still slow, and you've done the things I've mentioned
    above, then the problem lies in the way you're addressing your data in python.
    Certain idioms are just going to be slow in python no matter what you do.
    Luckily, python is a very clear language -- if a piece of code looks awkward or
    unwieldy, chances are its speed can be improved, too.  Read over `Why Pygame is
    Slow`_ for some deeper insight into why pygame might be considered slower than
    other frameworks/engines, and what that actually means in practice.
    And if you're truly stumped by performance problems, profilers like cProfile_
    (or SnakeViz_, a visualizer for cProfile) can help identify bottlenecks (they'll
    tell you which parts of the code are taking the longest to execute). That said,
    premature optimisation is the root of all evil; if it's already fast enough,
    don't torture the code trying to make it faster.  If it's fast enough, let it
    be :)

最後のノートです。(これは、最も重要なことではなく、ただ最後に出てきただけです。)
pygame は SDLをかなり軽量にしたラッパーです。
SDLはさらに、あなたのネイティブOSのグラフィックス呼び出し用の軽量ラッパーです。
もし、あなたのコードがまだ遅くて、上述したようなことを対処済みなら、
問題はPythonでデータを扱う方法にある可能性はかなり高いです。
ある種のイディオムを使うと、何をやってもPythonでは遅くなります。
幸いなことに、pythonは非常に明快な言語です。
もし、コードの一部が不恰好に見えたり、扱いにくかったりしたら、その速度も改善できる可能性があります。
pygameが他のフレームワークやエンジンよりも遅いと思われる理由と、
それが実際に何を意味するかについての深い洞察は、 `Why Pygame is Slow`_ を読んでください。
また、本当にパフォーマンスの問題で困っているのであれば、
cProfile_ (またはcProfile用のビジュアライザーである SnakeViz_) のようなプロファイラが
ボトルネックの特定に役立ちます。(コードのどの部分の実行に最も長い時間がかかっているかを教えてくれます)。
とはいえ、早まった最適化は諸悪の根源です。すでに十分な速度が出てるのであれば、
より速くしようとコードを苦しめる必要はありません。
十分速いのなら、そのままにしておけばいいのです。:)

.. comment
    There you go. Now you know practically everything I know about using pygame.
    Now, go write that game!

さあ、どうぞ。これで私が知っているpygameの使い方は、実質的にすべてわかったことになります。
さあ、ゲームを書きましょう!!

----
.. comment
    *David Clark is an avid pygame user and the editor of the Pygame Code
    Repository, a showcase for community-submitted python game code.  He is also
    the author of Twitch, an entirely average pygame arcade game.*

*David Clark は熱心なpygameユーザーであり、Pygame Codeの編集者でもあります。コミュニティーが投稿したPythonゲームコードのショーケースである
Pygame Code Repository のエディタです。彼はまた、 Twitch という全く平均的な pygame アーケードゲームの作者でもあります。*

.. comment
    *This guide was substantially updated in 2022.*

*このガイドは2022年に大幅に改訂を行いました。*

.. _Pygame: https://www.pygame.org/
.. _SDL: http://libsdl.org
.. _Python documentation: https://docs.python.org/3/
.. _Game Programming Patterns: https://gameprogrammingpatterns.com/contents.html
.. _Why Pygame is Slow: https://blubberquark.tumblr.com/post/630054903238262784/why-pygame-is-slow
.. _cProfile: https://docs.python.org/3/library/profile.html
.. _SnakeViz: https://jiffyclub.github.io/snakeviz/
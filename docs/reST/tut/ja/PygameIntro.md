# Pygame 入門

## Python Pygame 入門

<div class="rst-class" markdown="1">

docinfo

</div>

Author

:   Pete Shinners

Contact

:   <pete@shinners.org>

この記事は [Python programmers](https://www.python.org/) 向けの [pygame
library](http://www.pygame.org) 入門記事です。 オリジナルバージョンは、
[Py Zine](http://pyzine.com/?p=18) の第１巻3号に掲載されました。
本バージョンは、より良い記事となるように細かい修正を加えています。
Pygame は [SDL](http://www.libsdl.org)
ライブラリとそのヘルパーをラップしたPythonの拡張ライブラリです。

### 歴史

Pygame は
2000年の夏にスタートしました。長年、C言語のプログラマーであった私は、PythonとSDLを同時に発見しました。
当時のPythonはバージョン1.5.2でした。あなたにはすでに馴染みのあるPythonです。
あなたにはSDLの紹介が必要かもしれません。SDLは Simle DirectMedia
Layerの略です。 Sam
Lantingaにより作成されたSDLは、マルチメディアを制御するためのクロスプラットフォームのCライブラリです。
DirectXと比較されます。何百もの商用およびオープンソースのゲームで利用されています。
両方のプロジェクトが、なんて簡潔で直感的なんだと感銘を受けました。
そして、PythonとSDLの融合が興味深い提案であると気づくのに時間はかかりませんでした。

全く同じアイデアで、既に進行中のPySDLという小さなプロジェクトを見つけました。
Mark Bakerにより作成された PySDLはPython拡張として素直なSDL実装でした。
そのインターフェイスは一般的なSWIGラッピングよりは簡潔でしたが、"Cスタイル"のコードを強制されるように感じました。
PySDLの選択肢からなくなり、私を新しいプロジェクトに取り組むように促しました。

私は、Pythonを本当に活用したプロジェクトにしたかった。
私の目標は簡単なことを簡単に、難しいことを直感的に作成できるようにすることでした。
Pygameは2000年10月に開始されました。6ヶ月後バージョン1.0がリリースされました。

### お試し

新しいライブラリを理解するための最良の方法は、まっすぐ例題に飛び込むことです。
pygameの初期の頃、ボールが跳ねるアニメーションを7行で作成しました。
同じものを、よりわかりやすくしたバージョンを見ていきましょう。
これは、簡単なのでわかりやすく、そして完全な内訳です。

<img src="intro_ball.gif" class="inlined-right inlined-right" alt="image" />

``` python
import sys, pygame
pygame.init()

size = width, height = 320, 240
speed = [2, 2]
black = 0, 0, 0

screen = pygame.display.set_mode(size)

ball = pygame.image.load("intro_ball.gif")
ballrect = ball.get_rect()

while True:
    for event in pygame.event.get():
        if event.type == pygame.QUIT: sys.exit()

    ballrect = ballrect.move(speed)
    if ballrect.left < 0 or ballrect.right > width:
        speed[0] = -speed[0]
    if ballrect.top < 0 or ballrect.bottom > height:
        speed[1] = -speed[1]

    screen.fill(black)
    screen.blit(ball, ballrect)
    pygame.display.flip()
```

これはボールが跳ねるアニメーションとしては、限り無くシンプルなものです。
最初のpygameのインポートと初期化は特筆すべきことはありません。
`import pygame` はpygameの利用できる全モジュールをインポートします。
`pygame.init()` の呼び出しは、それらのモジュールを初期化します。

<span class="clr codelineref">line 8</span> で、
`pygame.display.set_mode()`
を呼び出し、グラフィカルなウィンドウを作成します。
PygameとSDLは、グラフィックハードウェアに最適なグラフィックモードをデフォルトで使用することで、簡単に作成します。
モードは上書きすることができ、SDLはハードウェアができないことを補うことができます。
Pygameは画像をサーフェスオブジェクトとして表現します。
`display.set_mod()`
関数は、実際に表示されるグラフィックを表す、新しいサーフェスオブジェクトを作成します。
このサーフェスに描画すると、モニターに表示されます。

<span class="clr codelineref">line 10</span>
で、ボールの画像をロードします。
PygameはSDL_imageライブラリ経由で各種画像フォーマットをサポートします。BMP,
JPG,PNG, TGA, そして GIFを含みます。 `pygame.image.load()`
関数はボールデータを持つサーフェスを返します。
このサーフェスはファイルのカラーキーもしくは透明度の情報を保持します。
ボール画像をロード後は `ballrect` という名の変数に格納します。
Pygameには `Rect <pygame.Rect>`
という名前の便利なユーティリティオブジェクト型があります。これは矩形領域を表します。
あとから出てくる、アニメーション部分のコードで、 *Rect*
オブジェクトができることを見ることになります。

<span class="clr codelineref">line 13</span>
で、このプログラムは初期化され、実行される準備が整います。
無限ループの中で、ユーザインプットをチェックし、ボールを動かし、そして、ボールを描画します。
もし、GUIプログラムに馴染があるなら、イベントやイベントループを扱ったことがあるでしょう。
Pygameにおいても、違いはありません。 *QUIT*
イベントの発生をチェックし、もしあれば、プログラムを終了します。
pygameは全てがきれいにシャットダウンをされることを保証します。

ボールの位置を更新する時がきました。 <span class="clr codelineref">Lines
17</span> で、変数 `ballrect` を現在のスピードで移動させます。 <span
class="clr codelineref">Lines 18 thru 21</span>
で、もしボールがスクリーンの外に移動したなら、進行スピードを逆方向に変更します。
ニュートン物理学とまでいきませんが、必要なのはこれだけです。

<span class="clr codelineref">line 23</span>
で、RBGの黒色で塗り潰してスクリーンを消します。
もし、いままでアニメーションを作成したことがなければ、これは奇妙に思えるかもしれません。
「なぜ全てを消す必要があるの?
なぜ、スクリーン上のボールを、ただ動かさないの?」と尋ねるかもしれません。
それは、コンピュータのアニメーションの仕組みとは少し違います。
アニメーションは、1枚以上の画像を連続して表示することで、人間の目に動いているように錯覚させています。
スクリーンは、ユーザーから見れば、ただの一枚の画像です。
もし、画面からボールを消さなければ、ボールの新しい位置を描き続けることで、ボールの「軌跡」を見ることになります。

<span class="clr codelineref">line 24</span>
で、ボール画像をスクリーンに描画しています。
`Surface.blit() <pygame.Surface.blit>`
メソッドで画像の描画を処理します。 `blit`
はピクセルをある画像から別の画像へコピーすることを意味します。 `blit`
メソッドに、コピー元となる `Surface <pygame.Surface>`
と、コピー元をコピー先に配置するための位置情報を渡します。

最後にするべきは、表示ディスプレイの更新です。
Pygameはディスプレイをダブルバッファで管理します。
描画を完了させた時に、 `pygame.display.flip()` メソッドを呼び出します。
これにより、画面サーフェス上に描画した全てのものが、見えるようになります。
バッファリングにより、完全に描画されたフレームのみが画面に表示されるようになります。
これがないと、ユーザーは作成中の不完全なスクリーンを見ることになります。

これで、pygameのこの短い紹介を終ります。
Pygameには、キーボードやマウス、ジョイスティックのインプットを処理するモジュールもあります。
オーディオのミキシングやストリーミング音楽のデコードも可能です。
*Surface* を使えば、簡単な図形描画や、写真の回転・拡大、 numpy
の配列を使ったリアルタイムの画像処理もできます。 Pygame は PyOpenGL
用のクロスプラットフォームの表示レイヤーとなる機能も持っています。
ほとんどのpygameモジュールはCで書かれており、Python
で書かれているものは、ほとんどありません。

pygameのWebサイトに、すべてのpygame関数の完全なリファレンス文書と、全ユーザー用のチュートリアルがあります。
pygame
のソースには、モンキーパンチやUFOシューティングようにな沢山の例題があります。

### PYTHON と ゲーム

「Pythonはゲーミングに向いているの?」、その答えは、「ゲームによります」です。

Pythonは、実はゲームを動かすのに非常に適しています。
30ミリ秒以下での動作が可能であることに驚かれるでしょう。
それでも、ゲームが複雑化すると、天井に到達する場合もあります。
リアルタイムに動作するゲームの場合、コンピュータをフル活用することになります。

<img src="intro_blade.jpg" class="inlined-right inlined-right" alt="image" />

過去数年にわたり、ゲーム開発の興味深いトレンドがありました。それは、より高レベルの言語への移行です。
通常、ゲームは2つの主要な部分に別れます。ゲームエンジンとゲームロジックです。
ゲームエンジンは可能な限り高速である必要があります。ゲームロジックは、エンジンを実際に動かすものです。
ゲームエンジンがアセンブリで書かれ、一部はCで書かれたのは、大昔の話ではありません。
現在は、Cがゲームエンジンに使用され、ゲーム自体は高レベルのスクリプト言語で書かれます。
Quake3 や Unreal
などのゲームでは、これらのスクリプトがポータブルなバイトコードとして実行れます。

2001年の初頭に、開発社の Rebel Act Studios が 自社のゲーム Severance:
Blade of Darkness を完成させました。
自社向けのカスタム3Dエンジンを使い、ゲームの残りの部分はPythonで書かれています。
このゲームは、第三者視点の血みどろアクションの戦闘ものです。
中世の戦士を操作し、ダンジョンや城を探検しながら、複雑なコンビネーションで攻撃し首を切ります。
このゲーム用のサードパーティアドオンをダウンロードできます。
これらのアドオンは、Pythonのソースファイル以外の何物でもありません。

より最近では、Freedom Force や Humungousの Backyard Sports
シリーズのような様々なゲームでPythonは利用されています。

<img src="intro_freedom.jpg" class="inlined-right inlined-right" alt="image" />

Pygame と SDL は 優れた Cで作成された2Dゲームエンジンとして機能します。
ゲームの実行時間の大部分は、グラフィックを処理するSDL内部で費されます。
SDLはグラフィックのハードウェアアクセレーションを利用できます。
これを有効にすると、1秒間に40フレーム程度で動作していたゲームが、
1秒間に200フレーム以上で動作することになります。
Pythonゲームが1秒間に200フレームで動作するとわかれば、
Pythonとゲームが一緒に動作できると実感します

PythonとSDLの両方がマルチプラットフォームで動作することは印象的です。
例えば、2001年5月、私自身の完全なpygameプロジェクトをリリースしました。
それは、アーケードスタイルのアクションゲームである SolarWolf です。
1年たって、私が驚いたことは、バグフィックスや更新のためのパッチが必要ないということです。
このゲームは完全にWindows上で開発しましたが、 Linux や Mac OSX や
多くのUnixで、何の追加作業もなく動作しています。

まだ、非常に明らかな限界はあります。
ハードウェアアクセレーショングラフィックの最適な管理方法が、
必ずしも、ソフトウェアレンダリングの最速の結果を得るとは限りません。
ハードウェアのサポートは全プラットフォームで利用できるわけではありません。
ゲームをより複雑にすれば、多くの場合、どちらかにコミットする必要があります。
SDLは、他の設計上の制限があります。
それは、フルスクリーンのスクロールするグラフィックが、
ゲームをプレイできない速度にまで低下させるというものです。
SDLは全種類のゲームに向いているわけではないけれど、
Lokiのような会社がSDLを使って、さまざまな種類の商用品質のタイトルを提供していることを覚えておいてください。

Pygameはゲームを書くことについてはローレベルです。
あなたはすぐに、一般的な関数を自分のゲーム環境用にラップする必要があることに気が付くでしょう。
この場合に素晴らしいところは、あなたの邪魔をするものが Pygame
にはないことです。 あなたのプログラムはすべてをコントロールできます。

その副作用として、より高度なフレームワークを構築するために、多くのコードを取り入れる必要があることがわります。
あなたは、自分のしていることを、より深く理解する必要があります。

### 最後に

ゲームの開発は、大変やりがいがのあるものです。
書いたコードで、見たり、対話できるのは、とてもエキサイティングです。
Pygameは現在、だいたい30件の他プロジェクトが利用しています。
そのうちのいくつかは、今すぐ遊べるようになっています。
pygameのWebサイトを訪ずれて、他のユーザーがPythonで実現していることを見て驚くかもしれません。

私が注目しているのは、ゲーム開発をするために、初めてPythonに触れる人の多さです。
ゲームが新しいプログラマにとって魅力的なのはわかりますが、
ゲームを作るには言語をしっかり理解する必要があるので、難しいかもしれません。
このような人達をサポートするために、多くの例題や
pygameのコンセプトが初めての人のためのチュートリアルを書きました。

結局のところ、私からのアドバイスは「シンプルであること」です。これは、いくら強調してもしきれません。
もし、最初のゲームの開発を計画しているなら、学ぶべきことが沢山あります。
シンプルなゲームでさえ、デザインに挑戦できるでしょうし、複雑なゲームが必ずしも楽しいゲームとは限りません。
Pythonを理解すれば、1、2週間でpygameを使って簡単なゲームを作成できます。
そこから、完全に体裁を整えたゲームにするために磨きをかけるには、驚くほどの時間が必要です。

#### Pygame モジュールの概要

|                                |                                               |
|--------------------------------|-----------------------------------------------|
| `cdrom <pygame.cdrom>`         | playback                                      |
| `cursors <pygame.cursors>`     | load cursor images, includes standard cursors |
| `display <pygame.display>`     | control the display window or screen          |
| `draw <pygame.draw>`           | draw simple shapes onto a Surface             |
| `event <pygame.event>`         | manage events and the event queue             |
| `font <pygame.font>`           | create and render TrueType fonts              |
| `image <pygame.image>`         | save and load images                          |
| `joystick <pygame.joystick>`   | manage joystick devices                       |
| `key <pygame.key>`             | manage the keyboard                           |
| `mouse <pygame.mouse>`         | manage the mouse                              |
| `sndarray <pygame.sndarray>`   | manipulate sounds with numpy                  |
| `surfarray <pygame.surfarray>` | manipulate images with numpy                  |
| `time <pygame.time>`           | control timing                                |
| `transform <pygame.transform>` | scale, rotate, and flip images                |

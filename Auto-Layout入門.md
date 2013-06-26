このwikiは、こちらのイベント [WWDCに行ってきたけど内容については一切話せません @ mixi](http://atnd.org/event/mixiwwdc2013) で発表した内容をまとめたものとなります。

内容については、予告なく修正、変更する場合があります。ご了承ください。


### AutoLayoutとは

iOS/OSXのアプリケーションでUIパーツを配置するときにその位置やサイズを指定する方法です。2012年に登場した比較的新しいトピックで、iOS6やOS X 10.6 以降で利用することができます。(iOS5.xでは実行時エラーが発生します)

親ビューや兄弟のビューに対して、どのようにレイアウトをするかを制約で記述します。その制約に沿って親ビューや兄弟ビューが変化した時にリサイズが適用されパーツが再配置されます。

パーツのリサイズに関してはAuto Resizing(spring and struts)がありますが、こちらより記述力が高いのでviewの項目をxibやstoryboardに寄せることができます。

### 制約の種類

設定することのできる制約には様々な種類がありますが、Xcodeから設定することのできる制約には以下のようなものがあります。

##### Pin
親ビューの上や左から何ポイント離すか、あるいはviewの幅や高さを指定します。兄弟のビューに対して、どれくらいの幅を持たせるかなども設定することができます。
設定できる項目としては以下のようなものがあります。

| constraint | 説明 |
| ---------- | ----- | 
| Width | view の幅 |
| Height | view の高さ |
| Horizontal Spacing | 兄弟のビューに対して水平方向にどれくらい間隔をあけるか |
| Vertical Spacing | 兄弟のビューに対して垂直方向にどれくらい間隔をあけるか |
| Leading Space to SuperView | 親ビューに対して左側※にどれくらい間隔をあけるか | 
| Trailing Space to SuperView | 親ビューに対して右側※にどれくらい間隔をあけるか | 
| Top Space to SuperView | 親ビューに対して上側にどれくらい間隔をあけるか | 
| Bottom Space to SuperView | 親ビューに対して下側にどれくらい間隔をあけるか | 
| Width Equally | 兄弟ビューと幅を同じに揃えます |
| Height Equally | 兄弟ビューと高さを同じに揃えます |

※　正しくは、アプリケーションの言語設定によって異なります。日本語や英語のように左から右へ書いていく言語では、Leading Spaceは左側、Trailing Spaceは右側の間隔となりますが、イスラム語のように右から左へ書き進める言語では左右が反転し、Leading Spaceが右側、Trailing Spaceは左側となります。


##### Align
隣り合うビューとviewの端を揃えることができます。Interface Builder で設定しているときのようにviewを揃えて配置することができます。
設定項目には以下のようなものがあります。

| constraint | 説明 |
| ---------- | ----- | 
| Left Edges | 左端揃え |
| Right Edges | 右端揃え |
| Top Edges | 上揃え |
| Bottom Edges | 下揃え |
| Horizontal Centers | 水平方向に並べ、縦方向の中心を揃える |
| Vertical Centers | 垂直方向に並べ、横方向の中心を揃える |
| Baselines | Labelやボタンなどのテキストの下を揃える |
| Horizontal Center in Container | コンテナ(親ビュー)の中で縦方向の中心で揃える |
| Vertical Center in Container | コンテナ(親ビュー)の中で横方向の中心で揃える |

### 制約のサンプル

実際に制約を追加する例を考えてみましょう。

![制約のサンプル](https://raw.github.com/mixi-inc/iOSTraining/master/Doc/Images/Studying-Auto-Layout/constraint-sample.png)

この図はあるViewの上に3つのUILabelを設置したサンプルです。
左側にあるUILabelには二つの制約をつけています

- Top Space To Super View (=20) 親ビューから高さ20の位置に上端を持ってくる
- Top Space To Super View (=20) 親ビューの左端から幅20の位置にこのviewの左端を持ってくる

また、右側にあるUILabel-2にも二つの制約をつけています

- Horizontal Space (=20) もう片方のUILabelの右端とこのLabelの左端の間に20ピクセルのスペースを入れる
- Bottom Alignment       もう片方のUILabelの下端とこのLabelの下端を揃えます

下にあるUILabel-3は親ビューの終端位置(右端)から50ピクセルの幅をもつ制約を付け加えています。(実際には制約が破綻するので、下からの位置の制約もあります。)

これを実行すると次のようになります。

![DEMO](https://raw.github.com/mixi-inc/iOSTraining/master/Doc/Images/Studying-Auto-Layout/demo1.png)


画面を横に向けて、親ビューをリサイズしたときにUILabelとUILabel-2はともに左上に配置され、UILabel-3は右下に配置されています。
これは右と下からの位置で制約があるためです。

また、この制約の中でUILabelに文字を追加します。

![DEMO](https://raw.github.com/mixi-inc/iOSTraining/master/Doc/Images/Studying-Auto-Layout/demo2.png)

UILabelの文字が増えて幅が広がります。それにあわせてUILabel-2も右にずれていきます。これは、UILabel-2の左端とUILabelの右端の間に常に20ピクセルの幅を持たせる制約があるためです。
また、Auto LayoutではUILabelのようなサイズを可変で変えれる物は、コンテンツの内容(この場合だとlabel.text)に変化があったときに自動的にリサイズしてくれる設定があります。

### Xcode上での設定

Auto Layoutの制約をXcode上から設定する方法について紹介します。Xcode上からは二カ所で設定することができます。
一つはInterface Builder上で、もう一つはメニューバーからです。

![DEMO](https://raw.github.com/mixi-inc/iOSTraining/master/Doc/Images/Studying-Auto-Layout/set-constraints1.png)
![DEMO](https://raw.github.com/mixi-inc/iOSTraining/master/Doc/Images/Studying-Auto-Layout/set-constraints2.png)

設定した制約はInterface BuilderのDocument Outlineから確認することができます。


![DEMO](https://raw.github.com/mixi-inc/iOSTraining/master/Doc/Images/Studying-Auto-Layout/set-constraints3.png)

widthやheightのようにあるview単体にかかってくる制約については、そのview以下に制約が追加されます。trailing spaceのようにview全体にかかってくる制約については、そのviewのConstraints以下にあります。

viewを配置したり、制約を追加するとここにその制約が表示されます。このとき青と紫のアイコンがあると思いますが、青はユーザーが設定した制約、紫はInterface Builderが自動的に補完した制約となります。
これは、制約をいくつか追加してもviewが一意に決められないといった場合に挿入されます。

### どのように制約が適用されるか 2

もう少し、制約が適用される例を紹介します。図のようにUIButtonを二つ並べて配置します。この時に以下のように制約を追加します。

- Button Aと親ビューの左端
- Button Bと親ビューの右端
- Button A と Button B との間

これだけの場合、横方向について、ボタンAとボタンBの幅が不定になります。そのためInterface Builderが

- Button Aの幅

という制約を追加します。

これを実行すると、Portrait, Landscape の画面は次のようになります。

![DEMO](https://raw.github.com/mixi-inc/iOSTraining/master/Doc/Images/Studying-Auto-Layout/demo4.png)

Landscapeにしたとき、画面全体の横幅が伸びます。しかし、マージンとボタンAの幅には制約があるため、制約のないボタンBの幅が拡大されます。

では、ボタンBの幅をできるだけ伸ばすが最大でも200に設定したいときにどのような制約を追加すればよいでしょうか。
Auto Layoutで加えることのできる制約には不等号も用いることができます。 `width ≦ 200`のような制約です。
この制約で最大の幅を設定できますがこの場合、IBで設定した幅になります(Portrait時の幅)。そこでできるだけ伸ばすと言う制約を追加します。そのためには、固定値で幅を設定します(`width = 200`)。
このときに 不等号の制約を等号の制約より強い優先度にします。こうすることで、幅を200以下に必ず抑えるがでその範囲内で幅を200に近づけるという制約を作ることが出来ます。
ボタンBと親ビューの右端を20以上にするという制約を追加することで所望の動作を実現することができます。

![DEMO](https://raw.github.com/mixi-inc/iOSTraining/master/Doc/Images/Studying-Auto-Layout/demo5.png)

**制約(優先度の強い順)**
1. ボタンの最大幅を設定 ( ≦ 200 )
2. ボタンと親ビューのtrailing spaceを設定 ( ≧ 20 )
3. ボタンの幅を設定 ( = 200 )

![DEMO](https://raw.github.com/mixi-inc/iOSTraining/master/Doc/Images/Studying-Auto-Layout/demo6.png)


### Auto Layoutを使う時の注意点
Auto Layoutは表現力があり強力ですが、いくつか利用する上で注意しないとならない点があります。
たとえば、一度配置した後にレイアウトを変更したときにその変更が反映されないということです。具体的には、パーツを配置した後にview.frameを変更する場合にそのレイアウト変更に対して制約は維持されません。bottom edges で整列させたいくつかのボタンのうち、一つをアニメーションさせたときに他のボタンはアニメーションせずにその場にとどまったままです。





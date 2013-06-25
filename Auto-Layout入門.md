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










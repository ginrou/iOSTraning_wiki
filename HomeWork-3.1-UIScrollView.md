ここでは、iOSにおけるviewの中でもよく使われるUIScrollViewの紹介と、UIScriollViewを用いた課題です

# UIScrollView紹介
## UIScrollViewとは
iOSのViewに入りきらないViewを表示するためにviewの一部を切り出してくれるviewです。

**もう少し詳しく**
- WebViewやmixiのアプリだとフィードを表示してる画面のように縦とか横にスクロールする画面
- 写真アプリなどで画像を拡大縮小するとき
- スワイプして次のページにというページング

などのシーンで使われます。画面内をスクロールするなど、とても使用頻度の高いview componentです

公式ドキュメントはこちら
[UIScrollView Class Reference](http://developer.apple.com/library/ios/#documentation/uikit/reference/UIScrollView_Class/Reference/UIScrollView.html)

## UIScrollViewの仕組み
UIScrollViewは、自分のサイズより大きなsubviewの一部を切り出して表示する役割を持っています。どの位置(厳密にはどのframe)を表示するかを指定することもできます。

そこでスクロールして画面をはみ出るコンテンツを表示したいときは、 画面のview → scroll view → コンテンツのview という階層構造でviewを構築することで実現できます。viewと同じサイズのscroll view を貼付け、scrollviewの中をコンテンツのviewが動き回ると言うイメージです。

例として下の画像のview階層を見てみましょう。

![scroll view の階層](https://raw.github.com/mixi-inc/iOSTraining/HEAD/Doc/Images/HomeWork/how_to_use_scrollview.png)

アプリの画面(view)に、そのサイズより大きい画像(imageView)を貼付けるとします。
この場合、アプリの画面(view)の下にscrollViewを追加し、scrollViewの下にimageViewを追加しています。コードで書くと、
```
[view addSubview:scrollView];
[scrollView addSubview:imageView];
```
となります。



# 実際に動かしてみる
上の例を実装することで、scrollViewの動作を確認してみましょう。
リポジトリのHomewor/3.1k以下にある scrollViewSample を開くか、Xcodeから新しいプロジェクトをテンプレートをSingle View Applicationで開き、こちらの画像をプロジェクトに追加してください。

画像のURL → あとで貼る

1. scroll view を貼る
  ``` 
    UIScrollView *scrollView = [[UIScrollView alloc] initWithFrame:self.view.frame];
    [self.view addSubview:scrollView];
  ```
  - scrollview の インスタンスを生成して、self.viewに追加します。
  - この時、scrollviewのframe(原点とサイズ)はself.viewと同じにします。そうすることで、画面全体にscrollviewを表示できます。
2. imageViewの準備
  - 画像を扱うimageviewについては次回以降で触れるので、今回は以下のコードを使ってください。
```
    UIImage *image = [UIImage imageNamed:@"big_image.jpg"];
    UIImageView *imageView = [[UIImageView alloc] initWithFrame:CGRectMake(0, 0, image.size.width, image.size.height)];
    imageView.image = image;
```

### Tips : あれ？うまく動かないというときは
- 画像が正しく表示されているか確認しましょう。意外とtypoしてたりします。
  - UIImage *image が nil でないことを確認する。画像ファイル名が間違っている時はnilになります。
  - `[self.view addSubview:imageView];` とすることでscrollviewに原因があるかを特定できます。画像が表示されたらscrollviewに原因があります。


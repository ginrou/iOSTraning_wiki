4.3までで、最低限のUITableViewの使い方は紹介しました。
この章では、4.3までで説明できなかったけど、よく用いられるtableviewの機能を紹介します。

**目次**

1. Section
2. Header, Footer
3. RefreshControll


# 1. Section

4.1で紹介したように、UITableViewは行ごと(cell)だけでなく、Sectionによって区切ることができます。
セクションで区切ることで、表示するデータをグルーピングして表示することができます。

// セクションの画像

セクションを追加する時に必要なメソッドは
`- (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView`
のみで、TableViewに表示するセクションの数を返してやります。
行数は各セクションごとに区切られ、tableview全体で通しの番号でないので注意してください


### セクションを実際に使ってみる
4.1の終了時のものまで一度戻してみてください(面倒な場合は、githubのソースコードからプロジェクトファイルを開いてください)

新しく作り直す時、必要な処理は

1. サンプルプロジェクトを作る
2. xibでviewControllerにtableviewを貼付け、ソースコードと紐づける
3. ヘッダファイルで UITableViewDataSourceとUITableViewDelegateの委譲を宣言し、実装する。必要なメソッドは以下の二つです
  - tableView:numberOfRowsInSection:
  - tableView:cellForRowAtIndexPath:

以上です。

では実際にセクションを追加します。
```
- (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView
{
    return 2;
}
```

この状態で実行すると、次のようになると思います。
表示するテキストは `[NSString stringWithFormat:@"(%d, %d)", indexPath.section, indexPath.row]`としました。

**// 画像 **

セクションの区切りが出来ているのが分かるかと思います。
tableviewのスタイルをgroupedにすると、より分かれて表示できます。

セクションにはタイトルを付けることもできます。delegateメソッドの一つである、tableView:titleForHeaderInSection:でタイトルを返すことができます。
例えば、以下のように実装すると
```
- (NSString *)tableView:(UITableView *)tableView titleForHeaderInSection:(NSInteger)section
{
    return [NSString stringWithFormat:@"%d 番目のセクション", section];
}
```

実行結果は次のようになります

**// 画像 **




# 2. Header, Footer
タイトルだけでなく、各セクションごとにヘッダとフッタを作ることで、よりリッチな表現をすることができます。
ヘッダをカスタマイズする場合は、次のメソッドを実装します。

```
- (CGFloat)tableView:(UITableView *)tableView heightForHeaderInSection:(NSInteger)section
```
このメソッドでは、headerの高さを返します。

```
- (UIView *)tableView:(UITableView *)tableView viewForHeaderInSection:(NSInteger)section
```
このメソッドでは、実際にheaderとなるviewを作って返します。

この二つを実装することでヘッダを表示することが出来ます。

### 実際にヘッダを作ってみる。
上述の通り、二つのメソッドを追加することでヘッダを追加することができます。

```
- (CGFloat)tableView:(UITableView *)tableView heightForHeaderInSection:(NSInteger)section
{
    return 120.0;
}

- (UIView *)tableView:(UITableView *)tableView viewForHeaderInSection:(NSInteger)section
{
    UIView *view = [[UIView alloc] initWithFrame:CGRectMake(0, 0, 320, 120)];
    view.backgroundColor = [UIColor redColor];
    return view;
}
```
今回は高さ120pxで、背景色が赤のviewを貼付けました。
以下のようになれば正解です！




### フッタについて
フッタもヘッダと同様に高さを返すメソッドと、viewを作るメソッドを実装すれば実現することが出来ます。
```
- (CGFloat)tableView:(UITableView *)tableView heightForFooterInSection:(NSInteger)section
```
と
```
- (UIView *)tableView:(UITableView *)tableView viewForFooterInSection:(NSInteger)section
```

の二つです。headerと同じ処理になるので、詳解は割愛します。


** // ふったとへっだを実装した図 **


# 3. RefreshControll

RefreshControllとは、引っぱり更新やPullToRefreshと呼ばれるアクションで、tableviewを一番上までスクロールしてさらに引っ張ることでデータを更新するUIです。

iOS6からこの機能がOSに実装されて、もはやスタンダードとなっているこのUIコンポーネントを紹介します。

### 仕組み







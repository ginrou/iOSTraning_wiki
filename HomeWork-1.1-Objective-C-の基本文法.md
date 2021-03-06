制御構文
- 基本的にはC言語と同じです
- if, else, while, for, switch-case などは同じように使えます
- 高速列挙に for-in 文があります
- Perlのように後置ifやmap, grepなどはありません

# 簡単なsandboxとコンソールへの出力
### sandbox プロジェクトの作成
簡単なsandboxとして適当なプロジェクトを作ってください。
- Xcodeを起動
- 左上File → New → Project
- SingleViewApplication → Product Name などは適当に → 保存するディレクトリも適当で構いません
- 新しいプロジェクトが出来ます。
- ViewControllerのメソッド viewDidLoad に色々書き込んで行けば実行されます。

### NSLogによるコンソールへの出力
- コンソールへの出力は昔ながらのprintfも使えますが、オブジェクトを出力するNSLogがよく使われます。
- ``NSLog(@"hello world");`` をviewDidLoadに書き込んで左上のRunを押すと実行されます。
- Xcode下部コンソールに"hello world"と表示されれば成功です。
- `NSLog(@"%@", obj);` とすると結構なんでも表示してくれるので使いましょう。

# Objective Cの基本的なデータ型

### NSArray
  - いわゆる配列型
  - オブジェクトは何でも代入できる。プリミティブなint型などはできない
  - インスタンス化 `` @[hoge, fuga]; ``
  - インスタンス化後の改変は不可
  - 事後改変可能な配列はNSMutableArray型
```
NSArray *array = @[obj1, obj2]; // インスタンス化
id obj = array[0]; // 0番目のオブジェクトを取り出す( obj = obj1 )
array[0] = hogehoge; // 代入は無理

NSMutableArray *mutableArray = [NSMutableArray array]; // mutable
[mutableArray addObject:hoge]; //mutableArrayの末尾にhogeを追加 ( mutableArray = @[hoge] )
[mutableArray addObject:fuga]; //                   fugaを追加 ( mutableArray = @[hoge, fuga] )
[mutableArray removeObjectAtIndex:0)]; // 先頭のオブジェクトを削除 ( mutableArray = @[fuga] )
```

###  NSDictionary
  - 辞書型
  - NSArrayと同様にオブジェクトは何でも代入できる。プリミティブなintなどは代入できない
  - キー名はNSStringで指定
  - インスタンス化 `` @{key : value} ``
  - インスタンス化後の改変は不可
  - 事後改変可能な辞書はNSMutableDictionary型
```
NSDictionary *dict = @{ @"key" : value}; // インスタンス化. valueは適当なオブジェクト
id obj = dict[@"key"]; // 0番目のオブジェクトを取り出す( obj = value )
dict[@"key2"] = fuga; // 代入は無理

NSMutableDictionary *mutableDict = [NSMutableDictionary dictionary]; // mutable

mutableDict[@"key"] = @"value"; // keyをキーとしてvalueという文字列を追加
[mutableDict removeObjectForKey:@"key"]; // キー名 @"key" のオブジェクトを削除
mutableDict[@"key"] = nil; // nilを代入するとクラッシュします。

```

###  NSString (文字列)
- 文字列型。よく使う
- 様々なインスタンス方法があるが、 ``@"hogefuga"`` @＋ダブルクオーテーションで括る形が一般的
- 後から改変する場合は NSMutableStringを使う
- 正規表現はNSRegularExpressionを使います。
```
NSString *str = @"hoge fuga";
NSMutableString *mutable = [NSMutableString string];
[mutable appendString:@"hogehoge"]; // 文字列をappend

NSString *string = [NSString stringWithFormat:@"%d + %d = %d",1 ,2, 3]; // フォーマット指定子も利用可能
NSLog(@"%@", string); // "1 + 2 = 3"

```

###  NSNumber (数値型)
- 数値をラップしたデータ型です
- NSArrayやDictionaryにint型などを持たせたい時などに使います
- @1, @2, などでインスタンス化できます
- int型、double型に変換したい時は`[number intValue], [number doubleValue]`のように使います
```
NSNumber *number = @1;
NSArray *array = @[number, @2]; //直接intなどを代入できないが、NSNumberでラップしたら使える
NSNumber *num = @YES; // YES, NO などもキャスト可能

int a = [number intValue]; // int型へ変換

```

###  NSData, NSURL, NSError, NSSet...
その他のデータ型はいろいろありますが、説明しきれないので参考図書なりググるなりお願いします。


# NSObject, nil, id型
特殊なオブジェクト型など

### NSObject
単一継承のみのObjective Cにおけるルートのオブジェクト。全てのオブジェクトはNSObjectを継承している。
簡単なモデルとかを作る時の親クラスに使うことなどが多いです。

時々使うメソッド
- `performSelector:withObject:afterDelay:` : delayを指定して遅延実行する

### nil
- 未初期化のオブジェクトでnullのクラスオブジェクト。何もないことを表す。NULLと同じようなものです
- 条件判断ではNOを返す
- nilオブジェクトのメソッドを呼び出しても握りつぶされます。(クラッシュなどはしません)
```
id obj = nil;
if(obj) { // always fales
 // do not come here
} else {
  // come here
}

[obj method]; // クラッシュはしませんが、何も起きません
```

### id型
- 全てのクラスを表すことのできる、汎用的な型。
- Cなどのvoid型に通じる物があると思います。



# 課題
## 課題1 基本的なデータ構造
以下のデータ構造を持つオブジェクトを上記オブジェクトなどを使って再現してください。(クラス化などはしなくても結構です)
```
(
  {
     domain => "mixi.jp"
     entry  => ("list_voice.pl", "list_diary.pl", "list_mymall_item.pl" )
  },
  {
    domain => "mmall.jp"
    entry => (
      {
        path => "add_diary.pl"
        query => (
          { "tag_id" => 7 }
        )
      }
    )
  },
  {
    domain => "itunes.apple.com"
  }
)
```
目的:NSDictionary, NSArrayの使い方に慣れる.

時間があれば:Mutableなクラスを使って、適宜addObjectやremoveObjectなどを行ってみてください

## 課題２ クラスの作成
NSMutableArrayを用いて、キューを実現するクラス TestQueue と スタックを実現する TestStackを作ってください。
それぞれ、以下のメソッドを追加してください
- `- (void)push:(id)object` オブジェクトを追加する。(TestQueueの場合は末尾に、TestStackの場合は先頭に追加する)
- `- (id)pop` 先頭のオブジェクトを返す
- `- (NSInteger)size` Queue, Stack の長さを返す

目的：クラスの作り方について学ぶ

時間があれば:優先度付きキューを作ってみてください
[参考プロジェクト](https://github.com/jessedc/JCPriorityQueue/tree/experimental/heap-queue)
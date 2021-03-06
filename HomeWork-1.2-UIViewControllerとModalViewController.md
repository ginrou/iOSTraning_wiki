UIViewControllerとUIModalViewControllerを使った課題です。
途中までは講義中のものと同じです

# 課題
### 概要
- UIViewControllerのView上にボタンを設置し、そのボタンを押すとモーダルが立ち上がる
  - 立ち上げるモーダルは新しいViewControllerクラスを作ってください
- 立ち上がるモーダルにはボタンが一つついており、そのボタンをタップするとモーダルが閉じる
- モーダルを殺す処理はモーダル自身がするのではなく、delegateを用いてモーダルを表示させた親が殺すようにする
- ---------ここまでは講義中のものと同じ------------
- modalが閉じた瞬間に新しいmodalを表示するようにしてください


### イメージ
![遷移イメージ](https://raw.github.com/mixi-inc/iOSTraining/master/Doc/Images/HomeWork/1-2-1.png)

見づらい場合はこちらを→[https://github.com/mixi-inc/iOSTraining/blob/master/Doc/Images/HomeWork/1-2-1.png](https://github.com/mixi-inc/iOSTraining/blob/master/Doc/Images/HomeWork/1-2-1.png)

### 少しだけ解説
dismissViewControllerにはcompletitionBlockという引数があります。
この引数には、モーダルが閉じきった時に実行するクロージャ(Blocks)を渡します。Blocksについては、また後日解説がありますが、
「完了時に実行したい処理」を書けば問題ありません。

### 目的
- UIViewControllerを作れるようになる
- ModalViewを表示させることができるようになる
- delegateパターンを実装できるようになる
- completitionBlockが使えるようになる
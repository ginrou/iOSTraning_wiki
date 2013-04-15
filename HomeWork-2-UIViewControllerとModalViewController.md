UIViewControllerとUIModalViewControllerを使った課題です。

# 課題
### 概要
- UIViewControllerのView上にボタンを設置し、そのボタンを押すとモーダルが立ち上がる
  - 立ち上げるモーダルは新しいViewControllerクラスを作ってください
- 立ち上がるモーダルにはボタンが一つついており、そのボタンをタップするとモーダルが閉じる
- モーダルを殺す処理はモーダル自身がするのではなく、delegateを用いてモーダルを表示させた親が殺すようにする


### イメージ
![遷移イメージ](https://raw.github.com/mixi-inc/iOSTraining/master/Doc/Images/HomeWork/1-2-1.jpg)

### 目的
- UIViewControllerを作れるようになる
- ModalViewを表示させることができるようになる
- delegateパターンを実装できるようになる　
UINavigationControllerとボタンのカスタマイズと、popToRootViewControllerについて

## 概要
- UINavigationControllerを無限にpushできるようにする(講義中と同じ)
- navigationbarのボタンについては
  - 右上はpushというタイトルのボタンで、タップすると同じview controllerがpushされる
  - 左上には、第一階層の時はpopボタンを、第二階層以降では戻るとpopボタンを配置する
    - 戻るボタンをタップすると、一つ前の階層に戻り
    - popボタンをタップすると、第一階層に戻る


## イメージ
あとではる


## ヒント、注意点など
- 右上のボタンは`self.navigationItem setRightBarButtonItem:`でセットできます。渡す引数はUIBarButtonItem型です
- 左上のボタンをセットすると戻るボタンが消えてしまいます。その時は`self.navigationItem.leftItemsSupplementBackButton = YES`としてください。
- 第一階層に戻るにはUINavigationControllerの`popToRootViewControllerAnimated:`を呼べば戻れます

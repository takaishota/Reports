iOS 9 週連続 Bootcamp！8週目 @dots
---
http://dev.classmethod.jp/news/ios9-bootcamp-8th/

## 考慮点

* NSNotification
  * 逃げの設計
  * オブジェクト思考を壊す

* 値わたしと参照わたし
  * できるだけ値わたしを使いたい
* モデル/ビューの完全な分離

  * メインループを意識する
  * ビューとモデルの不整合をなくす
    * 状態の把握

* 描画関連デリゲート順
  * 前提
    * storyboardで骨組みを作る
    * 細かいところのレイアウトはxibを使う

  * ビューの操作
    * updateViewConntraints
    * layoutSubViews
    とかでのみビューを触る

  * storyboard、Xibに定義していればコードをほとんど記述しなくて良い
  * 記述する場面（レアケース）
    * デバイダー動かしたり、回転したりとか状態が変わってします場合のみ

  * 回転
    * iOS7
      回転のデリゲートメソッド
    * iOS8〜
      trailCollection〜のデリゲートメソッド

* TopViewController一強時代
* デリゲート経由での通知を行う
* Notificationやシングルトンをやめる
* Extension

## swift使った書簡

* enum無双
* extension無双
* ジェネクリス
  * 共通処理をまとめられる
  * APIアクセスのコードで使っている

## まとめ

* Deployment Targetは8以上がオススメ
* とにかく状態が多いのでQAしやすいように状態を整理するのがオススメ
* Swiftだとenum、extensionが便利です

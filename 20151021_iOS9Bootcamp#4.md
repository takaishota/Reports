iOS 9 週連続 Bootcamp！4週目 @dots
---
http://dev.classmethod.jp/news/ios9-bootcamp-4th/

## tvOS をさわってみよう
### Apple TVとは
* Appleが開発/販売するセットトップボックス
* 放送信号を受信して表示する端末

#### Apple TVでできること
* 番組や映画を購入して
* Air PlayでMacやiPhoneの画面をテレビで写す

#### Top Shelf
* 画面上部のコンテンツが表示されている領域部分

#### 旧OSとの違い
* リモコン
  * Touch サーフェス上で操作
    * タップ
    * スワイプ
  * Siriで検索も可能
* アプリがストアからダウンロードできる

### tvosについて
* iOS9がベース
* TVML
  * アップr独自のマークアップ言語
* JavaScript

#### Frameworks
* TVMLJS
  * JSのコンポーネエント
* TVMLKit
* TVSearvices
  * topshelfExtensionの提供
* 利用可能iOS Frameworks
  * UIKitは使える
  * UIWebViewやWebkitは使えない
    -> 統一されたUIで使用できる
* Apple Tvに永続的なローカルストレーシはない
  -> データの保存にはiCloudを使う

### Sample Code for Apple
#### UIKit Catalog
* Focus
  * UIFocusGuide クラスがある
#### TVMLCatalog
* TVMLのコンテンツを表示する
* ターミナルでclientディレクトリに移動してWebサーバーを立ち上げるコマンドを実行する  
  python -m simpleHTTP server ポート
* Appdelegateしかない
  -> サーバの指定と最初に起動するJSファイルを指定
  -> あとはJSで処理するようになっている
* TVMLの表示、ユーザインタラクションはjsで実行される

### Forcus
  * リモコンや外部入力装置からの
  * 一つのviewにしか

### Forcus Engine
* フォーカスとフォーカス移動を制御するシステム

### UIFocusEnvironment
* preferredFocusedView
  * デフォルトのフォーカスビューを提供する
* shouldUpdateFocusInContext
  * フォーカス可能かどうかを判断
* didUpdateFocusInContext:withAnimationCoordinator:
  * フォーカスが新しいViewに移った直後に呼び出される
#### フォーカスの動き
#### フォーカス不要なビュー
触れないビューなどはフォーカス不可
* canBecomeEnabledがNO
* HiddenがYES
* alphaがNO  
など  

#### デバッグ
* クイックルックでデバッグできる
* 直前のfocused viewは赤
* 探索経路のフォーカスは赤のドット
* 赤枠が次にフォーカスが移るビュー
* フォーカス可能なフォーカスガイドは青枠

### Parallax Artwork
* 奥行きを表現する画像
* アプリアイコンには必須
* 他のUIにはOptional

#### Parallax Viewer
* アップルから提供されているlsrの表示、作成アプリ
* 画像を奥から貼り付けると画像が立体的に表示される

### まとめ
* TVMLとjsでプログラムが書ける
* リソースが制限されている
  * アプリのサイズは最大200MB
* フォーカスという概念が重要
* Parallax Artworkが必須

## Search APIsとUniversal linksの活用方法

<iframe src="//www.slideshare.net/slideshow/embed_code/key/mTpmtvkl2y3cgu" width="425" height="355" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC; border-width:1px; margin-bottom:5px; max-width: 100%;" allowfullscreen> </iframe> <div style="margin-bottom:5px"> <strong> <a href="//www.slideshare.net/kitasuke/search-apis-universal-links" title="Search APIs &amp; Universal Links" target="_blank">Search APIs &amp; Universal Links</a> </strong> from <strong><a href="//www.slideshare.net/kitasuke" target="_blank">Yusuke Kita</a></strong> </div>

### Myworks
* Cardio - Simple Health Kit

### How it Works
* インデックスを貼る
* on-device index
  * ユーザのアイテムの回覧など
* Apple's Cloud Index
  * Public

### Search APIs
#### UserActivitys
  * プライベートとパブリックどちらもいける
  * プロパティを指定
  * タップしたらアプリ側のAppDelegateで拾える
  * publicに出るのは複数のユーザが見るパブリックのコンテンツは出て来やすくなる
  * プライバシーに関わるものはPrivateにそれ以外はPublicに

#### CoreSpotlight
  * Privateのコンテンツ専用
  * インデックスしたアイテムの更新、削除もできる
  * CSSearchableItemをインスタンス化して使う
  * インデックス追加はメソッドを呼ぶだけ
  * アプリ側で拾うメソッドはNSUserActivityと同じ

#### Web Markup
  * 自分がアプリ持っていなくても出せるというのが重要なのでWebとの連携が重要
  * deeplinkに対応させるだけでAppleのクローラーが探してくれて勝手に使える
  * optionalだがメタ情報を入れることが推奨されている
    * ドキュメントでも何度も強調されている
  * AppleBotはどうやって探すか
    * salesURL、marketingを見てさがすので入れといたほうが良い

#### Deeplink
  * UniversalLinksとこれまでのCustom URL Schem2つあるが、UniversalLinksを推奨している
    * unique
    * Secure

### 検索ランキングに反映される要素
  * 関連性を重視してる（URL Popularity）
    NSUserActivity、CoreSpotlight、Web のuniqueIdを同じにすると相乗効果がある
  * Engagement
  * UX
    * 適度に丁度良い情報を表示しましょう
    * KeyWordsプロパティを上手く使う
      * 同じような意味の単語を入れておくと良い
    * 検索結果から表示した時にいきなりログインがでてくるというのはダメ
    * 検索結果をタップした後から表示までのスピード

### コード
* https://github.com/shinobicontrols/iOS9-day-by-day  
の 01-Search-APIsを元にしている  
* CSAttributesetのプロパティでsupportPhoneCallプロパティで電話をかけるActionを表示したりできる
* ViewControllerのUIResponderのプロパティにactivityというのがあって、そこにセットすると表示されやすくなるよう

### Q&A
* 上手く使っているアプリは?
  * AirBandB
  * Yelp
  * everNoteなど

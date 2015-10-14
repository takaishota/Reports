iOS 9 週連続 Bootcamp！3週目 @dots
---
http://eventdots.jp/event/571250

## AddressBookからContactsへ/田中 孝明@クラスメソッド

### 連絡先について
* 連絡先に登録されているユーザのデータベースを管理

#### どんなアプリに使われてる
* Line  
* Ingress
など

#### 活躍の場の例
* サポートデスクの連絡先の追加
* 社員の連絡先を追加する
* 指定された連絡先のみを削除する

### AddressBookとContactsについて
#### フレームワーク
* どちらにもUIとsuffixがついてるフレームワークがある
#### ContactsUI
* ビューコントローラーを生成し、presentViewするだけで使用できる
* これだけで一覧、詳細表示が使える

### What's New in iOS9
* AddressBookフレームワークがiOS9から非推奨になった
* Contactsフレームワークが追加された
* iOS8以下もサポートする場合は共存させる必要がある
  -> iOS8のサポート切れのタイミングで切り離す

### AddressBookでは--だったものがContaactsでは~~になる
#### AddressBook
* iOS専用の連絡先アクセスAPI
* 単一スレッドからしかアクセスできない

#### Contaacts
* iOS/Mac両方の連絡先API
* watchOS2に対応
* thread-safe（fetch/write）
  * メインスレッドをブロックしない仕組みが提供されている

### Privacyについて
#### アラート
* 連絡先にアクセスする際には許可を求めるアラートが表示される
* 連絡先アクセス許可状態を取得
    NotDetermined、Restriced、
* 許可をユーザに問い合わせるメソッドのブロック関数にステータスが入った変数が渡されてくる
* 一度、アラートが表示されるとその後なかなか表示されない
* 設定 > プライバシー > 連絡先 で変更可能

#### ユーザの取得
* idからの検索
  * AddressBook
      RecordIDを指定して取得
        int32型
  * Contaacts
      CNContact.identifierを指定して取得
        String型
          -> RecordIDとCNContact.identifierには互換性がない
* 名前からの検索
  * 姓、名、読みから検索できる
  * Contacts
      * keysToFetchで指定されていないプロパティへはアクセスできない
      * アクセスする前にキーが指定されているかをチェックする必要がある

### 連絡先の追加
  * AddressBook
      * データベースに該当するものを作成する
      * ABRecordRefを取得する
      * 必要なプロパティをセットする
      * AddressBookに対する操作を指定する
      * AddressBookに対するセーブを実施する
  * Contacts
      * データベースに該当するものを作成する
      * CNMutableContactsを作成する
      * CF~を取得
      * 必要なプロパティを設定する
      * CNSaveRequestへデータベースへの操作を指定する
      * CNContactStoreに対してセーブを実施する
#### Contacts Changed Notifications
  * CNContactStoreDidChangeNotification
  * 連絡先データの変更があるとNotificationを受け取れる

## 可能性が広がるWatchApp開発/酒多 優太@Retty
### Reetyってなに
* 口コミの制度を重視した実名制のグルメサービス
* だれかに勧めたいお店の情報が集まる
* 月間ユーザが1000万人を突破
* 今後はユーザの好みに合わせたリコメンドができるように

### RettyアプリをwatchOS2アプリに対応させた話
* Objective-Cで書かれたOS1向けのアプリをSwiftで書き直した
* WatchOS2 Appはbitcode対応しないといけない
#### bitcodeってなに
* LLVM IRを実行形式に埋め込むためのフォーマット
* Appleが突然CPUアーキテクチャを変更したデバイスを売り始めても
開発者がそれに対応してビルドする必要がない
* 含まれているFrameWork全てにbitcodeが含まれていないといけない
* watch向けアプリが動かないとリジェクトされる

#### WatchOS1、2の違い
* ネイティブ動作ができるようになった
#### 新機能
* 公式Appでしか使えなかった機能が使えるようになった
* Watch App Extensionがネイティブで動くことでiPhoneがなくても大抵のことができるようになった
  * WatchConnectivity
  * Security
  * CoreLocation
  をつかった
* BackGround
  * OSがいい感じのタイミングで転送
  * 転送前にキューに入ってくれる
  * 3種類の転送方法
    * Application Context
      最新のオブジェクトのみ送りたい
      [String:AnyObject]型
    * UserInfo
      全てのデータを送りたい
      [String:AnyObject]型
    * File
      NSURLとString:AnyObject飲めたデータ
    * Interractive
      すぐに転送が始まる
      NSDataや[String:AnyObject]型
      * Reachableであることが条件
        * Wathc Appがアクティブであること
        * 少なくともバックグラウンドでiOSアプリが起動していること

#### どんなアプリが良いか
* 小さい画面で画像を見てもあまり嬉しくない
* ましてや文章を読みたくない
* 操作中に常に左手をあげないとダメ

#### 今回注目した機能
* 豊富なセンサー類
* iPhoneを出すほどでもないちょっとした操作
##### 作ってみた
  * AppleWatchで取得した心拍数をラズペリーパイに送ってそれに合わせてLEDを点滅させる
  * 家電の操作  
    -> 完成できなかった
    * 赤外線センサを買ってきたが、光が弱すぎて反応しなかった

## モバイルバックエンド勉強会
* DynamoDB
* Elixir
* Amazon API Gateway/AWS Lambda、またそれらを利用したサーバーレスフレームワークであるJAWSなど

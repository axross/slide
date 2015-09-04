# Introduction to Redux

## whoami

axrossって名前でやってます。
少し前にGunosyにジョインして、JavaScriptを書いています。

## "Gunosy Manga"

で、どこでReact使ってるのか、っていうと、グノシーマンガというコンテンツがありまして、これはGunosyのモバイルアプリの中でマンガが読める、というものです。
「某少年の事件簿」とか、「某カンタービレ」とかが読めます。
で、これはReactとReact RouterとRedux、あとBemmerというものを使って作っています。

## Redux

で、今日は、そのうち「Redux」というライブラリについて話します。

## What is Redux?

で、「Redux」って聞いたことある人どれくらいいらっしゃいますか？

ReduxのリポジトリのREADMEの冒頭にはこのように書いてあります。

## What is Redux?

日本語にすると、「JavaScriptアプリケーションのための革新性のない状態コンテナ」ですね。

## Family of Flux

Reduxは、Fluxの一種と思ってもらえればよいでしょう。

## Family of Flux

Fluxの実装、亜種には代表的なものがFluxxor、Reflux、Flummoxなどとありますが、Reduxもその一種です。

## Flummox introducing Redux

中でも、Flummox。Reduxの名前をここから知った方も多いんじゃないでしょうか。
今年の1月中旬ごろに、このような文章がFlummoxのREADMEの冒頭に書き足されました。

## Flummox introducing Redux

日本語にすると、「バージョン4.0は最後のメジャーリリースになるだろう。代わりにReduxを使ってくれ。あれはマジで素晴らしい。」

## Redux is...

Flummoxの作者は今やReduxのMiddlewareとか作ったりしていて、Redux触ってると何かと参考になってお世話になることが多いです。まあそれは置いといて、データフローはFlummoxと似てます。で、Flummoxよりも「状態の管理」というところに重きを置いているように感じられます。

Flummoxの作者が手放しで賞賛するのは、データフローがFlummoxのものと似ていながら、Reduxにはさらに開発者にとって優しいアーキテクチャになっているからです。

<!-- ## Flummox Data Flow

Flummoxのデータフローはこのようになっています。
ComponentはStoreとconnectし、propsとしてStoreの値を受け取り、変更をdescribeします。ユーザーの入力などによって、Componentを通してActionの関数を実行する。ActionはStoreにdescribeされており、最終的に変更がStoreに通じ、Componentにも変更が反映されるというわけです。

## Redux Data Flow

Reduxのデータフローはこのようになっています。詳細な説明に入る前に、なぜReduxを作ったのか、そのあたりの話をしましょう。 -->

## Motivation

では、なぜReduxが良いのか、という話をします。

## SPA get more state needs to be managed

ドキュメントの中で、Reduxの作者はこう言っています。

JavaScriptのSingle Page Applicationを作ることが当たり前になって、どんどん凝ったつくりを求められるようになってきた。それに応じて、より多くの状態の管理が必要になった。

## too Hard to managing

絶えず変化する状態を管理するのは難しい。作っているうちに、自分の作ったアプリケーションの挙動を追い切れなくなってしまう。
そうすると、バグ修正の時に再現性を得るのが難しく、機能追加の時にも障害になる。

## React is great, but...

Reactによって状態とDOMは切り離され、多少マシにはなりました。Componentは値によって参照透過にDOM操作をする関数として機能しますが、その「値」、アプリケーションの状態の管理については手付かずの状態です。

## We are still on one's way Flux

僕らはそれをFluxというフローに当てはめて解決しようとしていますが、中でもReduxはこの状態の管理を一番うまくできるFluxかな、と僕は思います。

## Data Flow

では、Reduxのデータフローについてお話します。

## Single State Tree

まず、中核となるSingle State Treeについて話させてください。

###

Reduxの状態管理は、Single State Treeという名のとおり、1つの状態ツリーでなされています。

###

状態、Stateはツリー状にぶらさがっており、

###

それぞれのStateにはReducerという存在が紐付いています。

## Reducer

ReducerはStateのフィルター、あるいはマッパーであると言えます。受け取ったメッセージに対して、「自分と紐付いているStateを変更するかどうか」と「そのStateをどう更新するか」を担います。

## Data Flow

データフローは、Fluxの「一方向であること」や、「Observerパターン・モデル」な部分をまるごと継承しています。

###

Viewはイベントに応じて、Actionを用いてdispatchします。

###

Actionはtypeや値を含むObjectを返す存在です。

## in the Code

コードで説明するとこんな感じで、

###

本当にただのObjectを返すだけの単純な関数です。

## Data Flow

###

dispatchはあくまでView、ReactならComponentが行います。

###

dispatchされたメッセージは一度、すべてのReducerが受け取ります。

###

Reducerはメッセージ中のActionのtypeなどによってフィルタします。

## in the Code

コードで説明するとこんな感じで、

###

1行目のinitislStateっていうのはStateの初期状態です。

###

3行目の関数がReducerで、メッセージを受け取るとコールされます。

###

中では、こんな感じでフィルタリングします。このへんは手動で柔軟に設定できます。

###

フィルタリングして一致すれば、戻り値によってStateを更新します。

###

関係ないものは同じように戻り値で、変更していないStateを返すことでスルーします。

## Data Flow

###

このように、Reducerはメッセージを受け取り、必要に応じてStateを更新します。

###

ViewはStateを購読することで、

###

更新が伝搬し、画面が更新されます。

## Others

## With React Router


## Store is Single State Tree

では、ReduxのData Flowの話に戻りましょう。まずは中核となる、Single State Treeという概念についてお話します。Single State Treeは、他のFluxにおけるStoreにあたる概念です。

## State is updated by only Reducer

Single State Treeはその名のとおり、Stateのエントリポイントが単数です。それぞれの状態はReducerという存在と紐付いており、Stateの更新は必ずこのReducerを通して行われます。

## Reducer receives the all Messages

Reducerは、「Stateをどう更新するか」という役割を担います。あらゆるメッセージは、必ずすべてのReducerを通ります。その上で、そのメッセージはこのReducerで処理すべきかどうか、フィルタリングするのです。最終的に、メッセージから値を取り出し、自身と紐づくStateを更新します。

## Component connecting State

Componentは、必要に応じてconnectし、Stateの変更を購読します。これにより、Fluxのような一方向のデータフローが成り立っています。

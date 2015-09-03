# Introduction to Redux

##

## Redux

Reduxというライブラリについて話します。

## Predictable state container for JavaScript apps

Reduxとは？リポジトリのREADMEの冒頭にはこのように書いてあります。日本語にすると、「JavaScriptアプリケーションのための革新性のない状態コンテナ」となります。

## Redux is family of Flux

Reduxは、Fluxの一種と思ってもらえればよいでしょう。Fluxの実装、亜種はFluxxor、Reflux、Flummoxなどとありますが、Reduxもその一種です。

## Flummox 4.0 will likely be the last major release. Use Redux instead. It's really great.

FlummoxというFluxの亜種があります。Reduxの名前をここから知った方も多いんじゃないでしょうか。
今年の1月中旬ごろに、このような文章がFlummoxのREADMEの冒頭に書き足されました。「バージョン4.0は最後のメジャーリリースになるだろう。代わりにReduxを使ってくれ。あれはマジで良い。」

## Redux resembles Flummox

Flummoxの作者が手放しで賞賛するのは、Reduxの仕組みがFlummoxのものと非常に似ているからです。

## Flummox Data Flow

Flummoxのデータフローはこのようになっています。
ComponentはStoreとconnectし、propsとしてStoreの値を受け取り、変更をdescribeします。ユーザーの入力などによって、Componentを通してActionの関数を実行する。ActionはStoreにdescribeされており、最終的に変更がStoreに通じ、Componentにも変更が反映されるというわけです。

## Redux Data Flow

Reduxのデータフローはこのようになっています。詳細な説明に入る前に、なぜReduxを作ったのか、そのあたりの話をしましょう。

## SPA get more state needs to be managed

ドキュメントの中で、作者はこう言っています。

JavaScriptのSPAは、凝った作りを求められるようになってきている。それに応じて、より多くの状態の管理が必要になった。
絶えず変化する状態を管理するのは難しい。作っているうちに、自分の作ったアプリケーションの挙動を追い切れなくなってしまう。
そうすると、バグ修正の時に再現性を得るのが難しく、機能追加の時にも障害になる。

## Predictable state container for JavaScript apps

ドキュメントの最初には、このような「アプリケーションの状態の管理の難しさ」について挙げられています。
Reactによって状態がDOMと切り離され、多少マシにはなりました。Componentは値によって参照透過にDOM操作をする関数として機能しますが、その「値」、アプリケーションの状態の管理については手付かずの状態です。

僕らはそれをFluxというフローに当てはめて解決しようとしていますが、中でもReduxはこの状態の管理を一番うまくできるFlux亜種かな、と僕は思います。

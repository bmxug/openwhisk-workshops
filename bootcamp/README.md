# Table of Contents

- [Preface](#preface)
- [Serverless Computing](#serverless-computing)
- [環境の準備](#prepare-your-engines-)
- [サーバーレスをはじめよう!](#サーバーレスをはじめよう)
  * [アクション](#アクション)
    + [JavaScriptのアクションの作成と実行](#javascriptのアクションの作成と実行)
    + [非同期型のアクションの作成と呼び出し](#非同期型のアクションの作成と呼び出し)
    + [アクションにパラメータを引き渡す](#アクションにパラメータを引き渡す)
    + [デフォルトのパラメータを設定する](#デフォルトのパラメータを設定する)
    + [外部APIの呼び出しにアクションを用いる](#外部APIの呼び出しにアクションを用いる)
    + [パッケージを用いて複数のアクションを連続実行する](#パッケージを用いて複数のアクションを連続実行する)
  * [トリガーとルール](#トリガーとルール)
  * [ルールによるトリガーとアクションの連携](#ルールによるトリガーとアクションの連携)
  * [依存性(dependencies)のアップロード](#依存性dependenciesのアップロード)
- [さらに深い理解を求めて](#さらに深い理解を求めて)
  * [IBM Cloud Functions UIを利用する](#ibm-cloud-functions-uiを利用する)
  * [アクション](#アクション-1)
    + [Rest形式でアクションを呼び出す](#rest形式でアクションを呼び出す)
    + [web actionsを通してアクションを呼び出す](#web-actionsを通してアクションを呼び出す)
      - [web actionによるレスポンス](#web-actionによるレスポンス)
    + [アクションの定期実行](#アクションの定期実行)
  * [ログ](#ログ)
  * [パッケージの活用](#パッケージの活用)
    + [アクションのシーケンス化](#アクションのシーケンス化)
  * [トリガー](#トリガー)
  * [ルール](#ルール)
  * [モニタリング](#モニタリング)
- [Build a weather engine!](#build-a-weather-engine-)
  * [Address to locations service](#address-to-locations-service)
  * [Forecast from location service](#forecast-from-location-service)
  * [Sending messages to Slack](#sending-messages-to-slack)
  * [Creating the weather bot using sequences](#creating-the-weather-bot-using-sequences)
  * [Bot forecasts](#bot-forecasts)
  * [Connecting to triggers](#connecting-to-triggers)
  * [Morning forecasts](#morning-forecasts)
- [サーバーレスなマイクロサービスバックエンドを構築する](#サーバーレスなマイクロサービスバックエンドを構築する)
  * [はじめてのAPI](#はじめてのapi)
    + [エンドポイントにアクションをマッピングする](#エンドポイントにアクションをマッピングする)
  * [サーバレス式図書管理アプリケーション](#サーバレス式図書管理アプリケーション)
    + [Cloudantのインスタンスの作成](#cloudantのインスタンスの作成)
    + [データベースを作成する](#データベースを作成する)
  * [気象サービスの出力](#気象サービスの出力)
- [より複雑なサーバレスアプリケーションを構成する](#より複雑なサーバレスアプリケーションを構成する)
  * [はじめよう](#はじめよう)
  * [はじめてのComposition](#はじめてのcomposition)
  * [コンポジションのさらなる探求](#コンポジションのさらなる探求)
  * [ネスティングとデータ転送](#ネスティングとデータ転送)
  * [インラインコーディング](#インラインコーディング)
- [IBM App ConnectとMessage Hub](#ibm-app-connectとmessage-hub)
- [Special fuel for your engine!](#special-fuel-for-your-engine-)
  * [Developing with VS Code](#developing-with-vs-code)
  * [Developing with the Serverless Framework](#developing-with-the-serverless-framework)
    + [Installing the Serverless Framework](#installing-the-serverless-framework)
    + [Working with Actions](#working-with-actions)
    + [Working with Sequences](#working-with-sequences)
    + [Connecting API Endpoints](#connecting-api-endpoints)
    + [Working with Triggers and Rules](#working-with-triggers-and-rules)
    + [Packaging your weather services](#packaging-your-weather-services)
- [Node-REDとIBM Cloud Functions](#node-redとibm-cloud-functions)
  * [Node-REDのインストール](#node-redのインストール)
  * [Node-REDをの開始](#node-redの開始)
  * [Node-REDで"Hello World"](#node-redで-hello-world-)
    + [Injectノードの追加](#injectノードの追加)
    + [Debugノードの追加](#debugノードの追加)
    + [ノードの連結](#ノードの連結)
    + [デプロイ](#デプロイ)
    + [Functionノードの追加](#functionノードの追加)
  * [Node-REDにノードを追加](#node-redにノードを追加)
    + [Node-REDからIBM Cloud Functionsアクションを呼び出し](#node-redからibm-cloud-functionsアクションを呼び出し)
  * [Node-REDからのFunctionsトリガーの呼び出し](#node-redからのfunctionsトリガーの呼び出し)
    + [新規IBM Cloud FunctionsアクションをNode-REDから作成](#新規ibm-cloud-functionsアクションをnode-redから作成)
- [イケてるアプリは目前に!](#イケてるアプリは目前に)
  * [Vision App](#vision-app)
  * [Dark Vision](#dark-vision)
  * [Skylink](#skylink)
- [もっと知りたい！](#もっと知りたい)

# 序文

はじめに、 **IBM Bluemix OpenWhisk** は最近 **IBM Cloud Functions** に改名されました。 これは、公式の見解では、 **Apache OpenWhisk** は、Apacheで利用可能なオープンソース・プロジェクトを意味し、 **IBM Cloud Functions** はIBMのパブリック・クラウド上で動作するIBMのサーバーレス・プラットフォームを指します（ IBM Bluemix）。 IBM Cloud Functions は、両方のプロジェクトが同じコアコードベースを共有するため、Apache OpenWhiskに完全に基づいています。

> Before you start, please note that **IBM Bluemix OpenWhisk** has recently been renamed to **IBM Cloud Functions**. This means that, from an official point of view, **Apache OpenWhisk** refers to the open-source project being available on Apache, while **IBM Cloud Functions** refers to IBM's serverless platform running on top of IBM's public cloud (IBM Bluemix). IBM Cloud Functions is entirely based on Apache OpenWhisk as both projects share the same core codebase.

In the following we will, for reasons of simplicity and since most examples would also work on any (locally) hosted OpenWhisk deployment, refer to **OpenWhisk** only and not distinguish between Apache OpenWhisk and IBM Cloud Functions even though we will run many of the examples on top of IBM Bluemix.

During this workshop you will learn how to develop **serverless applications** composed of loosely coupled microservice-like functions. You'll explore OpenWhisk's latest *CLI* (command line interface) and UI and become an OpenWhisk star by implementing a weather bot using *IBM's Weather Company Data service* and *Slack*. You will also investigate how to use other capabilities such us our API Gateway integration allowing you to easily expose functions via API endpoints. You will have a first glance at our research-driven tech-preview called *Composer* allowing you to compose more complex serverless applications by combining multiple functions using control logic and state. Finally, you will find out how to package and deploy your entire serverless application together using the *Serverless Framework*.

We wish you a lot of fun and success...


# サーバーレスコンピューティング

**サーバーレスコンピューティング**（別名 **Funcions-as-a-Service (FaaS)** ）は、サーバーの存在が完全に抽象化されているモデルを指します。
つまり、サーバーがまだ存在していても、開発者はサーバの運用を気にする必要から解放されます。
スケーラビリティ、高可用性、インフラストラクチャセキュリティなどの低レベルのインフラストラクチャと運用を考慮する必要から解放されています。
したがって、サーバーレスコンピューティングは、開発者が付加価値の高いコードを開発することに迅速に集中できるように、基本的にメンテナンスの労力を軽減することです。

サーバレスコンピューティングは、クラウドネイティブアプリケーションの開発を簡素化し、
  特に複雑なアプリケーションを簡単に交換できる小さな独立したモジュールに分解するマイクロサービス指向のソリューションです。

サーバレスコンピューティングは、特定のテクノロジを参照するものではありません。その代わりに前に説明したモデルの基礎をなす概念を参照します。
それにもかかわらず、OpenWhiskのようなサーバレスモデルに続く開発アプローチの緩和が近年浮上しています。

OpenWhiskはクラウドファーストの分散イベントベースのプログラミングサービスで、イベントに応じてコードを実行できるFaaSプラットフォームです。

前述のサーバレスデプロイメントモデルとオペレーションモデルを提供し、
どのような規模でも細かい価格設定モデルを使用して、正確なリソースを提供します。- それ以上でもそれ以下でもありません - 実際に実行されるコードに対してのみ料金を請求します。柔軟なプログラミングモデルを提供します。*Java, JavaScript, PHP, Python, and Swift* などの言語や、*Docker* コンテナを使用してカスタムロジックの実行をサポートします。これにより、小さなアジャイルチームは既存のスキルを再利用し、目的に合った方法で開発することができます。また、開発したビルディングブロックをつなげて動作させるツールも提供します。オープンであり、ベンダーロックインを避けるためにどこでも実行できます。

まとめると、OpenWhiskは以下を提供します。
* ... 豊富なビルディングブロックを簡単につけたりはずしたりできます
* ... 低レベルで少ないインフラストラクチャと運用によりビジネスへの付加価値を重視することに注力出来ます
* ... シーケンスを利用して、簡単にマイクロサービスをつなげることが出来ます
* ... 制御ロジックと状態を使用して複数の機能を組み合わせることで、より複雑なサーバレスアプリケーションを構成することが出来ます（ * tech-preview * ）

まとめると、我々のバリューポジションと他との違いは:
* OpenWhiskはインフラストラクチャの複雑さを隠し、開発者がビジネスロジックに集中できるようにします。
* OpenWhiskはスケーリング、ロードバランシング、ロギング、フォールトトレランス、メッセージキューなどの低レベルの詳細を処理します。
* OpenWhiskは、さまざまな分野（分析、コグニティブ、データ、IoTなど）からのビルディングブロックの豊富なエコシステムを提供します。
* OpenWhiskは公開されており、オープンコミュニティをサポートするように設計されています。
* OpenWhiskはOpenWhiskパッケージ経由でマイクロサービスを共有できるオープンエコシステムをサポートしています
* OpenWhiskは、開発者が近代的な抽象化と連鎖を使用してソリューションを構成することを可能にします。
* OpenWhiskはJava、JavaScript、PHP、Python、Swiftなどの複数のランタイムやDockerコンテナにカプセル化された任意のバイナリプログラムをサポートします。
* OpenWhiskは実行するコードに対してのみ課金されます

OpenWhiskモデルは基本的に３つの概念で構成されています。
* `trigger` イベントが発生するクラス
* `action`, イベントハンドラ -- イベントに応答して実行されるコード
* `rule`, トリガーとアクションの関連付け

サービスはトリガとして発行するイベントを定義し、開発者はイベントを処理するアクションを定義します。

開発者は、必要なアプリケーションロジックの実装に注意するだけで済みます。システムは残りの部分を処理します。

# 環境の準備

はじめる前に:
* 作業を進めていくうちに、CLIがこのガイドとは異なる結果を示すかもしれません。これはあなたがこの文書が作成された際とは異なるnamespaceを利用していることに起因するものです。これに伴う差異は極めて小さく、nameの関わる箇所でのみ起きる事象となります。
* 【重要】*Linux* ユーザーの方へ:`cURL`などいくつかのツールを追加でインストールする必要があります。(e.g. *Ubuntu* の場合以下のコマンドでインストールできます。`sudo apt-get update && sudo apt-get install curl`)
* 【重要】*Windows* ユーザーの方へ: *Git* (https://git-for-windows.github.io/)をダウンロードし *Git bash* から作業を行うことを推奨しています。また`cURL` for Windows (https://curl.haxx.se/download.html)のダウンロードも推奨しています。

IBM Cloud Functionsの利用のはじめの一歩:
1. ブラウザウィンドウを開きます。
2. https://console.ng.bluemix.net/openwhisk/ にアクセスします。
3. IBM Cloudにログインします。  
   アカウントを持っていない場合は`「フリーアカウントの作成」`をクリックするか、
   https://console.ng.bluemix.net/registration/ に直接アクセスしてアカウントを作成します。
4. `アメリカ南部`または`英国`のどちらかのリージョンを選択します。(自国に近い地域を選択すると良いでしょう。) `アメリカ南部`を選択しなかった場合、今後出てくる`URL`内の`.ng`フラグメントを他のものに変える必要があります。`英国`の場合は`.eu-gb`となります。
5. `「CLIのダウンロード」`をクリックします。
6. 手順の1から3に従って作業します。(4は必須ではありません) ここには、CLIのダウンロード、Cloud Functionsプラグインをインストール、 APIのエンドポイント・組織・namespaceを選択してBluemixにログインするという作業が含まれます。

# サーバーレスをはじめよう!

ダウンロードしたCLIは、*アクション・トリガー・ルール・シークエンス* の作成といったIBM Cloud Functionsの基本操作に対応します。それではどのようにCLIを操作すればよいかを学習しましょう。

## アクション

*アクション* はIBM Cloud Functions上で機能する、短いコードのまとまりです。

### JavaScriptのアクションの作成と実行

このアクションは簡単な *JavaScript* で構成され、*JSON* オブジェクトを返します。

まず、任意のエディターを開き(例： *Atom* エディター https://atom.io/)、`hello.js`というファイルを作成して以下のコードを入力します。

```javascript
function main() {
    return { message: "Hello world" };
}
```

ファイルは任意のタイミングでいつでも保存してかまいません。

次に、ターミナルウィンドウを開き、`hello.js`を保存したディレクトリに移動します。以下のコマンドを入力して、`hello.js`の関数を反映した`hello`というアクションを実行しましょう。

<pre>
$ bx wsk action create hello hello.js
<b>ok:</b> created action <b>hello</b>
</pre>

作成したアクションはいつでも以下の方法でリスト化して表示できます。

<pre>
$ bx wsk action list
<b>actions</b>
hello                                  private nodejs:6
</pre>

アクションを実行するには```bx wsk action invoke```コマンドを使います。 *ブロッキング* (i.e.*同期*) の実行はアクションが完遂され結果を返されるまで待機されます。その設定には```--blocking```オプション(または```-b```)を利用します。

<pre>
$ bx wsk action invoke --blocking hello
<b>ok:</b> invoked <b>hello</b> with id <b>dde9212e686f413bb90f22e79e12df74</b>
[...]
"response": {
    "result": {
        "message": "Hello world"
    },
    "status": "success",
    "success": true
},
[...]
</pre>

上記のコマンドによるアウトプットには2つの重要な情報が含まれています。
*	```activation id``` (```dde9212e686f413bb90f22e79e12df74```)
*	```activation response``` (及びその出力結果)

この```activation id``` は将来のとある時点での(非同期) invokeのログや結果を取り出す際に利用します。もし```activation id```を書置きしておくことを失念しても、いつでも実行結果のリストを表示することができます。

<pre>
$ bx wsk activation list
<b>activations</b>
dde9212e686f413bb90f22e79e12df74             hello                                   
eee9212e686f413bb90f22e79e12df74             hello
</pre>

最新の```activation id```が最上列に来るようになっています。

特定のアクションの実行結果を確認するには(以下のコマンド上の```activation id```を各々の```id```に書き換える必要があります。):

<pre>
$ bx wsk activation get dde9212e686f413bb90f22e79e12df74
<b>ok:</b> got activation <b>dde9212e686f413bb90f22e79e12df74</b>
[...]
"response": {
    "status": "success",
    "statusCode": 0,
    "success": true,
    "result": {
        "message": "Hello world"
    }
},
[...]
</pre>

アクションを削除するには:

<pre>
$ bx wsk action delete hello
<b>ok:</b> deleted action <b>hello</b>
</pre>

アクションの削除が成功したかを確認するには:

<pre>
$ bx wsk list
entities in namespace: <b>default</b>
<b>packages</b>
<b>actions</b>
<b>triggers</b>
<b>rules</b>
</pre>

### 非同期型のアクションの作成と呼び出し

*非同期* で実行される *JavaScript* 関数は`main`関数が返されたあとにアクティベーションを返す必要があります。これは`Promise`を返すことで遂行することができます。

それでは`asyncAction.js`というファイルを作成し、下のコマンドを入力しましょう。

```javascript
function main(params) {
    return new Promise(function(resolve, reject) {
        setTimeout(function() {
            resolve({ message: "Hello world" });
        }, 2000);
    });
}
```

`main`関数はアクティベーションがまだ完遂していないことを示す`Promise`を返します。

上記の例における`setTimeout`関数はコールバック関数をコールする前に2秒待機します。これは非同期コードであることを示し、`Promise`のコールバック関数に引き渡します。

`Promise`のコールバックは`resolve`と`reject`の２つの関数を実引数に持ちます。`resolve`のコールは`Promise`を履行し、アクティベーションが通常通り完遂したことを示します。

`reject`のコールは`Promise`を却下するために用いられるものでアクティベーションが異常終了したことを示します。

次に以下のコマンドを実行し、アクションを作成・実行します。:

<pre>
$ bx wsk action create asyncAction asyncAction.js
<b>ok:</b> created action <b>asyncAction</b>

$ bx wsk action invoke --blocking --result asyncAction
{
    "message": "Hello world"
}
</pre>

最後に以下のコマンドを実行し、アクティベーションログをフェッチしてアクティベーションが完遂するまでどのくらいかかるのかを確認してください。

<pre>
$ bx wsk activation list --limit 1 asyncAction
<b>activations</b>
b066ca51e68c4d3382df2d8033265db0       asyncAction

$ bx wsk activation get b066ca51e68c4d3382df2d8033265db0
{
    "start": 1455881628103,
    "end":   1455881648126,
    "duration": 2055,
    ...
}
</pre>

アクティベーションレコードとして表示されている`duration`エントリーを見れば、アクティベーションは2秒をわずかに上回っていることがわかります。

### アクションにパラメータを引き渡す

アクションはいくつかの名前つきのパラメータを伴って実行されるでしょう。

以下を実行し`hello`アクションを変更(及び保存)してください。

```javascript
function main(params) {
    return { message: "Hello, " + params.name + " from " + params.place };
}
```

もう一度アクションを作成します。

<pre>
$ bx wsk action create hello hello.js
<b>ok:</b> created action <b>hello</b>
</pre>

*JSON* ペイロードとしてあるいはCLIを通して、名前付のパラメータを引き渡すことができます。

<pre>
$ bx wsk action invoke -b hello -p name "Bernie" -p place "Vermont" --result
{
    "message": "Hello, Bernie from Vermont"
}
</pre>

`--result` パラメータ (または`-r`(invocateのブロッキングの際のみ利用可能) )は`activation id`を用いずにすばやく結果を表示した際に使います。

### デフォルトのパラメータを設定する

再度前述の`hello`アクションを、`name`(名前)と`place`(出身地)の2つのパラメータを伴った上でコールします。

毎回すべてのパラメータをアクションに引き渡すのではなく、特定のパラメータのみを *バインド* することができます。`place`パラメータをバインドし、`Vermont, CT`をplaceのデフォルト値としてみましょう。

<pre>
$ bx wsk action create helloBindParams hello.js --param place "Vermont, CT"
<b>ok:</b> created action <b>helloBindParams</b>

$ bx wsk action invoke -b helloBindParams --param name "Bernie" --result
{
    "message": "Hello, Bernie from Vermont, CT"
}
</pre>

アクションを実行すれば今後は`place`パラメータを指定する必要がなくなります。さらに、バインドされたパラメータはアクション実行時に別のパラメータを指定することで上書きされます。

### 外部APIの呼び出しにアクションを用いる

これまでにご紹介した例はそれだけですべてが充足した関数でした。もちろんそのような形式に限らず、外部APIを呼び出す形のアクションも作成することができます。

次の例では *Yahoo Weather Service* をinvokeし、特定の地域の気象情報を入手しています。

`weather.js`というファイルを作成し、以下を入力してください。

```javascript
var request = require("request");

function main(params) {
    var location = params.location || "Vermont";
    var url = "https://query.yahooapis.com/v1/public/yql?q=select item.condition from weather.forecast where woeid in (select woeid from geo.places(1) where text='" + location + "')&format=json";

    return new Promise(function(resolve, reject) {
        request.get(url, function(error, response, body) {
            if (error) {
                reject(error);
            }
            else {
                var condition = JSON.parse(body).query.results.channel.item.condition;
                var text = condition.text;
                var temperature = condition.temp;
                var output = "It is " + temperature + " degrees Fahrenheit in " + location + " and " + text;

                resolve({params: output});
            }
        });
    });
}
```

上記のアクションは *Yahoo Weather API* への *HTTP* リクエストの送信と *JSON* Resultから特定のフィールドを引き出すことを目的として *JavaScript request library* を利用しています。

例では、非同期アクションが必要であることも示されています。アクションは`Promise`を返しており、関数が返ってきた時点ではまだアクションの結果が取得できていないことを示しています。しかし、*HTTP* のコールが完遂した時点でのコールバックでは結果の取得は済んでおり、`resolve`関数への引数として前述したように引き渡されています。

それでは、以下のコマンドを実行してアクションを作成し実行しましょう。

<pre>
$ bx wsk action create yahooWeather weather.js
<b>ok:</b> created action <b>yahooWeather</b>

$ bx wsk action invoke --blocking --result yahooWeather --param location "Brooklyn, NY"
{
    "params": "It is 28 degrees Fahrenheit in Brooklyn, NY and Cloudy"
}
</pre>

### パッケージを用いて複数のアクションを連続実行する

複数のアクションをひとつなぎの *シーケンス* として実行することができます。
*パッケージ* を用いたアクションを通して、そのようなシーケンスをどのようにして使えばいいのかをお見せしましょう。

通常、どのパッケージを用いることが可能かを知るには以下のコマンドを利用します。

<pre>
$ bx wsk package list /whisk.system
<b>packages</b>
/whisk.system/cloudant                 shared
/whisk.system/alarms                   shared
/whisk.system/watson                   shared
/whisk.system/websocket                shared
/whisk.system/weather                  shared
/whisk.system/system                   shared
/whisk.system/utils                    shared
/whisk.system/slack                    shared
/whisk.system/samples                  shared
/whisk.system/github                   shared
/whisk.system/pushnotifications        shared
</pre>

次に、`/whisk.system/cloudant`パッケージに内蔵されているエンティティの一覧を表示するには以下のコマンドを利用します。

<pre>
$ bx wsk package get --summary /whisk.system/cloudant
<b>package</b> /whisk.system/cloudant: Cloudant database service
   (<b>parameters</b>: BluemixServiceName host username password dbname includeDoc overwrite)
<b>action</b> /whisk.system/cloudant/read: Read document from database
<b>action</b> /whisk.system/cloudant/write: Write document to database
<b>feed</b> /whisk.system/cloudant/changes: Database change feed
[...]
</pre>

出力結果は`/whisk.system/cloudant`が、`read`や`write`そしてトリガーである`changes`という *フィード* といった複数のアクションを実行していることがわかります。`changes`フィードは *Cloudant* データベースにドキュメントが追加された際にトリガーを起動します。

またパッケージは`username`、`password`、`host`、`port`といったパラメータも定義します。これらのアクションやフィードに対するパラメータは値を持っている必要があります。パラメータは *Cloudant* アカウントの管理のためのアクションを許可します。

このパッケージへのアクションにアクセスする1つの方法はバインドです(パッケージに直接アクセスすることも可能です)。バインドすると、namespace内のパッケージにリファレンスを作成できます。そのメリットは`/whisk.system/utils/actionName`の代わりとして、`myUtil/actionName`とアクセスするたびに記載されるようになることです。

それでは、`/whisk.system/utils`というパッケージのアクションのセットを利用してみましょう。

そのパッケージの中に何が含まれているか確認できますか？

バインドするためには以下のコマンドを利用します。

<pre>
$ bx wsk package bind /whisk.system/utils myUtil
<b>ok:</b> created binding <b>myUtil</b>
</pre>

これによって下記のアクションにアクセスできます。
* `myUtil/cat`:  テキストを *JSON* 配列に変換するためのアクション
* `myUtil/head`: 配列の中の最初の要素を返すためのアクション
* `myUtil/sort`: 配列の中のテキストをソートするためのアクション

上記のアクションのシーケンスとなる複合型のアクションを作成してみましょう。1つのアクションの結果が次のアクションの実引数となっていく様子が見て取れることでしょう。

<pre>
$ bx wsk action create myAction --sequence myUtil/sort,myUtil/head
<b>ok:</b> created action <b>myAction</b>
</pre>

The composite action above will return the first element of a sorted array:

<pre>
$ bx wsk action invoke -b myAction -p lines '["c","b","a"]' --result
{
    "lines": [
        "a"
    ],
    "num": 1
}
</pre>

ソートされた配列の最初の要素が返されることがわかるでしょう。

サービスを有効化するための独自のパッケージの作成方法に関する公式の文書はこちら
https://github.com/openwhisk/openwhisk/blob/master/docs/packages.md#creating-and-using-package-bindings

## トリガーとルール

*トリガー* はイベントのストリームの名前つきの"チャンネル"を意味します。

*location updates* を送信するためにトリガーを作成してみましょう。

<pre>
$ bx wsk trigger create locationUpdate
<b>ok:</b> created trigger <b>locationUpdate</b>
</pre>

トリガーが作成されているか確認するには以下のようにします。

<pre>
$ bx wsk trigger list
<b>triggers</b>
locationUpdate                         private
</pre>

イベントが起動するための名前つきのチャンネルを作っただけでは物足りませんね。

名前とパラメータを特定した上でトリガーを起動できるようにしてみましょう。

<pre>
$ bx wsk trigger fire locationUpdate -p name "Donald" -p place "Washington, D.C"
<b>ok:</b> triggered <b>locationUpdate</b> with id <b>11ca88d404ca456eb2e76357c765ccdb</b>
</pre>

今`locationUpdate`に起こしたイベントは今の状態では何もしません。何か働きを持たせるには、トリガーとアクションを関連付けるためのルールが必要です。

## ルールによるトリガーとアクションの連携

*ルール* トリガーとアクションを関連付けるために用いられます。これにより、イベントトリガーが起動するたびにアクションはイベントのパラメータとともにinvokeされます。

location updateがある度に`hello`アクションを呼び出すルールを作成してみましょう。必要となるパラメータはルールの`name`、トリガーそしてアクションです。

<pre>
$ bx wsk rule create myRule locationUpdate hello
<b>ok:</b> created rule <b>myRule</b>
</pre>

これで、location updateイベントが起こるたびに`hello`アクションが該当するイベントのパラメータとともに呼び出されます。

<pre>
$ bx wsk trigger fire locationUpdate -p name "Donald" -p place "Washington, D.C"
<b>ok:</b> triggered <b>locationUpdate</b> with id <b>2c0b4602f5a84ea1b049a57c059e1ec1</b>
</pre>

最新のアクティベーションをチェックした上でアクションが実際にinvokeされていることが確認できます。

<pre>
$ bx wsk activation list hello
<b>activations</b>
12ca88d404ca456eb2e76357c765ccdb       hello
8b61fbedb91144269fee474e5f503e67       hello
</pre>

オプションとなる実引数`hello`が結果をフィルターし、`hello`アクションが反映されていることが確認できるでしょう。

ご紹介済みですが、特定のアクションの呼び出し結果を入手する方法は以下となります。(`activation id`はご自身の作業環境でそれまでの作業の中で獲得した`id`に書き換える必要があります。)

<pre>
$ bx wsk activation result 12ca88d404ca456eb2e76357c765ccdb
{
    "result": "Hello, Donald from Washington, D.C."
}
</pre>

これでようやく`hello`アクションがイベントペイロードを受け取り変数を返していることが確認できます。

## 依存性(dependencies)のアップロード

単一の *JavaScript* ソースファイルにすべてのコードを書きあげる代わりに`npm`パッケージとしてアクションを実行することができます。(NodeJS (https://nodejs.org/) のインストールが必要です).

構成は以下のようになります。

まずこのように`package.json`を定義します。

```json
{
    "name": "my-action",
    "version": "1.0.0",
    "main": "index.js",
    "dependencies" : {
        "left-pad" : "1.1.3"
    }
}
```

次に、`index.js`をこのように定義します。

```javascript
function myAction(params) {
    const leftPad = require("left-pad");
    const lines = params.lines || [];

    return { padded: lines.map(l => leftPad(l, 30, ".")) }
}

exports.main = myAction;
```

アクションが`exports.main`で出力されていますね。このように、アクションハンドラーは、オブジェクトのやり取り(やオブジェクトの`Promise`)を許容するものであれば、どんな名称を取ることもできます。

このパッケージからIBM Cloud Functionsのアクションを作成するには以下の手順に従います。

まず、ローカル環境ですべての依存性をインストールします。

<pre>
$ npm install
</pre>

次に、すべてのファイル(および依存性)を含む.zipアーカイブを作成します。

<pre>
$ zip -r action.zip *
</pre>

そしてアクションを作成します。

<pre>
$ bx wsk action create packageAction --kind nodejs:6 action.zip
<b>ok:</b> created action <b>packageAction</b>
</pre>

CLIツールを用いて.zipアーカイブからアクションを作成する際には、明示的に`--kind`フラッグへ値を提供しなければなりません。

最後に他の作業と同じようにinvokeします。

<pre>
$ bx wsk action invoke --blocking --result packageAction --param lines '["and now", "for something completely", "different"]'
{
    "padded": [
        ".......................and now",
        "......for something completely",
        ".....................different"
    ]
}
</pre>

ほとんどの`npm`パッケージは`npm install`上の *JavaScript* ソースをインストールしますが、それに加えてバイナリアーティファクトをインストールしコンパイルするものもあります。アーカイブファイルのアップロードは現在バイナリ依存をサポートせず、 *JavaScript* 依存のみをサポートしています。バイナリ依存を含むアーカイブの場合にはアクションの呼び出しに失敗します。

# さらに深い理解を求めて

CLIに代わるものとして、IBM Cloud Functions UIというビジュアルコードエディタも、アクション・トリガー・ルール・シーケンスの作成といったIBM Cloud Functionsの基本的な作業を行うことができます。それでは、IBM Cloud Functions UIの使い方を学んでいきましょう。

## IBM Cloud Functions UIを利用する

ブラウザーウィンドウを開き、 https://console.ng.bluemix.net/openwhisk/ にアクセスし、「作成の開始」をクリックしましょう。

IBM　Cloud Functions UIは次のセクションを含みます。

1. `マイ･アクション`  
   `マイ・アクション`セクションにはあなたがそれまでに作成したアクションがリスト化されています。
   アクションをクリックすると、コードがエディタへとロードされます。
   アクションの上にカーソルをかざせばゴミ箱マークが出てきて、アクションを削除することができます。  
   この時点で最低でもこれまでに作成した`hello`アクションを確認することができるでしょう。

2. `マイ・シーケンス`  
   `マイ・シーケンス`セクションにはあなたがそれまでに作成したシーケンスがリスト化されています。
   シーケンスをクリックすればモデルがビジュアルモデラーへとロードされます。
   シーケンスにカーソルをかざせばゴミ箱マークが出てきて、シーケンスを削除することができます。

3. `マイ・ルール`  
   `マイ・ルール`セクションにはあなたが作成したルールがリスト化されています。
   ルールをクリックすればモデルがビジュアルモデラーへとロードされます。
   ルールにカーソルをかざせばゴミ箱マークが出てきてルールを削除することができます。
   この時点で最低でもこれまでに作成した`myRule`を確認することができるでしょう。

4. `マイ・トリガー`  
   `マイ・トリガー`セクションにはあなたが作成したトリガーがリスト化されています。
   トリガーにカーソルをかざせば、閃光アイコンをクリックしてトリガーを起動したり、ゴミ箱マークをクリックしてトリガーを削除したりすることができます。

## アクション

それではCLIを使ったときと同様にUIを使って簡単なアクションを作成して使い方を探ってみましょう。

まず、「`アクションの作成`」ボタンをクリックします。
次に、任意の名前(例：`helloUI`)を「`アクション名`」のボックスの中に入力しましょう。
他の項目はそのままにし、画面上の「`作成`」ボタンをクリックします。

オプションをいじらなくても、`言語`や`メモリー割り当て量`・`時間設定`などを編集したいと思うかもしれません。そういったときは`詳細はこちら`リンクをクリックしてより詳細な情報を取得しお好きに設定を変更して構いません。

以下のコードをエディターにコピーして既存で書かれたコードの上に上書きしてください。

```javascript
function main() {
    return { message: "Hello world" };
}
```

次に「`アクションを実行`」ボタンをクリックし、ブラウザから直接アクションのテストをしてください。
アクションを作動する前にそれをlive状態にする必要があります。なのでテスト状態を追え実際に作用させるには「`ライブにする`」ボタンをクリックしてください。
その後、「`この値で実行`」ボタンをクリックしてください。

アクションはパラメータの引渡しを必要としていませんので、*JSON* インプットを明示する必要はありません。

下の結果を確認できるはずです。

<pre>
{
    "message": "Hello world"
}
</pre>

次に、アクションがパラメータを持つ際にどのような動きをするのかを確認するために、再度`アクションの作成`ボタンをクリックしてください。
そして、再度、任意の名称(例：`helloUI2`)を入力し、`アクションの作成`ボタンをクリックしてください。

次に、下記のコードをエディタに上書きしてください。

```javascript
function main(params) {
    return { message: "Hello, " + params.name + " from " + params.place };
}
```

繰り返しになりますが、`アクションを実行`ボタンを、先ほどと同様にブラウザ上でこのアクションのテストの様子を確認してください。

今回は任意のパラメータが必要となりますので *JSON* 形式のインプットが必要となります。例えば、下記のような値をインプットします。

```json
{
    "name": "Andreas",
    "place": "Stuttgart, Germany"
}
```

すると、下記のような結果が現れるでしょう。

<pre>
{
    "message": "Hello, Andreas from Stuttgart, Germany"
}
</pre>

### Rest形式でアクションを呼び出す

アクションはCLIやIBM Cloud Functions UIを通してという形ではinvokeできません。また、*REST* APIのコールという形でもできません。*REST* APIエンドポイントに`POST`するという形をとることが必要です。

アクションに対する正しい *REST* APIエンドポイントを捉えるには、アクション(例：`helloUI`)を選択し、エディタの右下にある`RESTエンドポイントの表示`リンクをクリックします。

テストをするには、`cURL URL`を使います。`cURL URL`の隣にある`コピー`ボタンをクリックし実行してください。

例えば`hello UI`アクションをinvokeするには、このようにします。

<pre>
$ curl -d "{\"arg\":\"value\"}" "https://openwhisk.ng.bluemix.net/api/v1/namespaces/andreas.nauerz%40de.ibm.com_dev/actions/helloUI?blocking=true" -XPOST -H "Content-Type: application/json" -H "Authorization: Basic xxx="
</pre>

すると、以下の結果が確認できるでしょう。

<pre>
[...]
"response": {
    "result": {
        "message": "Hello world"
    },
    "success": true,
    "status": "success"
},
[...]
</pre>

### web actionsを通してアクションを呼び出す

Web actionsはIBM Cloud Functionsのwebベースのアプリケーションをすばやく構築するためのアクションです。これにより、IBM Cloud Functionsの認証キーを得ることなく、ウェブアプリケーションは匿名的にバックエンドプログラムにアクセスすることができます。認証・認可サービス(例：`Oauth`)の実装はアクションの作成者に委ねられています。

Web actionのアクティベーションはアクションの作成者が行います。このアクションはアクションの呼び出し者からオーナーへのアクションのアクティベーションにかかるコストを大きくします。いままで`hello`と呼ばれていたアクションをweb action enterとするには以下のようにします。

<pre>
$ bx wsk action update hello --web true
<b>ok:</b> updated action <b>hello</b>
</pre>

一度アクションを実行可能にすれば、新たな *REST* インターフェースを通したweb actionとして利用可能になります。

`URL`は以下のように構成されていますー`https://{APIHOST}/api/v1/web/{QUALIFIED ACTION NAME}.{EXT}`。このQualified Action Nameの部分には`namespace`・`packagename`・`action name`の3つのパートが盛り込まれています。web actionのQualified nameには名前付パッケージに内蔵されていなければ`デフォルトの`パッケージ名が盛り込まれているでしょう。`URI`の最後の部分には、`http`や`json`といった拡張子が入ります。web action APIのパスにはAPI keyではなく、`cURL`や`wget`が用いられます。それはブラウザに直接入力されます。

namespaceを`andreas.nauerz@de.ibm.com_dev`から自らのものに変更した上で、`https://openwhisk.ng.bluemix.net/api/v1/web/andreas.nauerz@de.ibm.com_dev/default/hello.json?name=Andreas&place=Stuttgart`を開いてみましょう。

どんなアクションもIBM Cloud Functions UIを用いてweb actionとして利用可能であることがわかるでしょう。また、web actionをinvokeするための正確な`URL`も見つけることができるでしょう。

このファイルはちょっとしたドリルとしてみなさんのために残しておきましょう。正しい場所はわかりましたか？

#### web actionによるレスポンス

web actionsは *HTTP* ハンドラーとして実装できます。*HTTP* ハンドラーは`ヘッダー`・`ステータスコード`・`ボディ`を有します。その場合でもweb actionは *JSON* オブジェクトを返す必要がありますが、その`コントローラー`となるIBM Cloud Functionsは、その結果が下記の *JSON* プロパティを含む場合、web actionの挙動を異にします。
* `ヘッダー`：キーをヘッダーネームとし、値をそのヘッダーの文字値とする *JSON* オブジェクト(デフォルトではヘッダーは有さない)
* `ステータスコード`: *HTTPステータスコード* (デフォルトでは200文字まで許容)
* `ボディ`: (バイナリデータのための)プレインテキストまたはbase64エンコード文字列

`コントローラ` はアクションが特定づけられた *ヘッダー* に紐づけられます。もし対象となるヘッダがないようであれば、 *リクエスト/レスポンス* 終了時に *http* クライアントと紐づけられます。同様に、 `コントローラ`は与えられた *ステータスコード* がある際にはそれを返します。そして、*ボディ* は *レスポンス* の *ボディ* に紐づけられます。もしも *Content-Typeヘッダー* がアクションの結果の *ヘッダー* 内で宣言されていなければ、それが文字列であれば(あるいはエラーが排出されれば) *ボディ* はそれそのものと紐づけられます。 *Content-Type* が定義づけられていれば、`コントローラ`は *レスポンス* がバイナリデータまたはプレインテキストかを見極め、必要に応じて *Base64デコーダ* を用いた文字列をデコードします。もしも、 *ボディ* が正確にデコードできなければ、エラーが返されます。

*JSON* オブジェクトまたは配列はバイナリデータで *Base64* エンコードでなければいけません。

さあ、`ヘッダー`と`ステータスコード`を正確に作成しリダイレクトを送ってみましょう。下のように、`webAction`というアクションを作成してください。

```javascript
function main() {
    return {
        headers: { location: "http://openwhisk.org" },
        statusCode: 302
  };
}
```

アクションをweb actionとして実行します。

<pre>
$ bx wsk action update webAction --web true
<b>ok:</b> updated action <b>webAction</b>
</pre>

（namespaceを自分のものに書き換えた上で）ブラウザで次のリンクを開いてみてください。
`https://openwhisk.ng.bluemix.net/api/v1/web/andreas.nauerz%40de.ibm.com_dev/default/webAction.http` openwhisk.orgのサイトにりだいれくとされることでしょう。

次に`ヘッダー`・`ステータス`・`ボディ`のプロパティをイメージと共に返されるようにしてみましょう。それでは先に作成したweb actionをアップデートしましょう。

```javascript
function main() {
    let png = "<STRING REPRESENTING A BASE64 ENCODED IMAGE>"
    return { headers: { "Content-Type": "image/png" },
             statusCode: 200,
             body: png };
}
```

オンラインで利用できるBase64エンコーダはどれでも、あなたが選択したイメージをエンコードするために上に示された文字列のようにして利用できます。

再び、ブラウザを通してweb actionを実行してください。指定したイメージを確認できるでしょう。

最後に、`ヘッダー`・`ステータス`・`ボディ`のプロパティから簡単な *HTML* を返してみましょう。先に作成したweb actionを次のようにアップデートしてください。

```javascript
function main() {
    let html = "<html><body>Hello World!</body></html>"
    return { headers: { "Content-Type": "text/html" },
             statusCode: 200,
             body: html };
}
```

もう一度web actionをブラウザで実行してください。`Hello World!`というメッセージを確認できるでしょう。

### アクションの定期実行

以前説明したようにアクションはブロッキング(同期)または非ブロッキング(非同期)型のどちらかのみでは実行できませんが、アクションは *定期的な* 実行が可能です。

これをテストするには、IBM Cloud Functions UIを開き以前作成した`helloUI`を選択してください。
次に、コードエディタの右下部にある「`このアクションを自動化`」ボタンをクリックしてください。  
それから、次の画面で`Periodic`のアイコンを選択してください。
`新規アラーム`アイコンをクリックし、新しいトリガー(アラーム)を作成しましょう。
`:MM minutes`アイコンを選択肢、`N`を`1`にしてアクションが毎分起動するようにしましょう。
この定期トリガーに任意の名称をつけ、`定期的なトリガーの作成`ボタンをクリックしましょう。
最後に`次へ`をクリックし、`これは適切なようです`を選択した後、`ルールの保存`を押しましょう。

結果を見るには、`アクティビティの表示`を押してダッシュボードを確認しましょう。毎分アクションが実行されていることがわかります。これを止めるには、作成したルールを無効化する必要があります。どこで実行すれば良いかわかりますか？

## ログ
もちろんIBM Cloud Functionsではアクションにカスタムログのステートメントを加えることもできます。

ログがどのように稼働しているかを確認するには、`アクションの作成`ボタンをクリックしてください。
そして、任意の名前をつけ(例：`helloLogging`)、`アクションの作成`ボタンをクリックしてください。

次に、下のコードをコピーし、コードエディタ上の既存のコードに上書きしてください。

```javascript
function main(params) {
    console.log("Running helloLogging... ");
    return { message: "Hello world!" };
}
```

`このアクションを実行`ボタンをクリックし、今までの手順と同様にし、ブラウザ上でアクションをテストしてください。

すると、下の結果を得ることができるでしょう。

<pre>
{
    "message": "Hello world"
}
</pre>

ログを確認するには、アクションを実行した後に、`ログの表示`リンクをクリックします。

下のようなログが確認できるでしょう。

<pre>
2016-10-18T08:36:34.472273207Z stdout: Running helloLogging...
</pre>

あなたのオリジナルのアクションでも自由に試した時に、異なるプログラミング言語で実行することがあるかもしれません。その場合には、以下のリンクを参照して公式の文書を参照してください。

https://github.com/openwhisk/openwhisk/blob/master/docs/actions.md#creating-python-actions
https://github.com/openwhisk/openwhisk/blob/master/docs/actions.md#creating-swift-actions
https://github.com/openwhisk/openwhisk/blob/master/docs/actions.md#creating-java-actions
https://github.com/openwhisk/openwhisk/blob/master/docs/actions.md#creating-docker-actions

## パッケージの活用

これまでに確認したように、IBM Cloud Functionsでは、パッケージとしていくつかのアクションやトリガーを提供しています。さらにIBM Cloud Functions UIによってパッケージの探索やテストが簡単になっています。これらをどのように用いればいいか学んでいきましょう。

まず、画面の右上部にある`パブリックパッケージの参照`ボタンをクリックしましょう。
パッケージが利用可能ないくつかのパッケージがアイコンとともに表示されます。

`Samples`パッケージをクリックしましょう。
画面の左部に短いこのパッケージの機能の簡単な説明が表示されます。上部中央からはパッケージが提供する異なるアクションやトリガーへとアクセスできます。(Samplesパッケージでは表示されたアクションのみが提供されています。)
`curl`・`greeting`・`helloWorld`・`wordCount`からアクションを選択できます。簡単な実行内容の説明とサンプル入力とそれによって実行した時にどのような出力が得られるか各アクションごとに表示されます。

`wordCount`アクションを試してみましょう。
`wordCount`アクションを選択し、説明書きを読んでその機能を理解してください。また、サンプル入力を確認し、どのようにアクションを作成すればいいか、またその実行後どのような出力結果を得られるかを確認しましょう。
`このアクションを実行`ボタンをクリックしましょう。

実行前に確認したサンプル入力をベースにして、JSON入力欄に下のコードを貼り付け、`この値で実行`ボタンをクリックしましょう。

```json
{
    "payload": "OpenWhisk is simply super cool"
}
```

すると以下の結果が得られるでしょう。

<pre>
{
    "count": "5"
}
</pre>

パッケージとして提供されたアクションをそのまま転用するのではなく、それに含まれるコードを確認することができますね。(そうすることで、自ら作成したアクションにコードを活用できます。)

`curl`アクションのコードを確認してみましょう。
カタログに戻り(呼び出しコンソールを閉じるのに'閉じる'を押します)、もう一度`Samples`パッケージをクリックします。
今回は`curl`アクションを選択し、説明書きを読みます。
次に、`ソースの表示`ボタンをクリックし、アクションのコードを確認し理解します。

他のパッケージも同様に試してみてください。

### アクションのシーケンス化

次に、先にCLIを用いた際と同様に簡単なシーケンスを視覚的にモデリングしてみましょう。

そこでまずは、簡単なアクション(`echo`という名前にしてください)を今までと同様の方法で作成してください。

```javascript
function main(params) {
    return { payload: "Life is " + params.payload };
}
```

見ての通り、このアクションは`payload`と呼ばれるパラメータを通して持ち込まれたテキストを返すだけです。

さて、もしかして`echo`に与えたテキストを全て英語からフランス語に翻訳するようなシーケンスを作ってみたくなったんじゃないですか？

これを作成するために`Watson`パッケージに入った`translate`アクションを実行してみましょう。

さて、まずは`Watson Language Translator`サービスのインスタンスを作成しましょう。
まずは、画面の右上部にある`カタログ`リンク(パブリック・パッケージの参照ではありません)をクリックしましょう。
画面の左部のメニューから`Watson`を選択します。
次に、`Language Translator`をクリックします。
全ての設定をそのままにし、画面右下部の`作成`をクリックします。
次に、`サービス資格情報`タブに移り、`資格情報の表示`リンクをクリックします。
`username`と`password`をメモします。

それでは、このパッケージとアクションがどのように作用するのかみてみましょう。
IBM Cloud Functions UIに戻り、カタログにアクセスし(`パブリック・パッケージの参照`)、`Watson Translator`パッケージをクリックします。
`translator`アクションをクリックし、説明書きとサンプル入力/出力を読み内容を理解します。

次に、Watsonを使えるようにするためにバインドします。
画面の左にある`New Binding`ボタンをクリックします。
任意の名称を入力し、先ほど作成した`Language Translator`インスタンスを選択します(あるいは任意の名称を入力した後、先ほど作成した`username`と`password`を入力してください)。そして、`構成の保存`をクリックしてください。

次に、(まだ設定されていなければ)バインドしたものの選択、`translator`アクションが選択されたままになっているかの確認をし、`このアクションを実行`をクリックしてください。

下のインプットを入力し、`この値で実行`ボタンをクリックします。(その前に`ライブにする`ボタンのクリックを求められるかもしれません。)

```json
{
    "translateTo": "fr",
    "payload": "Wonderful",
    "username": "xxx",
    "translateFrom": "en",
    "password": "xxx"
}
```

`username`と`password`の値はバインドを作成した際に振られたものに書き換える必要があります。
代わりに、デフォルトで入力されている`username`と`password`は削除して構いません。

すると、下の結果が得られるでしょう。

```json
{
    "payload": " Merveilleux"
}
```

さて、それではシーケンスとして2つのアクションをくっつけてみましょう。
先に作成した`echo`アクションを選択します。
画面の右下部にある`シーケンスにリンク`ボタンをクリックします。
それから、次の画面に表示される`Watson Translator`パッケージをクリックし、`translator`アクションと先に作成したバインドを選択します。
そして、`シーケンスに追加`ボタンをクリックし、`これは適切なようです`ボタンを選択します。
最後に、シーケンスの名前を入力し(任意)、`アクションシーケンスの保存`をクリックして、`完了`ボタンを選択します。
シーケンスをテストするには`このシーケンスを実行`ボタンをクリックします。

下記のインプットを入力し、`この値で実行`ボタンをクリックします。

```json
{
    "translateTo": "fr",
    "payload": "wonderful",
    "translateFrom": "en"
}
```

するとしたの結果が得られるでしょう。

```json
{
    "payload": "La vie est belle"
}
```

## トリガー

IBM Cloud Functions UIを用いてトリガーを実行できます。

特定の *Github* リポジトリに更新があった際に、先に作成した`hello`アクションを実行したいと思ったことはありませんか？

まず、`hello` アクションを選択します。
次に、画面右下部の`このアクションを自動化`ボタンをクリックします。
それから、`Github`アイコンをクリックします。
そして、`新規トリガー`アイコンをクリックします。

ここから先に進めるには *Github* のアカウントが必要です。もし持っていないようでしたら、今sign-upしましょう。

*Github* の`username`と`access token`、それからチェックしたいをリポジトリの`name`を入力します。

*Github* にて、`username`はログイン後の`Signed in as ...`の下に確認できます。access tokenは`Settings内のDeveloper Settings`にあります。`Generate new token`ボタンをクリックし、任意の`name`を入力し、`repo`チェックボックスをクリックします。同様に、テスト用のリポジトリも作成すると良いでしょう。

Githubの`username`と`access token`を入力すれば、リポジトリをプルダウンメニューから選択することもできます。

eventsには`*`を入力し全てのイベントをチェックできるようにしましょう。

全ての項目を入力したら、`構成の保存`ボタンをクリックしましょう。
（もし選択されていなければ)先ほど作成したトリガーを選択し、`次へ`ボタンをクリックしましょう。
次に、`これは適切なようです`ボタンをクリックし、`ルールの保存`を選択します。

テストのために、まずはマニュアルに従ってトリガーを起動しましょう。

`アクティビティの表示`ボタンをクリックし、モニタリング用のダッシュボードを開くと、何が起こっているのかを確認することができます(このダッシュボードの詳細はこのあと説明があります。)。右上部では、起動されているトリガーと実行されているアクションを確認できます。定期的に自動で更新されます。`更新`アイコンをクリックすれば任意に更新することも可能です。
テスト状態のまま続行するにはあなたのアクション・トリガー・ルールが示されているブラウザタブを選択し、先に作成したトリガーの上にカーソルをかざし、`このトリガーを起動`と書かれた`雷`アイコンをクリックして起動します。
次の画面に現れる`この値で実行`ボタンをクリックします。
それｋら、ブラウザタブをトリガーの起動状態を確認するためにモニタリングダッシュボードに戻し、たった今、`hello`アクションが起動したことを確認します。

最後に新規のブラウザタブを開き、 *Github* にログインしてください。

あなたのリポジトリに行き、ファイルを追加するかファイルの内容を変更するかして、変更をコミットしてください。
それから、モニタリングダッシュボードのブラウザタブに戻り、`hello`アクションが実行されていることを確認してください。

## ルール

IBM Cloud Functions UIを使えばルールはシーケンスと同様にして作成できます。まずはルールの一部とするアクションを選択してください。
それから、`このアクションを自動化`を`ルールの作成`ボタンとしてこれまでに行ったようにクリックしてください。

トリガーと同様にルールはルールを選択した後に`このトリガーを起動`ボタンをクリックすることで起動します。
代わりに、ルールを選択した後で、`このアクションのみを実行`ボタンをクリックすることでルールの中の一部のみを実行できます。
すでに作成したルールを利用して試してみてください。

## モニタリング

モニタリングダッシュボードを使えばシステムの機動状況を確認できます。

ダッシュボードの左上部アクションやルールごとの呼び出しカウントを確認できます。これによって、特定のアクションやルールがどんな頻度で呼び出されているのか、どれが最も呼び出されているのかを確認できます。棒グラフのうち、起動に成功したものは緑、失敗したものは赤で表示されます。

ダッシュボードの右上部には最近のアクティビティが表示されています。呼び出されたトリガーやアクションは呼び出し時間などのメタデータと共に表示されています。成功したアクティビティは緑、失敗したものは赤で表示されています。`activation id`をクリックすれば、そのアクティベーションの詳細を確認することができます。

ダッシュボードの中央部には特定の時点においてどれほどの呼び出しがあったかのカウントを確認できます。成功した呼び出しは緑、失敗した呼び出しは赤で表示されます。

今までに作成したアクションやトリガーなどを試してみましょう。トリガーの起動、アクションの呼び出しなどをし、モニタリングダッシュボードの様子を確認してみましょう。

# 天気予報エンジンを作る！

さあ、あなたが学んだことをもとに、役立つデモを構築しましょう

このデモでは、ユーザーに天気予報を通知する*Slack*用のボットを作成します。ユーザーはチャットメッセージを送信する事により、ボットに特定の場所の予測を尋ねることが出来ます。例えば毎日午前８時のように、ボットは定期的な感覚で位置の予測を送信するように設定することも出来ます。

ボットはいくつかの機能が必要です。例えばアドレスを場所に変換し、場所の天気予報を取得し、*Slack* と統合します。ボットをモノシリックアプリケーションとして実装するのではなく、これらすべての機能のロジックを含んでいるため、別のサービスとして展開したいと考えています。

後に、シーケンスを使用してバインドする方法を見ていきます。コードを書かずにボットを作成することができます。

Notice ここで説明する成果物のほとんどの物は、CLIもしくはOpenWhisk UIのどちらかで作成できます。　あなた次第です。

## 住所を位置情報へ

このサービスは外部のジオコーディングAPIを使用して住所の「緯度」と「経度」の座標値の取得を行います。

アクション（マイクロサービス）は、以前に触れたように、単一の関数(`main`)内でアプリケーションロジックを実装します。以前と同じように、パラメータはオブジェクトの引数(`params`)として関数呼び出しに渡されます。サービスは*Google*ジオコーディングAPIへのAPI呼び出し行い、最初のアドレス一致の呼び出しの応答から結果を返します。

Notice 関数から`Promise`を返すことは、サービス応答を非同期に返すことが出来ることを意味します。

では、次のコードを使ってアクション(名前は`location_to_latlong`)を作りましょう。これまで述べたように、CLIやOpenWhisk UIを使用して、以前に学んだ方法と同じように作成する事ができます:

```javascript
var request = require("request");

function main(params) {
    var options = {
        url: "https://maps.googleapis.com/maps/api/geocode/json",
        qs: {address: params.text},
        json: true
    };

    return new Promise(function (resolve, reject) {
        request(options, function (err, resp) {
            if (err) {
                console.log(err);
                return reject({err: err});
            }

            if (resp.body.status !== "OK") {
                console.log(resp.body.status);
                return reject({err: resp.body.status});
            }

            resolve(resp.body.results[0].geometry.location);
        });
    });
}
```

次に、以前に学習した方法でアクションを展開しましょう:

<pre>
$ bx wsk action create location_to_latlong location_to_latlong.js
<b>ok:</b> created action <b>location_to_latlong</b>
</pre>

次に、アクションをテストしましょう:

<pre>
$ bx wsk action invoke location_to_latlong -b -r -p text "London"
{
    "lat": 51.5073509,
    "lng": -0.1277583
}
</pre>

## 位置情報からの予測

ここで、位置情報から予測を検索するサービスを実装しましょう。

このサービスでは、外部APIを使用して地域の天気予報を取得し、24時間以内に天気のテキストの説明を返します。

まず、*Weather Company Data service*.のインスタンスを作成する必要があります。
これをするには、画面の右上にある「カタログ」リンクをクリックしてください。
画面の左側に表示されるメニューから「データ＆分析」を選択します。
次に`Weather Company Data`をクリックします。
すべての設定をそのままにして、画面右下にある「作成」ボタンをクリックします。
次に、`サービス資格情報`タブに切り替え`資格情報の表示`リンクをクリックします。
※訳注）`資格情報の表示`が存在しない場合、`新規資格情報`を一度クリックし、作成します。
Note `username` and `password`を書き留めてください。もし米国南部に無いサービスを使用する場合は、`host`を書き留めてください。

次のコードを使用してアクション(名前は`forecast_from_latlong`)を作成しましょう:

```javascript
var request = require("request");

function main(params) {
    if (!params.lat) return Promise.reject("Missing latitude");
    if (!params.lng) return Promise.reject("Missing longitude");
    if (!params.username || !params.password) return Promise.reject("Missing credentials");
    var host = params.host || "twcservice.mybluemix.net";

    var url = "https://"+host+"/api/weather/v1/geocode/"+params.lat+"/"+params.lng+"/forecast/daily/3day.json";

    var options = {
        url: url,
        json: true,
        auth: {
            user: params.username,
            password: params.password
        }
      };

      return new Promise(function (resolve, reject) {
          request(options, function (err, resp) {
          if (err) {
              return reject({err: err});
           }
           resolve({text: resp.body.forecasts[0].narrative});
        });
    });
}
```

次に、アクションを再度デプロイしてみましょう:

<pre>
$ bx wsk action create forecast_from_latlong forecast_from_latlong.js
<b>ok:</b> created action <b>forecast_from_latlong</b>
</pre>

Notice サービスは４つのパラメータ、`緯度`と`経度`が`サービス資格情報`(これまでに書き留めたもの)と一緒になることを期待しています。パラメータとして、`サービス資格情報`を渡すと、コード内に埋め込む必要がなくなり、実行時に動的に変更することが出来ます。

アクションをもう一度試してみましょう:

<pre>
$ bx wsk action invoke forecast_from_latlong -p lat "51.50" -p lng "-0.12" -p username &lt;username&gt; -p password &lt;password&gt; -p host &lt;host&gt; -b -r
{
    "text": "Partly cloudy. Lows overnight in the low 60s."
}
</pre>

リクエストごとに`サービス資格情報`を渡したくないので、デフォルトの別名バインドされたパラメータをアクションにバインドしましょう。つまり、`緯度`と`経度`パラメータでサービスを呼び出すだけです。

アクションを更新し、上記のパラメータをバインドしましょう:

<pre>
$ bx wsk action update forecast_from_latlong -p username &lt;username&gt; -p password &lt;password&gt; -p host &lt;host&gt;
<b>ok:</b> updated action <b>forecast_from_latlong</b>
</pre>

アクションをもう一度試してみましょう:

<pre>
$ bx wsk action invoke forecast_from_latlong -p lat "51.50" -p lng "-0.12" -b -r
{
    "text": "Partly cloudy. Lows overnight in the low 60s."
}
</pre>

## Slackへのメッセージ送信

予測ができたら、ボットのメッセージとして*Slack*に送信する必要があります。*Slack* は、*webhook* を利用して単純なボットを書く簡単な方法を提供します。着信webhookは、通常の*HTTP*リクエストを使用してデータを送信するURLをアプリケーションに提供します。*JSON* リクエスト本文の内容はぼっとメッセージとしてチャンネルに投稿されます。

まず、https://slack.com/にアクセスし、画面の一番上にある「新しいチームを作成」リンクをクリックして、*Slack* 上に新しいチームを作成します。

指示に従ってチームを作成してください:
あなたの`メールアドレス`を入力し、`次へ`ボタンをクリックしてください。
メールで送信した`確認コード`を入力してください。
あなたの`名前`、`名字`、`ユーザ名`を入力して、`パスワード設定へ進む`ボタンをクリックします。
`パスワード`を設定し、`チーム情報設定へ進む`ボタンをクリックしてください。
`関心のあるグループ`のようなオプションを選択して *Slack* を使用する物を指定し、`グループ名設定に進む`ボタンをクリックします。
任意の`グループ名`を入力し、`チームURL指定へ進む`ボタンをクリックします。
任意の`チームURL`を入力し、`チームの作成`ボタンをクリックします。
`スキップ`ボタンをクリックして招待状を送信するプロセスをスキップし、`Slackを探索`ボタンをクリックして開始してください。
最後に、最下部のテキストフィールドに何かを入力して開始します。

コミュニケーションチャンネルを作成する方法は次のとおりです:
画面左側の`チャンネル`という文字の隣にある小さな`+`アイコンをクリックします
そして、あなたのチャンネルに`weather`という名前をつけて、`チャンネルを作成する`ボタンをクリックするだけです。

*Slack* が設定できました。

これらの *HTTP* リクエストの送信を行う別のアクション(マイクロサービス)を書くことが出来ましたが、既にご存知のように、OpenWhiskには、多くのサードパーティ製システムのインテグレーション(パッケージ提供)が付属しています。

利用可能なパッケージをもう一度見直してみましょう:

<pre>
$ bx wsk package list /whisk.system
<b>packages</b>
/whisk.system/cloudant                 shared
/whisk.system/alarms                   shared
/whisk.system/watson                   shared
/whisk.system/websocket                shared
/whisk.system/weather                  shared
/whisk.system/system                   shared
/whisk.system/utils                    shared
/whisk.system/slack                    shared
/whisk.system/samples                  shared
/whisk.system/github                   shared
/whisk.system/pushnotifications        shared
</pre>

ここでは`Slack`パッケージに注目します。この中にあるものを見てみましょう:

<pre>
$ bx wsk package get --summary /whisk.system/slack
<b>package</b> /whisk.system/slack: This package interacts with the Slack messaging service
   (<b>parameters</b>: username url channel token)
 <b>action</b> /whisk.system/slack/post: Post a message to Slack
</pre>

コードを記述することなく*Slack*にメッセージを投稿するアクションを呼び出す事ができます。

Notice 最初に着信webhookの`URL`をあなたのものに置き換える必要があります。あなたの着信webhookを知るには、次の手順で進めてください:

画面左上のあなたのチーム名をクリックします。
表示されるメニューから`App管理`を選択します。
画面上の`Appディレクトリを検索`に`incoming`を入力し、`着信Web フック`というエントリを選択します。
次に`設定を追加`をクリックします。
次に先ほど作成した`weather`チャンネルを選択し、`着信Web フック インテグレーションの追加`ボタンをクリックします。
次に`Webhook URL`項目に表示された`URL`をコピーします。

<pre>
$ bx wsk action invoke /whisk.system/slack/post -p url https://hooks.slack.com/services/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 -p channel weather -p text "Hello"
<b>ok:</b> invoked <b>/whisk.system/slack/post</b> with id <b>78070fe2acb54c70ae49c0fa047aee51</b>
</pre>

あなたの*Slack*チャンネルでメッセージがポップアップしているのが見えるということは、これがうまく行ったことを証明します。

繰り返しますが、アクションのデフォルトパラメータをバインドしたいのですが、グローバルパッケージをローカルネームスペースに最初にコピーしない限り、これはサポートされていません。

では、やってみましょう:

<pre>
$ bx wsk action create --copy webhook /whisk.system/slack/post -p url https://hooks.slack.com/services/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 -p channel weather -p username "Weather Bot" -p icon_emoji ":sun_with_face:"
<b>ok:</b> created action <b>webhook</b>
</pre>

カスタマイズされた*Slack*サービスは`text`パラメータだけで呼び出すことができ、`weather`チャンネルにフレンドリーなメッセージを送れます:

<pre>
$ bx wsk action invoke webhook -p text "Hello again"
<b>ok:</b> invoked <b>webhook</b> with id <b>a4044f7192544d69bc179a991a970559</b>
</pre>

## シーケンスを利用してお天気ボットを作成する

ボットのロジックを処理する3つのアクション(マイクロサービス)があります。ここでは、これらの3つの要素を以前に学習した方法でつなげるシーケンスを作成しましょう:

それではボットがこれらのサービスに参加するための新しいシーケンスを定義しましょう。

<pre>
$ bx wsk action create location_forecast --sequence location_to_latlong,forecast_from_latlong,webhook
<b>ok:</b> created action <b>location_forecast</b>
</pre>

このメタサービスを定義すると、最初のサービス（`text`）の入力パラメータで` location_forecast`アクションを呼び出すことができます。 その結果、その場所の予報が*Slack*に表示されます。

それでは試してみましょう。
結果は次のようになります:

<pre>
$ bx wsk action invoke location_forecast -p text "London" -b
<b>ok:</b> invoked <b>location_forecast</b> with id <b>d63b40bb36c54cfbaf8262b6f7e5c2e9</b>
{
    "activationId": "d63b40bb36c54cfbaf8262b6f7e5c2e9",
    "annotations": [],
    "end": 1473179750086,
    "logs": [],
    "name": "location_forecast",
    "namespace": "andreas.nauerz@de.ibm.com",
    "publish": false,
    "response": {
        "result": {},
        "status": "success",
        "success": true
    },
    "start": 1473179746914,
    "subject": "andreas.nauerz@de.ibm.com",
    "version": "0.0.1"
}
</pre>

アクションをWebアクションとして呼び出すには、次のように入力します:

<pre>
$ bx wsk action update location_forecast --web true
<b>ok:</b> updated action <b>location_forecast</b>
</pre>

## ボットの予報
ここでの問題は、ボットが予報に必要な場所をどのようにして知ることができるかです。
At this point the question is how we can ask the bot for forecasts about a location?

*Slack* は、チャンネルメッセージにキーワードが現れたときに*JSON*メッセージを外部のURLにポストする発信webhookを提供します。あなたのチャンネルに新しい発信Webhookを設定すると、ユーザーは`wetaher: london`という事でボットに応答させることができます。d.

したがって、定義されたトリガーワードで始まるメッセージが以前に作成した`weather`チャンネル経由で送信されると、アクションが適切に呼び出されていることを確認する必要があります。

これを実現するには、次のように進めます:
チャンネルに入ったら、一番上にある歯車アイコンをクリックし、表示されたメニューから `アプリを追加する`リンクを選択してください。
画面上の検索フィールドに`outgoing`という単語を入力し、`発信 Webフック`を選択します。
次に`設定を追加`と`発信 Webフック インタグレーションの追加`ボタンをクリックします。
インテグレーションの設定の`チャンネル`に以前に作成したチャンネルを選択します。
`引き金となる言葉`に`weather`を指定します。
`URL`には`location_forecast`アクションの`web action URL`を以下のように指定します:
`https://openwhisk.ng.bluemix.net/api/v1/web/andreas.nauerz@de.ibm.com_dev/default/location_forecast.json`  
次に、`設定を保存する`ボタンをクリックします。

次に、チャンネルを表示しているブラウザタブに戻り、チャンネルのメッセージ欄に以下を入力します:
`weather: london`

## トリガーに接続する

これまで学んだように、トリガーは外部からOpenWhiskへのイベントストリームを表すために使用されます。*REST* APIを使用して手動で呼び出すことも、トリガー フィードに接続してから自動的に呼び出すこともできます。アクションはルールを使用してトリガーにバインド出来ます。複数のアクションが同じトリガーを拾うすることが出来ます。

ボットサービスをサンプルトリガーにバインドし、そのトリガーを起動して間接的に呼び出す方法を見てみましょう:

<pre>
$ bx wsk trigger create forecast
<b>ok:</b> created trigger <b>forecast</b>

$ bx wsk rule create forecast_rule forecast location_forecast
<b>ok:</b> created rule <b>forecast_rule</b>

$ bx wsk trigger fire forecast -p text "London"
<b>ok:</b> triggered <b>forecast</b> with id <b>49914a20416d416d8c90282d59eebee3</b>
</pre>

トリガーを起動し、`text`パラメーターを渡すと、ボットは自動的に呼び出され、`London`の予報をチャンネルに投稿しました。

では、毎朝ボットを起動して仕事を開始する前に予報をしましょう。

## 朝の予報

新しい外部イベントが発生するたびに自動的に起動するようにトリガーを設定しましょう。これにより、ルールを介してこのトリガーにバインドされたすべてのアクションが呼び出されます。

これまでのように、トリガは、外部トリガフィードへの参照を渡すことによって、作成中に外部イベントソースにバインドされます。OpenWhiskのパブリックパッケージには、外部イベントソースに使用できる多数のトリガフィードが含まれています。

これらのパブリックトリガフィードの1つは、既に以前使用した`alarm`パッケージに含まれています。このように、このアラームフィードは予め指定された感覚でトリガを実行します。ウェザーボットのトリガーでこのフィードを使用することで、毎朝特定の住所について実行しロンドンの予報を行うことができます。

ではやってみましょう:

<pre>
$ bx wsk package get /whisk.system/alarms --summary
<b>package</b> /whisk.system/alarms: Alarms and periodic utility
   (<b>parameters</b>: cron trigger_payload)
 </b>feed</b>   /whisk.system/alarms/alarm: Fire trigger when alarm occurs

$ bx wsk trigger create regular_forecast --feed /whisk.system/alarms/alarm -p cron "*/10 * * * * *" -p trigger_payload "{\"text\":\"London\"}"
<b>ok:</b> created trigger <b>feed regular_forecast</b>

$ bx wsk rule create regular_forecast_rule regular_forecast location_forecast
<b>ok:</b> created rule <b>regular_forecast_rule</b>
</pre>

トリガースケジュールは`cron`パラメータによって提供されます。これはテストするために10秒ごとに実行するように設定されています。この新しいトリガーをボットサービスに結びつけることで、ロンドンの予報がチャンネルに表示されはじめます。

さて、うまくいったので怒られる前にアラームを止めておきましょう:

<pre>
$ bx wsk rule disable regular_forecast_rule
<b>ok:</b> rule <b>regular_forecast_rule</b> is <b>inactive</b>
</pre>

# サーバーレスなマイクロサービスバックエンドを構築する

アクションがいかに柔軟性を持ち独立的にデプロイ可能なマイクロサービスであるかを実感していることでしょう。アクションは機能を *API* (Application Programming Interface)機能を出力するとして完全にサーバーレスなマイクロサービスバックエンドの構築に最適です。

ここでの文章ではAPIは、目を離せないような顧客体験を産み、新しい市場機会に参入するための、サービスやアプリケーションやセンサーやモバイルデバイスを結び合せるデジタルな接着剤なのです。APIにより、市場に新しいデジタルサービスをもたらし、利益のチャネルを開き、顧客の期待を高めることができます。

IBM Cloud FunctionsのAPIゲートウェイインテグレーションは、アクションを *RESTful* エンドポイントとして簡単に出力するためのIBM Cloud Funtionsの新しい特色である。アクションを任意のエンドポイントに振り分け、`GET`・`PUT`・`POST`・`DELETE`といった動作を他のアクションに振り分けた同じエンドポイントから実行することもできる。

APIゲートウェイを用いてアクションを出力するには2つの異なる方法が存在する。
* APIのエンドポイント/動作の組み合わせを任意のアクションに独立して振り分ける。
* アクションにAPIエンドポイントを振り分けるのに *Swagger* 設定ファイルを用いる。

CLIまたはUIを用いてAPIを定義することができます。この後の説明では両方の方法を説明します。

IBM Cloud FunctionsのAPIゲートウェイインテグレーションを用いたアクションの出力は現時点ではweb actionsのように扱われている。そのため、先に確認したように`ヘッダー`・`ステータス`・`ボディ`といったプロパティを利用することができる。

## はじめてのAPI

*REST* APIとしてフィボナッチ数列を作成するアクションを出力する方法を探索してみましょう。

というわけで、まずはアクションそのものについて見ていきましょう。
フィボナッチ数列に従って、前の2つの数字を足し合わせたものが次の数になるという数字の生成は比較的単純なものです。
コマンドラインからアクションを呼び出して、(数列のn番目の値のための)`num`パラメータを設定すると、フィボナッチ数列の帰納的な呼び出しにメソッドに従ってn項目の値と初項からn項目までの数列とフィボナッチメソッドを回帰的に呼び出した回数を返します。

```javascript
var sequence = [1];
var invocations = 0;

function main(params) {
    invocations = 0;
    var int = parseInt(params.num);

    //num is a zero-based index
    return {
        body: "n: " + int + ", value: " + fibonacci(int) + ", sequence: " + sequence.slice(0,int+1) + ", invocations: " + invocations
    };
}

function fibonacci(num) {
    invocations ++;
    var result = 0;

    if (sequence[num] != undefined) {
        return sequence[num];
    }

    if (num <= 1 || isNaN(num)) {
        result = 1;
    } else {
        result = fibonacci(num-1) + fibonacci(num-2);
    }

    if (num >= 0) {
        sequence[num] = result;
    }

    return result;
}
```

次に、アクションをデプロイし呼び出しましょう。

<pre>
$ bx wsk action create fibonacci fibonacci.js
<b>ok:</b> created action <b>fibonacci</b>

$ bx wsk action invoke fibonacci -p num 5 -b -r
<b>ok:</b>  invoked action <b>fibonacci</b> with id <b>dde9212e686f413bb90f22e79e12df75</b>
{
  "body": "n: 5, value: 8, sequence: 1,1,2,3,5,8, invocations: 9"
}
</pre>

### エンドポイントにアクションをマッピングする

それではどのようにアクションがAPIのエンドポイント/動作に関連づいているかを学んでいきましょう。IBM Cloud Functions CLIを用いる際には、`APIパス`・`動作`(`GET`・`POST`・`PUT`・`DELETE`)そして`アクション`を設定しなければなりません。

下記のコマンドをnamespaceを適当なものに直した上で実行してください。

<pre>
$ bx login -a api.ng.bluemix.net -o &lt;organization&gt; -s &lt;namespace&gt;
</pre>

上のプロパティの意味がわからないようであれば、次のリンクから、コマンドをフルコピーしてください。 https://console.bluemix.net/openwhisk/learn/cli

さて、アクションをweb actionとして実行しましょう。

<pre>
$ bx wsk action update fibonacci --web true
<b>ok:</b> updated action <b>fibonacci</b>
</pre>

次に、APIパス`/fibonacci`を用いて、`fibonacci`アクションを`GET`しましょう。

<pre>
$ bx wsk api create /fibonacci get fibonacci
<b>ok:</b> created API /fibonacci GET for action <b>/_/fibonacci</b>
https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/8326f1d8a3dbc5afd14413a2682b7a78e17a55ee352f6c03f6be82718d69726e/fibonacci
</pre>

さて、実行してみましょう。

<pre>
$ curl --request GET https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/8326f1d8a3dbc5afd14413a2682b7a78e17a55ee352f6c03f6be82718d69726e/fibonacci?num=10
n: 10, value: 89, sequence: 1,1,2,3,5,8,13,21,34,55,89, invocations: 19
</pre>

クエリ文字列を通して引き渡されたパラメータは、アクションの`main`関数へと引き渡された`params`オブジェクトで利用できます。

## サーバレス式図書管理アプリケーション

それではもう少し難易度をあげたものに挑戦しましょう。あなたが読むなどした図書を管理するアクションのセットを出力するなんていかがでしょう？このアプリには、図書を新規登録し、読み、更新し、削除するためのサーバーレスマイクロサービスバックエンドを構成するアクションの実装が必要です。

ここからは、いささか複雑になりますので *Insomnia* のような *REST* クライアント (https://insomnia.rest/)を使いこれから定義するAPIエンドポイントを呼び出すことを強く推奨します。
しかし、もしあなたが、`curl` など他のクライアントを使うことにしたのならば、必ず`application/json`ヘッダーを除外してください。

### Cloudantインスタンスの作成

さて、図書を貯蓄するのには、IBM Cloud Functionsによって提供済の *Cloudant* パッケージを使いコードを書く手間を省きましょう。

IBM Cloud Functionsを開き、画面の右上部にある`カタログ` を開きましょう(`パブリックパッケージの参照`ではありません)
左部のメニューから`データ＆分析`を選択します。
`Cloudant NoSQL DB`をクリックします。
サービス名は`bookStore`とします。他はそのままにして、`作成`ボタンをクリックします。

インスタンスが作成されたら、`サービス資格情報`のタブへと移動し、`新規資格情報`リンクそクリックして新しい資格情報を作成した後、`資格情報の表示`リンクをクリックします。この後ここに書かれた`username`・'password'・'host'の情報を利用しますので、このブラウザタブはこのまま開いたまま置いておきましょう。

### データベースを作成する

*Cloudant* インスタンスを作成しましたね。それでは図書を納めるためのデータベースを作成していきましょう。

IBM Cloud Functionsでは自動的に(IBM Cloud上の) *Cloudantサービス* インスタンスをバインドしたパッケージを作成します。

<pre>
$ bx wsk package refresh
_ refreshed successfully
created bindings:
Bluemix_bookStore_Credentials-1
[...]
</pre>

更新後自動的にあなたが作成した *Cloudantサービス* インスタンスのパッケージバインディングが作成されます。
これを検証するにはー

<pre>
$ bx wsk package list
<b>packages</b>
/andreas.nauerz@de.ibm.com_dev/Bluemix_bookStore_Credentials-1        private
[...]
</pre>

`/whisk.system/cloudant`パッケージに入っているエンティティのリストを表示するには下記のコマンドを使います。

<pre>
$ bx wsk package get --summary Bluemix_bookStore_Credentials-1
<b>package</b> /whisk.system/cloudant: Cloudant database service
   (<b>parameters</b>: BluemixServiceName host username password dbname includeDoc overwrite)
<b>action</b> /whisk.system/cloudant/read: Read document from database
<b>action</b> /whisk.system/cloudant/write: Write document to database
<b>feed</b>   /whisk.system/cloudant/changes: Database change feed
[...]
</pre>

パッケージのアクションに毎回同じパラメータを引き渡す手間を避けるために、パラメータをバインドしてしまいましょう。

<pre>
$ bx wsk package bind /whisk.system/cloudant myBookStore -p username &lt;username&gt; -p password &lt;password&gt; -p host &lt;host&gt;
<b>ok:</b> created binding <b>myBookStore</b>
</pre>

すでに使えるアクションに`create-database`というものがあります。
これを使ってデータベースを作りましょう。

<pre>
$ bx wsk action invoke myBookStore/create-database -p dbname books
<b>ok:</b> invoked <b>/_/myBookStore/create-database</b> with id <b>3f67a23daa8b44efa35725fc22585f9</b>
</pre>

これで、上のパッケージの`write`アクションを使って図書を簡単に貯蔵できます。代わりに、APIエンドポイントをここやパッケージの中の他の有用なアクションに配置することもできます。

それをする前に、バインドをアップデートして、`dbname`を引き渡ししなくていいようにしておきましょう。

<pre>
$ bx wsk package update myBookStore -p username &lt;username&gt; -p password &lt;password&gt; -p host &lt;host&gt; -p dbname books
<b>ok:</b> updated package <b>myBookStore</b>
</pre>

アクションのマッピングの前に、`query index`を`name`フィールドに作成して、あとで書名で図書を検索できるようにしておきましょう。

<pre>
$ bx wsk action invoke myBookStore/create-query-index -p index "{\"index\": {},\"type\":\"text\"}" --blocking
<b>ok:</b> invoked <b>/_/myBookStore/create-query-index</b> with id <b>4g67a23daa8b44efa35725fc22585f0</b>
</pre>

現時点ではパッケージをweb actionとして使えるようにアクションをパッケージにバインドしないのですが、それと同時にAPIゲートウェイを通してアクションをweb actionとして出力する必要があるので、ここでちょっとした工夫が必要です。web actionとして使えるアクションであり、シーケンスを使ってそれまでに定義されたパラメータを全て抱えたアクションをバインドしたパッケージを呼び出すことができる、簡単なプロキシアクションを実装します。これは単なる工夫ではないのです。実際のアクションの前後にこのようなプロキシアクションを実行するということはしばしば必要となることなのです。実際のアクションを実行する前に実行したほうが良いアクションに関しては、認証など、注意して置いたほうが良いものがあることがあります。一方、実際のアクションの後に実行されるアクションに関しては、データの移行が必要になることがあります。

それでは、以下のようにして`proxy`というアクションを作成してみましょう。

```javascript
function main(params) {
    return params;
}
```

次に3つのシークエンスを作成し、web actionとして機能するようにしましょう。

<pre>
$ bx wsk action create endpoint_get --sequence proxy,myBookStore/exec-query-find --web true
<b>ok:</b> created action <b>endpoint_get</b>

$ bx wsk action create endpoint_post --sequence proxy,myBookStore/write --web true
<b>ok:</b> created action <b>endpoint_post</b>

$ bx wsk action create endpoint_delete --sequence proxy,myBookStore/delete-document --web true
<b>ok:</b> created action <b>endpoint_delete</b>
</pre>

次に、APIエンドポイントをアクションに配置しましょう。

<pre>
$ bx wsk api create /books GET endpoint_get
<b>ok:</b> created API /books GET for action <b>/_/endpoint_get</b>
https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/8326f1d8a3dbc5afd14413a2682b7a78e17a55ee352f6c03f6be82718d69726e/books

$ bx wsk api create /books POST endpoint_post
<b>ok:</b> created API /books POST for action <b>/_/endpoint_post</b>
https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/8326f1d8a3dbc5afd14413a2682b7a78e17a55ee352f6c03f6be82718d69726e/books

$ bx wsk api create /books DELETE endpoint_delete
<b>ok:</b> created API /books DELETE for action <b>/_/endpoint_delete</b>
https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/8326f1d8a3dbc5afd14413a2682b7a78e17a55ee352f6c03f6be82718d69726e/books
</pre>

それでは図書を貯蔵しましょう。
*REST* クライアントを用いて先に作ったエンドポイントに`POST`しましょう。

下記の *JSON* データを必ず引き渡しましょう。

```json
{
    "doc": {
        "name":"firstBook"
    }
}
```

出力結果:

```json
{
    "ok": true,
    "id": "1d6e1a830c5a9c4bc62db7f14b1e91e0",
    "rev": "1-5cb5fef5b2fc44f78cb181f6ace8f8db"
}
```

そして:

```json
{
    "doc": {
        "name":"secondBook"
    }
}
```

出力結果:

```json
{
    "ok": true,
    "id": "2e6e1a830c5a9c4bc62db7f14b1e91e0",
    "rev": "2-6cb5fef5b2fc44f78cb181f6ace8f8db"
}
```

次に全ての本を検索しましょう。
*REST* クライアントを使って、先に作成したエンドポイントに`GET`しましょう。

*selector* を定義するために以下のクエリパラメータを引き渡します。

```json
{
    "selector":{
        "name":{
            "$regex":".*"
        }
    },
    "sort":[
        {
            "name":"asc"
        }
    ]
}
```

出力結果:

```json
{
    "docs": [
        {        
	    "_id": "d67e49d6a85d20e9e2ec45710d12d816",
	    "_rev": "1-f4e3fbffab0b7dfcf8677c68689bf9c3",
	    "name": "firstBook"
	},
	{
	    "_id": "26a38a8193722046b2cac60e66dbb0f5",
	    "_rev": "1-3db09f4b6275c63cafca157112bb01d0",
	    "name": "secondBook"
	}
],
[...]
```

次に、特定の本のみを検索します。
もう一度 *REST* クライアントを使って`GET`してください。

セレクタを定義するために以下のクエリパラメータを引き渡します。

```json
{
    "selector":{
        "name":{
            "$eq":"firstBook"
        }
    },
    "sort":[
        {
            "name":"asc"
        }
    ]
}
```


出力結果:

```json
{
    "docs": [
        {
	    "_id": "d67e49d6a85d20e9e2ec45710d12d816",
	    "_rev": "1-f4e3fbffab0b7dfcf8677c68689bf9c3",
	    "name": "firstBook"
	}
    ],
[...]
```

それでは探し当てた図書を削除しましょう。
*REST* クライアントを使って`DELETE`しましょう。
クエリパラメータとして探した図書の`docid`と`docrev`を引き渡します。

図書が適切に削除されたか、全ての本を検索して検証しましょう。


## 気象サービスの出力

先に実装した気象サービス(関数)もAPIを通してアクセスできるようにしましょう。今回はAPIの定義に(CLIではなく)UIを使っていきます。

IBM Cloud Functions UIを開きます。
`API`タブを選択します。
`OpenWhisk APIの作成`ボタンをクリックします。(それまでにAPIを作成したことがない場合のみ表示されます。)
`API名`を`weatherAPI`とします。  
他の設定をそのままにして、画面下部の`保存`をクリックします。

次の画面で画面左部の`定義`タブを選択します。
`操作の作成`クリックします。
`パス`を`location_to_latlong`とします。
`アクション`に`location_to_latlong`アクションを選択します。
他はそのままにして、画面下部の`保存`をクリックします。
もう一度、画面下部の`保存`をクリックします。

この操作を呼び出しするための`URL`を確認するために、`APIエクスプローラー`タブに移ります。
左部にあるリストから、`getloactiontolatlong`エントリーを選択し、`GET URL`をコピーします。
ブラウザウィンドウを開き、クエリパラメータ`?location=London`を加えます。
ロンドンの緯度と軽度が表示されているでしょう。

`定義`タブに戻り、今までの学習を元に、`forecast_from_latlong`アクションを新たな操作を追加することによって出力してください。

APIゲートウェイインテグレーションのその他の特色も色々探っていただいても構いませんよ。

# より複雑なサーバレスアプリケーションを構成する

これまでは、単一のアクション(関数)による、疎結合されたマイクロサービスである、アプリケーションを構築してきました。どちらかというと、単純で具体的なタスクに焦点が当てられたものでした。

そういったマイクロサービスの実装は比較的簡単である一方で、それらの組み合わせや結合はむしろより複雑です。それがKubernetesのようなフレームワークにIstioのようなものを加えて利用するのがとても流行っている理由なのです。IBMの *Composer* ディベロッパを使えば、複数の関数を有し、より複雑でend to endなソリューションのためにコーディネートされたフローを要するアプリケーションを構築することができます。

Composerは独立した関数をより大きなアプリケーションに組み込むためのプログラミングモデル(拡張子)である。 *Compositions* という非公式の名前がつけられた *アプリケーション* は自動管理されたコンピュートとメモリを使ってクラウド上で起動しています。Composerは安定した計算機能、管理フローそして潤沢なパターン数のデータフローを可能とします。

つまり、Conposerは、管理ロジックとステータスを使って複数の関数を組み合わせ、より複雑なサーバーレスアプリケーションの構築を可能とするのです。

Composerには2つのパターンがあります。1つはプログラム的に構成状態を表すライブラリです。そのライブラリは現時点ではNode.jsで利用できます。2つ目は構成を実行するランタイムです。

## はじめよう

Composerを扱うには、新しいfunctions programming shell(fsh)が必要です。

それではまず`fsh`をインストールしましょう。

<pre>
$ npm install -g @ibm-functions/shell
</pre>

インストールが終わったら、このようにして`fsh`を基本的な機能として確認できます。

<pre>
$ fsh
Welcome to the IBM Cloud Functions Shell

Usage information:
[...]
</pre>

## はじめてのComposition

compositionはJSONまたはComposer SDK上のNodeコードを使って定義できます。この後の流れでは、開発者にとってはより自然である、先ほどあげたうち2つ目のアプローチに焦点を当てていきます。

CombinatorsはインラインNode関数も指名された関数(アクション)も許容できます。後者に関しては、関数の正式名称も省略名称も使えます。

理解と汎用性を求めた時に思い当たる最も簡単なCompositionメソッドの1つは`if`です。
`composer.if(condition, consequent, alternate)`は、conditionがtrueの際の`consequent`タスクもそうでない際の`alternate`タスクも稼働できます。`condition`・`consequent`・`alternate`タスクは全てCompositionの入力パラメータオブジェクトに呼び出されます。Conditionタスクの出力パラメータオブジェクトは破棄されます。

それではまずcompositionを定義しましょう(そして`demo_if.js`ファイルにそれを格納しましょう。)。

```javascript
composer.if('condition', /* then */ 'success', /* else */ 'failure')
```

このCompositionは関数の`conditionが`true`ならば関数を`成功`させ、そうでなければ関数は`失敗`にします。

それでは、前述の3つの関数を見ていきましょう。

まずは`condition`関数です。(`condition.js`というファイルに貯蔵されています。)

```javascript
function main(params) {
	if (params.password == "andreas") {
		return { value: true };
	}

    return { value: false };
}
```

基本的に、キー名が`value`でブーリアンであるJSONオブジェクトを返すようになっています。

2つ目は`success`関数です。(`success.js`というファイルの中に貯蔵されています。)

```javascript
function main() {
    return { message: "Success" };
}
```

3つ目は`failure`関数です。(`failure.js`というファイルに貯蔵されています。)

```javascript
function main() {
    return { message: "Failure" };
}
```

次に3つの関数をデプロイします。

<pre>
$ fsh action create condition condition.js
$ fsh action create success success.js
$ fsh action create failure failure.js
</pre>

それから、実際のコンポジションをデプロイします。

<pre>
$ fsh app create demo_if demo_if.js
</pre>

コンポジションを呼び出す前に、`fsh app preview demo_if.js`と入力することにより、その確認ができます。

次にコンポジション呼び出します。まずは、`condition`関数を呼び起こすパスワードを指定せずに`failure`にし、`failure`関数が呼び出されるようにしましょう。

<pre>
$ fsh app invoke demo_if
{
    message: "Failure"
}
</pre>

最後に、コンポジションをもう一度呼び出します。今回は`andreas`というパスワードを指定し、`condition`関数を`true`にし、`success`関数が呼び出されるようにしましょう。

<pre>
$ fsh app invoke demo_if -p password andreas
{
    message: "Success"
}
</pre>

`fsh session get <session id>`を入力すると、呼び出しの結果を確認できます。やってみましょう！

## コンポジションのさらなる探求

もう1つの簡単に理解でき汎用性のあるコンポジションのメソッドは`repeat`です。
`composer.repeat(count, task)`により`count`回`task`が実行されます。

それではまず、コンポジションを定義します。(そして`demo_repeat.js`という名前のファイルに貯蔵します)

```javascript
composer.repeat(5, 'task_repeat')
```

さて、`task_repeat`という関数を定義しましょう。（`task_repeat.js`というファイルに貯蔵します。）

```javascript
function main(params) {
    x = params.count;
    x++;

    return { count: x };
}
```

それぞれの呼び出しの出力結果が次の呼び出しを引き起こしています。

次に、関数とコンポジションをデプロイします。

<pre>
$ fsh action create task_repeat task_repeat.js
$ fsh app create demo_repeat demo_repeat.js
</pre>

そして、コンポジションを呼び出します。

<pre>
$ fsh app invoke demo_repeat -p count 10
{
    count: 15
}
</pre>

さらに最後にもう1つ理解しやすく汎用的なコンポジションメソッド`while`をご紹介します。
`composer.while(condition, task)`は`condition`がtrueである限り繰り返し`task`を実行します。

それではまずコンポジションを定義しましょう。（そしてそれを`demo_while.js`というファイルに貯蔵します）

```javascript
composer.while('condition_while', 'task_while')
```

それから`condition_while`関数を定義しましょう。(`condition_while.js`ファイルに格納します。)

```javascript
function main(params) {
    x = Math.random();

    if (x > 0.2) {
        return { value: true};
    }

    return { value: false };
}
```

次に、`task_while`関数を定義します。(`task_while.js`ファイルに格納します。)

```javascript
function main(params) {
    x = params.count;
    x++;

    return { count: x };
}
```

そして、関数とコンポジションをデプロイします。

<pre>
$ fsh action create condition_while condition_while.js
$ fsh action create task_while task_while.js
$ fsh app create demo_while demo_while.js
</pre>

できたら、コンポジションを呼び出します。

<pre>
$ fsh app invoke demo_while -p count 10
{
    count: 18
}
</pre>

おそらく異なる結果（count）が出力されたでしょう。これは今回の場合は数字がランダムで排出されるからです。

`fsh session get <session id>`で呼び出しの結果が確認できますので、ぜひ試してみてほしいと思います。

現在利用できるコンポジションの総覧は下のリンクからご確認ください。
https://github.com/ibm-functions/composer/tree/master/docs#compositions-by-example

## ネスティングとデータ転送

コンビネータの重要な特徴は、それが入れ子になっていることです。これにより、コンビネータはモジュール性と再利用性を持ちます。

ネスティングと入れ子になったコンポジションの間のデータ転送は別の例で説明することができます。もしあなたが2つのアクションを連携しようとしたとしましょう。1つ目のアクションは`reverse`といい、引き渡した *文字列* を元に戻すことができます。2つめのアクション`output`は元の(戻していない)入力 *文字列* を (戻した) *文字列* と同様にダンプします。

(`task_reverse.js`に格納された)`task_reverse`アクションは下のようにして確認できます。

```javascript
function main(params) {
    return { reverse: params.input.split("").reverse().join("") };
}
```

(`task_output.js`に格納された)`task_output`アクションは下記のようにして確認できます。

```javascript
function main(params) {
    return { message: params.input + " reverted is: " + params.reverse };
}
```

(`demo_nesting.js`に格納された)2つのアクションを連携するコンポジションは下記のようにして確認できます。

```javascript
composer.sequence('task_reverse', 'task_output')
```

`composer.sequence(task_1, task_2, ...)`というコンポジションは(空の)タスクのシーケンスを実行します。コンポジションの入力パラメータオブジェクトはシーケンスの最初のタスクの入力パラメータオブジェクトでもあります。シーケンスのあるタスクの出力パラメータオブジェクトは、シーケンスの次のタスクの入力パラメータオブジェクトでもあります。シーケンスの最後のタスクの酒強くパラメータオブジェクトはコンポジションの出力パラメータオブジェクトとなります。

それでは全てのアーティファクトをデプロイしましょう

<pre>
$ fsh action create task_reverse task_reverse.js
$ fsh action create task_output task_output.js
$ fsh app create demo_nesting demo_nesting.js
</pre>

残念なことにコンポジションを呼び出しても欲しかった結果そのものを手に入れることはできません。

<pre>
fsh invoke demo_nesting -p input myText -r
{
    message: "undefined reverted is: txeTym"
}
</pre>

シーケンス(i.e. ネスティング)自体が機能しているように思えますが、初期入力パラメータの値は喪失しています。
それは`task_reverse`の出力結果が戻された *文字列* であるがためです。初期入力 *文字列* は確かに喪失したのです。
シーケンスに加えて必要なのはデータ転送です。

`retain`コンポジションがこの説明に良いのです。`composer.retain(task[, flag])`は、コンポジションの入力パラメータオブジェクト`params`と`task`の出力パラメータオブジェクトの`result`2つを生み出す、入力パラメータオブジェクトに乗った`task`を実行します。

それではコンポジションをその形に書き換えてみましょう。

```javascript
composer.sequence(composer.retain('task_reverse'), 'task_output')
```

`task_output`もその形に直してみましょう。

```javascript
function main(params) {
    return { message: params.params.input + " reverted is: " + params.result.reverse };
}
```

"1つ目の"`params`は`main`メソッドに引き渡される実数に言及しています。
”2つ目の"`params`は`retain`コンポジションの結果であり、`task_reverse`アクションの呼び出しの`結果`と同様に、最初の `入力`へのアクセスを許します。

それではアーティファクトをアップデートしましょう。

<pre>
$ fsh action update task_output task_output.js
$ fsh app update demo_nesting demo_nesting.js
</pre>

もう一度やってみます。

<pre>
fsh invoke demo_nesting -p input myText -r
{
    message: "myText reverted is: txeTym"
}
</pre>


魔法みたいですね。

`fsh session get <session id>`を入力して呼び出しの結果を視覚化すると良いでしょう。

## インラインコーディング

前にお話ししたように、分かれたファイルの間で関数のコードを定義する必要は常にあるわけではありません。
特に、簡単なロジックは常にインラインで定義されているものです。

コンポジションを定義してみましょう。(そして`demo_inline.js`ファイルに格納しましょう)

```javascript
composer.task(params => ({message: `Hello ${params.name}!`}))
```

そしたらデプロイします。

<pre>
$ fsh app create demo_inline demo_inline.js
</pre>

最後に簡単に呼び出します。

<pre>
fsh invoke demo_inline -p name Andreas -r
{
    message: "Hello Andreas!"
}
</pre>

Composerについてもっと学びたかったら次のURLを参考にしてください。: https://github.com/ibm-functions/composer

# IBM App ConnectとMessage Hub

*IBM App Connect* を使えばビジネスを効果的に進めるための異なるアプリケーションをつなぎ合わせることができます。それにより自動化フローがセットアップされ、どのように1つのアプリケーションのイベントが他のアクションを引き起こすかを示します。また、関連し合うアプリケーションで共有したい情報の配置もできます。

*IBM Message Hub* は *IBM Cloud PaaS* によって管理された *Apache Kafka* であり、リアルタイムのデータパイプラインとストリーミングアプリケーションを構築するスケーラブルではいスループットなサービスです。オープンプロトコルを使ったマイクロサービスをつなぎ合わせたり、強力な洞察を実現する分析とデータをつなぎ合わせたり、リアルタイムで処理をする複数のアプリケーションにデータを引き渡したりします。オンプレミスのメッセージングシステムとクラウドシステムの架け橋となり、ハイブリッドクラウドなメッセージングソリューションを構築します。

この後は *App Connect* を使って、専有の *Message Hub* トピックにデータをポストして、アクションを呼び出すためのIBM Cloud Functionsのトリガーを起動する流れを実践します。

まず、 *Message Hub* インスタンスとトピックを立ち上げましょう。
IBM Cloud Functions UI上の画面右上部の`カタログ`リンクをクリックします。(`パブリック・パッケージの参照`ではありません)
画面左部のメニューにある`アプリケーション・サービス`を選択します。
`Message Hub`をクリックします。
設定はそのままにして右下部の`作成`をクリックします。
`管理`タブに移動し、`+`アイコンをクリックして新しいトピックを作成します。トピック名を`openwhisk`とします。
設定をそのままにして、`トピックの作成`ボタンをクリックします。

次に、 *App Connect* インスタンスを立ち上げます。
新しいブラウザタブを立ち上げます。
IBM Cloud Functions UI上の画面右上部の`カタログ`リンクをクリックします。(`パブリック・パッケージの参照`ではありません)
画面左部のメニューにある`インテグレーション`を選択します。
`App Connect`をクリックします。
設定をそのままにして、画面右下部の`トピックの作成`ボタンをクリックします。

それでは *Salesforce* のテストアカウントにサインアップして、新しいコンタクトが作成されたのと程なくして *App Connect* から *Message Hub* に何かをPOSTさせましょう。(そして、IBM Cloud Functionsのトリガーを起動し、アクションを呼び出しましょう)

新しいブラウザタブを開き、https://www.salesforce.com/form/signup/freetrial-sales.jsp にアクセスしてください。  
右側の欄を埋め、`無料トライアルにサインアップ`ボタンをクリックします。

*App Connect* インスタンスのブラウザタブに戻ります。(もし閉じてしまっていたら、もう一度`カタログ`をクリックし、画面左部の`ハンバーガ`(三本線)アイコンをクリックし、`ダッシュボード`を選択します。）
必要であれば、`Launch App Connect`ボタンをクリックし、次に出てくる案内はskipします。
`New`ボタンをクリックし、`Create an event-driven flow`ボタンを選択します。
`Salesforce`をクリックし、Contact内の`New Contact`を選択します。
`Connect`を選択した後、`Connect to Salesforce`ボタンをクリックします。
ログインしたあと新しいブラウザタブに出てくる`許可`ボタンをクリックします。
*App Connect* に戻り、フローに`Message Hub`の`Send Message`をクリックして加えます。
`Connect`ボタンをクリックします。
*Message Hub* インスタンスを表示しているブラウザタブに戻ります。(もし閉じてしまっていたら、もう一度`カタログ`をクリックし、画面左部の`ハンバーガ`(三本線)アイコンをクリックし、`ダッシュボード`を選択します。）
`サービス資格情報`タブに移動し、`資格情報の表示`リンクをクリックします。
表示されている *JSON* をコピーするためのアイコンをクリックします。
次に、*App Connect* が表示されているブラウザタブに戻り、先ほどコピーした *JSON* を全て`Message Hub Service Credentials`と書かれた欄に貼り付け、`Connect`ボタンをクリックします。
Topicに`openwhisk`を指定します。
payloadとして、(入力欄の隣のお助けアイコンをクリックしたあと)インスタンスの`lastname`を選択します。
最後に、画面右上部の`Exit and switch onボタン`をクリックします。

それでは先ほど作成した *Message Hub* トピックにPOSTがあったら必ずトリガーが起動するようにしましょう。

IBM Cloud Functions UIの開発タブに移りましょう。
新しいアクション(`newContact`という名前にしてください)を作成し、下のコードを貼り付けてください。


```javascript
function main(params) {
    return { "message": "New Salesforce contact data: " + params.message };
}
```

右下部にある`このアクションを自動化`ボタンをクリックし、トリガーにより起動するようにしてください。
`Messaging`をクリックします。
`新規トリガー`をクリックします。
*Message Hub* インスタンスのサービス資格情報を見て当てはまる情報を入力してください。
`構成の保存`ボタンをクリックします。
`これは適切なようです`と`ルールの保存`をクリックします。
最後に、UIの`モニター`タブに移り起こっていることを確認します。

*Salesforce* のブラウザタブに戻ります。
メインメニューの`商談`をクリックします。
画面右上部の`新規`ボタンをクリックします。
少なくとも`商談名`と`取引先名`をクリックして`保存`をクリックします。

IBM Cloud Functions UIモニターに戻ったら、先ほど作成したアクションが、先ほど作成した *Salesforce* 上の商談の情報を以って呼び出されたことがわかるでしょう。

要約すれば、App Connectフローによって、新規の *Salesforce* 上の商談が作成されたら、専有の *Message Hub* のトピックへPOSTするようになったということです。それにより、IBM Cloud functionsのトリガーが起動しアクションが呼び出されたということなのです。

# Special fuel for your engine!

OpenWhisk also integrates with other (3rd party) tools to provide developers with a great developer experience. In the following we have picked two simple samples to demonstrate such kind of integration.

## Developing with VS Code

Many, especially *JavaScript/NodeJS*, developers use *VS Code* to develop their code.
We have recently developed a prototypical extension (not yet officially supported) for *VS Code* that enables complete round trip cycles for authoring OpenWhisk actions inside the editor.

The key point for this extension is that it has full round trip for OpenWhisk actions (*list, create new local, create new remote, update, import from remote system, invoke, etc.*) without the need to leave the IDE which makes development cycles far shorter and easier. The extension works for action written in different languages (like *JavaScript and Swift*) and on different platforms (like *Windows, Mac, and Linux*).

In the future we plan to provide more such plug-ins for additional IDEs (this is no official commitment) and hence seek for early feedback.

First, download *VS Code* for your platform from here: https://code.visualstudio.com/  
Next, download the extension from here: https://ibm.box.com/s/r4pdwpdmmceubzpnmsskp3hoh65r9zmm (in the near future you will also get the latest code from here: https://github.com/openwhisk/openwhisk-vscode#downloads)

To install the extension open *VS Code* and switch to the extensions view (`View → Extensions`).  
Click the `more` menu (represented by the `•••` icon at the very top) and select `install from VSIX...`  
Point to the `VSIX file` you downloaded.

Once you have the extension installed, you will have to run `wsk property set` inside of *VS Code* to set the `apihost`, `auth`, and `namespace` values the same way you did configure your local CLI at the very beginning of this workshop:

Open the command palette via `View → Command Palette` or by pressing `F1` and entering: `wsk property set`

When prompted select the option `apihiost` and press `enter`.  
Next enter the correct value for the apihost property.

In the console you should see a result like this:

<pre>
$ wsk property set apiHost openwhisk.ng.bluemix.net
set config: apiHost=openwhisk.ng.bluemix.net
Configuration saved in C:\Users\IBM_ADMIN\.openwhisk\vscode-config.json
</pre>

Repeat this procedure to set the proper values for the `auth` and `namespace` properties.

Notice that you can retrieve the correct values from here (after clicking the `Looking for the wsk CLI?` link at the very bottom of the screen): https://new-console.ng.bluemix.net/openwhisk/cli

Now switch to the explorer (`View → Explorer`), implement the following action and save the file (name it `helloFromVSCode.js`):

```javascript
function main() {
    return { message: "Hello from VS Code" };
}
```

Press `F1` to open the command palette and enter:

<pre>
wsk action create
</pre>

When prompted enter an identifier for your action like `helloFromVSCode`.

In the console you should see a result like this:

<pre>
$ wsk action create helloFromVSCode
Creating a new action using the currently open document: file:///c%3A/Users/IBM_ADMIN/Downloads/helloFromVSCode.js
OpenWhisk action created: andreas.nauerz@de.ibm.com_dev/helloFromVSCode
</pre>

Finally, invoke the action by opening the command palette (`F1`) again and entering:

<pre>
wsk action invoke
</pre>

From the pull-down menu appearing select the action to be invoke – in our case the one named `helloFromVSCode`.

In the console you should see a result like this:

<pre>
$ wsk action invoke helloFromVSCode
......
{
    "result": {
        "message": "Hello from VS Code"
    },
    "success": true,
    "status": "success"
}
>> completed in 1855ms
</pre>

Feel free to experiment with the extension a bit on your own and provide us with any feedback you have.

## Developing with the Serverless Framework

Very recently we have announced our integration with the *Serverless Framework* (https://serverless.com/framework/). Hence, developers can now use the framework to build applications for the OpenWhisk platform.

The *Serverless Framework* is the most popular open-source framework for building serverless applications. Launching back in 2015, under a different name, the framework has experienced tremendous growth and now has over fourteen thousands stars on *Github*.

Thousands of developers are using the tool to build serverless applications every day.

Using a simple manifest file, developers can define serverless functions, connect them to event sources and declare cloud services needed by their application.

The framework handles deploying these serverless applications to the cloud provider. It also allows developers to monitor services in production, roll-out updates and assist debugging issues.

It also has a vibrant ecosystem of third-party plugins to extend the functionality of the framework.

With the aforementioned integration developers using the framework can now choose to deploy their serverless applications to any OpenWhisk platform instance. Multi-provider support also means moving applications between platforms is much easier and developers can even develop multi-cloud serverless applications.

### Installing the Serverless Framework

First, let's install the framework and the required dependencies:

<pre>
$ sudo npm install --global serverless serverless-openwhisk
</pre>

Now, using the `create` command, you can create an example service from the following the [following template](https://github.com/serverless/serverless/tree/master/lib/plugins/create/templates/openwhisk-nodejs).

<pre>
$ serverless create --template openwhisk-nodejs --path my_service
$ cd my_service
$ npm install
</pre>

Finally, let's deploy (the boilerplate includes an example that can be deployed without modification):

<pre>
$ serverless deploy
</pre>

If the deployment succeeds, the following messages will be printed to the console:

<pre>
$ serverless deploy
Serverless: Packaging service...
Serverless: Compiling Functions...
Serverless: Compiling API Gateway definitions...
Serverless: Compiling Rules...
Serverless: Compiling Triggers & Feeds...
Serverless: Deploying Functions...
Serverless: Deployment successful!

Service Information
platform:	openwhisk.ng.bluemix.net
namespace:	_
service:	my_service

actions:
[...]

triggers:
[...]

rules:
[...]

endpoints:
[...]

web-actions:
[...]
</pre>

### Working with Actions

First open the `serverless.yml` file and try to understand its basic structure which is pretty self-explanatory. It defines some of the OpenWhisk entities you have learned about before. For instance, it defines the name of your service (which represents the collection of all your artifacts), some functions (aka actions) and properties of these (like the handlers containing their code) and so forth. It also defines that you are working with OpenWhisk as your serverless engine.

One of the functions defined in the `serverless.yml` is called `hello`. The corresponding code lives in the file `handler.js` and, to be more precise, in a function the handler is pointing to (which is the function `main`).

Now, let's use the `invoke` command to test your newly deployed service:

<pre>
$ serverless invoke --function hello
{
    "payload": "Hello, World!"
}
</pre>

And once again with parameters:

<pre>
$ serverless invoke --function hello --data '{"name": "OpenWhisk"}'
{
    "payload": "Hello, OpenWhisk!"
}
</pre>

### Working with Sequences

Open the `serverless.yml` file and let's define a sequence by reusing the actions `myUtil/sort` and `myUtil/head` again. To define the sequence simply extend the `functions` section like this:

<pre>
functions:
    [...]
    mySequence:
        sequence:
            - /_/myUtil/sort
            - /_/myUtil/head
</pre>

Next, redeploy the service:

<pre>
$ serverless deploy
</pre>

Next, test the sequence:

<pre>
$ serverless invoke --function mySequence --data '{"lines":["c","b","a"]}'
{
    "lines": [
        "a"
    ],
    "num": 1
}
</pre>

### Connecting API Endpoints

Open the `serverless.yml` file and define an API endpoint for the `hello` action we have worked with prior. To define the endpoint simply extend the `functions` section like this:

<pre>
functions:
    [...]
    hello:
        handler: hello.handler
        events:
            - http: GET /api-demo/hello
</pre>

Next, redeploy the service:

<pre>
$ serverless deploy
</pre>

Watch the output of the redeployment.

Use the shown endpoints' `URL` to invoke the `hello` action:

<pre>
$ curl --request GET <endpoint_URL>
{
  "payload": "Hello, World!"
}
</pre>

### Working with Triggers and Rules

Open the `serverless.yml` file and define an triggers and rules for the `hello` action we have worked with prior. To define the endpoint simply extend the `functions` section like this:

<pre>
functions:
    [...]
    hello:
        handler: hello.handler
        events:
            - http: GET /api-demo/hello
            - trigger: myHelloTrigger
            - rule: myHelloRule
</pre>

Next, redeploy the service:

<pre>
$ serverless deploy
</pre>

Test the trigger and rule the same way you did earlier.
You can learn more about using the *Serverless Framework* here: https://github.com/serverless/serverless-openwhisk

### Packaging your weather services

At this point it may be a good exercise to package together the previously implemented weather services using the *Serverless Framework* – we leave this as a voluntary exercise for you.

# Node-REDとIBM Cloud Functions

IoTアプリケーションはサーバーレスプラットホームの殊に素晴らしいユースケースになりえます。

サーバーレスはIoTソリューションを構築するのに実に適切です。IoTアプリケーションは元々イベントドリブン型であり、予想ができないトラフィックパターンを持ちます。IoTではアプリケーションはしばしば接続された外部デバイスからデータを聞き出し、処理をかけた後に内部のデータストアに引き渡します。

このセクションでは、IoTデバイスやAPIやオンラインサービスをIBM Cloud Functionsと連携するために、有名なオープンソースツールを用います。

*Node-RED* は「IoTを結び合せるビジュアルツール」と自身を表現しています。ブラウザベースのエディタで、視覚的に「メッセージフロー」を構築してデバイスとオンラインのAPIやサービスを接続できます。一度メッセージフローが構築されれば、開発者はバックエンドサービスにそのフローをデプロイし起動させることができます。 *Node-RED* はデバイスやオンラインサービスやAPIを個別の「ノード」として表現します。サードパーティによるノードコミュニティが形成されており、ほとんどすべてのハードウェアデバイスやAPIやサードパーティサービスに対応できます。

IBM Cloud Functionsはアクションやトリガーを起動するための *Node-RED* 向けのノードを提供しています。これらのノードによって *Node-RED* のランタイムを通してリソースを作成したり呼び出したりできます。 *Node-RED* をIBM Cloud Functionsノードと共に使うと、サーバレスプラットフォームと連携されたIoTアプリケーションを簡単に構築できます。

## Node-REDのインストール

まずは *Node-RED* ローカル環境にインストールすることから始めましょう。

*Node-RED* は開発者がコマンドラインユーティリティとしてツールをインストールするのに`Node.js`ランタイムと`Node Package Manager`を用いています。もしNode.jsをローカル環境にインストールしていなければ、まずは環境を整えることから始めましょう(https://nodejs.org/en/)。

以下のコマンドを実行し *Node-RED* をすべてのユーザーが利用可能なコマンドラインユーティリティとしてインストールしましょう。

<pre>
$ npm install -g node-red
</pre>

このコマンドを実行して *Node-RED* とそれに全依存物をインストールするにはしばらく時間が必要です。`npm`はこのプロセスの間に多くのログメッセージを生成するでしょうがそれで通常です。エラーなくコマンドが実行終了すれば、このアプリケーションを利用開始できます。

## Node-REDの開始

*Node-RED* がインストールされれば、以下のコマンドで開始できます。

<pre>
$ node-red
</pre>

すると以下のメッセージが出力されます。

<pre>
Welcome to Node-RED
===================
24 Oct 10:33:00 - [info] Node-RED version: v0.15.1
24 Oct 10:33:00 - [info] Node.js  version: v6.2.2
24 Oct 10:33:00 - [info] Darwin 16.0.0 x64 LE
24 Oct 10:33:00 - [info] Loading palette nodes
24 Oct 10:33:01 - [info] Settings file  : /Users/andreas/.node-red/settings.js
24 Oct 10:33:01 - [info] User directory : /Users/andreas/.node-red
24 Oct 10:33:01 - [info] Flows file     : /Users/andreas/.node-red/flows.json
24 Oct 10:33:01 - [info] Server now running at http://127.0.0.1:1880/
24 Oct 10:33:01 - [info] Starting flows
24 Oct 10:33:01 - [info] Started flows
</pre>

*Node-RED* を開始すると、サーバが1880番ポートで起動します。
ウェブブラウザを開き、次のURLを入力してエディタを開きましょう。http://localhost:1880

*ノード* は画面左部のパレットにあります。ユーザーは画面左部のノードをドラッグ＆ドロップしてグリッドの上に置いて「メッセージフロー」を構築します。グリッド上のノードは「ワイヤー」で接続されメッセージを交換し合います。

*Node-RED* に関するドキュメントがもっと欲しければ、プロジェクトのウェブサイトを参照してください。http://nodered.org/docs/

## Node-REDで"Hello World"

それでは”Hello World"サンプルからまずは始めてみましょう。

### Injectノードの追加
`Inject`ノードはフローにinjectメッセージを加えます。ノード上のボタンを押すか入力の間隔をセットすることで起動します。

パレットからワークスペースにノードを1つドラッグします。
サイドバーを開き(`Ctrl+Space`またはドロップダウンメニューで開きます)、`情報`タブを選択します。
新規に追加した`Inject`ノードを選択肢、プロパティ情報やその機能の詳細を確認します。

### Debugノードの追加

`Debug`ノードはデバッグサイドバーにあらゆるメッセージを表示します。デフォルト状態ではメッセージのペイロードを表示するだけですが、メッセージオブジェクトをすべて表示することも可能です。

パレットからDebugノードを1つワークスペースにドラッグしましょう。

### ノードの連結

`Inject`ノードと`Debug`ノードをその出力ポートと入力ポートをドラッグでつなぐことで連結しましょう。

### デプロイ

この状態ではノードはエディタ上に存在しているだけなので、これをサーバにデプロイする必要があります。
`デプロイ`ボタンをクリックします。シンプルでしょう？

デバッグサイドバータブを選択し、(Injectノードの左に飛び出ている)`Inject`ボタンをクリックします。サイドバーに数字が出てくるでしょう。デフォルト状態では、`Inject`ノードはペイロードとして1970年1月1日から何ミリ秒経過したかを表示します。ここからはより有用なことに挑戦してみましょう。

### Functionノードの追加

`Function`ノードは *JavaScript* 関数を通してメッセージを引き渡します。

`Function`ノードを`Inject`ノードと`Debug`ノードの間に配置し接続します。(キーボード上の`delete`キーを押し)既存のワイヤを削除します。

次に`Function`ノードをダブルクリックして編集ダイアログを開きます。
次のコードを関数フィールドにコピーします。

```javascript
// Create a Date object from the payload
var date = new Date(msg.payload);
// Change the payload to be a formatted Date string
msg.payload = date.toString();
// Return the message so it can be sent on
return msg;
```

次に`完了`ボタンをクリックして編集ダイアログを閉じ、`デプロイ`ボタンをクリックします。
もう一度`Inject`ボタンをクリックすれば、スライドバーのメッセージはより読み取りしやすいタイムスタンプになるでしょう。

この例でどのようにエディタを用いてノードを接続し、フローを構築して *Node-RED* ランタイムにデプロイできるかがわかったでしょう。

パレット内の他のノードを自由に使い、より複雑なフローを構築してみましょう。

## Node-REDにノードを追加

Node-REDには何千ものサードパーティデバイスやAPIやオンラインサービスと接続するためのノードを発行した外部開発者による巨大コミュニティがあります。

このウェブサイトには全てのノードが収蔵されています。http://flows.nodered.org/

IBM Cloud functionsノードを *Node-RED* にインストールしましょう。
検索バーに`openwhisk`と入力すると、2つのインストール可能なエンティティが表示されます。

公式サポートされた *Node-RED* 用のIBM Cloud Functionsノードが入った`node-red-node-openwhisk`をインストールします。

*Node-RED* エディタに戻り、画面右上部のメニューアイコンをクリックし、`パレットの管理`をクリックします。
画面左側にノードをインストールするためのダイアログが表示されます。この画面にはインストール済みのノードとインストール可能な外部ノードが表示されます。これを使ってIBM Cloud Functionsのノードをインストールします。

パレットの`ノードを追加`タブを選択し、`node-red-node-openwhisk`と入力します。
`ノードを追加`ボタンをクリックします。

メインパレットメニューに戻れば、IBM Cloud Functions(Openwhisk)ノードが追加されていることがわかるでしょう。

### Node-REDからIBM Cloud Functionsアクションを呼び出し

ノードがインストールできたので、IBM Cloud Functionsアクションを呼び出すフローを作成しましょう。

まず、Openwhisk `action`ノードをフローパネルに配置します。
必ず(`trigger`ノードではなく)入力ポートと出力ポートを有している`action`ノードをドラッグしてください。入力ポートはアクションを引き起こすメッセージを受け取り、(必要に応じて)呼び出しのためのパラメータを引き渡します。出力ポートはアクティベーションのレスポンスメッセージを返します。

次にノードをダブルクリックし、編集パネルを開きます。
この編集パネルではフローにメッセージが達した時にアクションが呼び出されるためのアクションの名前とnamespaceを定義できます。これらのパラメータはメッセージオブジェクトのプロパティとしてパラメータを引き渡すことによりランタイムで無効化できます。

しかし、アクションを呼び出す前に、 *Node-RED* が通信するためのIBM Cloud Functionsプラットホームを準備しましょう。

Service設定用ドロップダウンの横の`鉛筆`アイコンをクリックします。

フォームに以下の情報を埋めます。
* `API URL`: `https://openwhisk.ng.bluemix.net/api/v1`
* `Auth Key`: 認証キーはUse the CLIをクリックすれば確認できます。 (https://console.ng.bluemix.net/openwhisk/cli)
* `Name`: `OpenWhisk`

`追加`をクリックして、このサービスを *Node-RED* に追加します。

これで呼び出したいアクションの`action名`と`namespace`の値を埋められます(Use the CLIをクリックで確認できます。)。
これまでに作成した`hello`アクションを使いましょう。

そうしたら、もう一度(先ほどのものを削除していたら)`Inject`ノードと`Debug`ノードをフローグリッドに追加します。その間にIBM Cloud Functionsノードを配置し接続します。
それから画面右上部の`デプロイ`ボタンｗ押してフローをデプロイします。
`Inject`ノードをいくらかクリックすれば、アクションを引き起こし、呼び出し結果がデバッグパネルに反映されるでしょう。

<pre>
{"message: "Hello, undefined from undefined"}
</pre>

次に`Inject`ノードで生成された入力メッセージに`name`パラメータを加えるためにフローをアップデートしましょう。`Inject`ノードの編集パネルを開きペイロードのタイプを *JSON* に変えましょう。

以下の値を追加します。

<pre>
{"name": "Bernie"}
</pre>

`Inject`ノードの設定を保存し、デプロイしたら、また何度かInjectメッセージを入力します。`Barnie Sanders`という名前を伴うメッセージが返ってくるでしょう。

<pre>
{"message: "Hello, Bernie from undefined"}
</pre>

幸運にもうまく動いたようです。 *Node-RED* を使ったトリガーの起動に移る前にあなた自身の`place`の情報をパラメータに加えてみてはどうでしょう？

## Node-REDからのFunctionsトリガーの呼び出し

OpenWhisk`トリガー`ノードをフローパネルにドラッグします。

`トリガー`ノードは入力ポートのみを有し、トリガーを起動するメッセージを受け取って、(必要に応じて)呼び出しのためのパラメータを引き渡します。

さあ、ノードをダブルクリックし、編集パネルを開きましょう。
この編集パネルでは、メッセージがフローに達した際にトリガーを起動するための`name`と`namespace`を定義できます。これらのパラメータは、パラメータをメッセージオブジェクトのプロパティとして引き渡すことでランタイムでは無効化されます。

繰り返しになりますが、ここでは呼び出したいトリガーの`service`、`name`、`namespace`を埋めることができます。すでにIBM Cloud Functionsのサービス資格情報を設定していますから、ここはもう一度設定する必要はありません。

これまでに作成した`locationUpadate`トリガーを使っていきましょう。

まず、フローエディタ画面に戻る前にノードの設定を保存します。
画面上の`Inject`ノードと今作成した`トリガー`ノードを接続します。
画面右上部の`デプロイ`ボタンをクリックしてデプロイします。
`Inject`ノードを数回クリックし、この新しい呼び出しをテストします。

`wsk`コマンドラインユーティリティを用い、呼び出しログをチェックしてみてください。アクティベーションは現れたでしょうか？

### 新規IBM Cloud FunctionsアクションをNode-REDから作成

IBM Cloud Functionsのノードを使えば、 *Node-RED* の編集パネルを通して新たなアクションを定義できます。設定パネル内のコードエディタを用い、既存/新規のアクションのソースを作成/アップデートできます。

既存の`hello`アクションを用い、ソースコードのアップデートをしましょう。

まず、OpenWhisk `action`ノードをダブルクリックし、編集パネルを開きましょう。
アクションのソースコードが自動的に映し出されます。
次に、アクションが返すgreeting文字列を変えましょう。
`Allow Edits`のチェックボックスを選択します。
greeting文字列を以下のように編集します。

<pre>
"Salutations " + params.name + "!"
</pre>

さあ、新たに`key`(`name`)と`value`(`Donald`)のパラメータを追加します。
次に、`完了`をクリックして、変更を保存します。
フローをアップデートする前に、`Inject`ノードのペイロードをタイムスタンプに変更し直して、アクションがデフォルトのパラメータを使えるようにしましょう。
一度これを完了すれば、フローをデプロイしコンソール上の結果を持ち出せます。今回は、アップデートされたgreetingとデフォルトのパラメータを用いた新しいメッセージが返されることでしょう。

# イケてるアプリは目前に!

ここからは4つの一般に利用可能なIBM Cloud Functionsでなにができるかを示したサンプルをご紹介します。

## Vision App

Vision Appの詳細はこちら。
https://github.com/IBM-Bluemix/openwhisk-visionapp

Vision AppはiOSアプリのサンプルで、IBM Visual Recognitionの技術を用いて、自動的にイメージにタグ付けしたり顔認識をしたりします。
これを使えば、撮影したばかりの写真や既存のイメージを使って、アプリケーション上で、タグのリストを作ったり、写真上の人や建造物や物体を特定したりすることができます。そしてその結果をSNSでシェアすることができます。

## Dark Vision

Dark Visionの詳細はこちら。
https://github.com/IBM-Bluemix/openwhisk-darkvisionapp

Dark Visionは映像のダークデータを探し出します。IBM Watson Visual Recognitionを用いてビデオのフレームを分析し、タグや映像上の有名人や建造物を使って映像のサマリーを作ります。このサマリーによって、映像を見つけ出したりカテゴリー分けしたりすることが容易になります。

## Skylink

Skylinkの詳細はこちら。
https://github.com/IBM-Bluemix/skylink

Skylinkを使えばDJIドローンを *IBM Cloud* に連携し、*IBM Cloudant, IBM Cloud Functions, IBM Watson, Alchemy Vision* などを用いて、リアルタイムに近いイメージ分析を行うことができます。

# もっと知りたい！

こちらのリソースからIBM Cloud Functionsの知識をより深めることができます。

* IBM Cloud Functions: https://www.ibm.com/cloud/functions
* Apache OpenWhisk: http://openwhisk.org
* OpenWhisk on Github: https://github.com/openwhisk/openwhisk/
* OpenWhisk on Twitter: https://twitter.com/openwhisk
* OpenWhisk on Medium: https://medium.com/openwhisk
* OpenWhisk additional material on Slideshare: http://www.slideshare.net/OpenWhisk
* OpenWhisk additional material on Youtube: https://www.youtube.com/channel/UCbzgShnQk8F43NKsvEYA1SA
* OpenWhisk on Slack: http://slack.openwhisk.org/
* Other OpenWhisk material: https://github.com/openwhisk/awesome-openwhisk
* Composer: https://github.com/ibm-functions/composer
* The Serverless Framework: https://github.com/serverless/serverless-openwhisk
* Node-RED: https://nodered.org/

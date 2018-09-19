[![FIWARE Banner](https://fiware.github.io/tutorials.PEP-Proxy/img/fiware.png)](https://www.fiware.org/developers)

[![FIWARE Security](https://img.shields.io/badge/FIWARE-Security-ff7059.svg?logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABsAAAAVCAYAAAC33pUlAAAABHNCSVQICAgIfAhkiAAAA8NJREFUSEuVlUtIFlEUx+eO+j3Uz8wSLLJ3pBiBUljRu1WLCAKXbXpQEUFERSQF0aKVFAUVrSJalNXGgmphFEhQiZEIPQwKLbEUK7VvZrRvbr8zzjfNl4/swplz7rn/8z/33HtmRhn/MWzbXmloHVeG0a+VSmAXorXS+oehVD9+0zDN9mgk8n0sWtYnHo5tT9daH4BsM+THQC8naK02jCZ83/HlKaVSzBey1sm8BP9nnUpdjOfl/Qyzj5ust6cnO5FItJLoJqB6yJ4QuNcjVOohegpihshS4F6S7DTVVlNtFFxzNBa7kcaEwUGcbVnH8xOJD67WG9n1NILuKtOsQG9FngOc+lciic1iQ8uQGhJ1kVAKKXUs60RoQ5km93IfaREvuoFj7PZsy9rGXE9G/NhBsDOJ63Acp1J82eFU7OIVO1OxWGwpSU5hb0GqfMydMHYSdiMVnncNY5Vy3VbwRUEydvEaRxmAOSSqJMlJISTxS9YWTYLcg3B253xsPkc5lXk3XLlwrPLuDPKDqDIutzYaj3eweMkPeCCahO3+fEIF8SfLtg/5oI3Mh0ylKM4YRBaYzuBgPuRnBYD3mmhA1X5Aka8NKl4nNz7BaKTzSgsLCzWbvyo4eK9r15WwLKRAmmCXXDoA1kaG2F4jWFbgkxUnlcrB/xj5iHxFPiBN4JekY4nZ6ccOiQ87hgwhe+TOdogT1nfpgEDTvYAucIwHxBfNyhpGrR+F8x00WD33VCNTOr/Wd+9C51Ben7S0ZJUq3qZJ2OkZz+cL87ZfWuePlwRcHZjeUMxFwTrJZAJfSvyWZc1VgORTY8rBcubetdiOk+CO+jPOcCRTF+oZ0okUIyuQeSNL/lPrulg8flhmJHmE2gBpE9xrJNkwpN4rQIIyujGoELCQz8ggG38iGzjKkXufJ2Klun1iu65bnJub2yut3xbEK3UvsDEInCmvA6YjMeE1bCn8F9JBe1eAnS2JksmkIlEDfi8R46kkEkMWdqOv+AvS9rcp2bvk8OAESvgox7h4aWNMLd32jSMLvuwDAwORSE7Oe3ZRKrFwvYGrPOBJ2nZ20Op/mqKNzgraOTPt6Bnx5citUINIczX/jUw3xGL2+ia8KAvsvp0ePoL5hXkXO5YvQYSFAiqcJX8E/gyX8QUvv8eh9XUq3h7mE9tLJoNKqnhHXmCO+dtJ4ybSkH1jc9XRaHTMz1tATBe2UEkeAdKu/zWIkUbZxD+veLxEQhhUFmbnvOezsJrk+zmqMo6vIL2OXzPvQ8v7dgtpoQnkF/LP8Ruu9zXdJHg4igAAAABJRU5ErkJgggA=)](https://www.fiware.org/developers/catalogue/)
[![License: MIT](https://img.shields.io/github/license/fiware/tutorials.Time-Series-Data.svg)](https://opensource.org/licenses/MIT)
[![Documentation](https://readthedocs.org/projects/fiware-tutorials/badge/?version=latest)](https://fiware-tutorials.readthedocs.io/en/latest)

このチュートリアルでは、FIWARE [Wilma](https://fiware-pep-proxy.rtfd.io/) PEP Proxy と **Keyrock** を組み合わせて、FIWARE Generic Enablersによって公開されるエンドポイントへのアクセスを保護します。ユーザ、または他のアクターは、ログインし、トークンを使用してサービスにアクセスする必要があります。[以前のチュートリアル](https://github.com/Fiware/tutorials.Securing-Access)で作成したアプリケーション・コードを展開して、分散システム全体のユーザを認証します。FIWARE Wilma (PEP Proxy) の設計について説明し、他のサービスの認証に関連する Keyrock GUI と REST API の部分について詳しく説明します。

[cUrl](https://ec.haxx.se/) コマンドは、Keyrock および Wilma REST API にアクセスするために全面的に使用されています。これらの呼び出しに [Postman documentation](http://fiware.github.io/tutorials.PEP-Proxy/) も利用できます。

[![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/6b143a6b3ad8bcba69cf)

# コンテンツ

- [PEP Proxy を使用したマイクロ・サービスの保護](#securing-microservices-with-a-pep-proxy)
  * [ID 管理の標準概念](#standard-concepts-of-identity-management)
  * [:arrow_forward: ビデオ : Wilma PEP Proxy の紹介](#arrow_forward-video--introduction-to-wilma-pep-proxy)
- [前提条件](#prerequisites)
  * [Docker](#docker)
  * [Cygwin](#cygwin)
- [アーキテクチャ](#architecture)
- [起動](#start-up)
  * [登場人物 (Dramatis Personae)](#dramatis-personae)
  * [REST API を使用した Keyrock へのログイン](#logging-in-to-keyrock-using-the-rest-api)
    + [パスワードでトークンを作成](#create-token-with-password)
    + [トークン情報を取得](#get-token-info)
- [PEP Proxies と IoT Agents の管理](#managing-pep-proxies-and-iot-agents)
  * [:arrow_forward: ビデオ : Wilma PEP Proxy の設定](#arrow_forward-video--wilma-pep-proxy-configuration)
  * [PEP Proxies と IoT Agents の管理 - 起動](#managing-pep-proxies-and-iot-agents---start-up)
  * [PEP Proxy CRUD アクション](#pep-proxy-crud-actions)
    + [PEP Proxy の作成](#create-a-pep-proxy)
    + [PEP Proxy の詳細を読み込む](#read-pep-proxy-details)
    + [PEP Proxy のパスワードをリセット](#reset-password-of-a-pep-proxy)
    + [PEP Proxy の削除](#delete-a-pep-proxy)
  * [IoT Agent の CRUD アクション](#iot-agent-crud-actions)
    + [IoT Agent を作成](#create-an-iot-agent)
    + [IoT Agent の詳細を読み込む](#read-iot-agent-details)
    + [IoT Agents の 一覧](#list-iot-agents)
    + [IoT Agent のパスワードをリセット](#reset-password-of-an-iot-agent)
    + [IoT Agent を削除](#delete-an-iot-agent)
- [Orion Context Broker のセキュリティ保護](#securing-the-orion-context-broker)
  * [Orion の保護 - PEP Proxy の設定](#securing-orion---pep-proxy-configuration)
  * [Orion の保護 - アプリケーションの設定](#securing-orion---application-configuration)
  * [Orion の保護 - 起動](#securing-orion---start-up)
    + [:arrow_forward: ビデオ : REST API を保護](#arrow_forward-video--securing-a-rest-api)
  * [ユーザが REST API を使用してアプリケーションへのログイン](#user-logs-in-to-the-application-using-the-rest-api)
    + [PEP Proxy - アクセス・トークンのない Orion へのアクセス拒否](#pep-proxy---no-access-to-orion-without-an-access-token)
    + [Keyrock - ユーザによるアクセス・トークンの取得](#keyrock---user-obtains-an-access-token)
    + [PEP Proxy - アクセス・トークンを使用して Orion にアクセス](#pep-proxy---accessing-orion-with-an-access-token)
  * [Orion の保護 - サンプル・コード](#securing-orion---sample-code)
- [IoT Agent の保護](#securing-an-iot-agent)
  * [IoT Agent の保護 - PEP Proxy の設定](#securing-an-iot-agent---pep-proxy-configuration)
  * [IoT Agent の保護 - アプリケーションの設定](#securing-an-iot-agent---application-configuration)
  * [IoT Agent のセキュリティ確保 - 起動](#securing-iot-agent---start-up)
  * [IoT センサが REST API を使用してアプリケーションにログイン](#iot-sensor-logs-in-to-the-application-using-the-rest-api)
    + [Keyrock - IoT センサによるアクセス・トークンの取得](#keyrock---iot-sensor-obtains-an-access-token)
    + [PEP Proxy - アクセス・トークンを使用して IoT Agent にアクセス](#pep-proxy---accessing-iot-agent-with-an-access-token)
  * [IoT Agent の保護 - サンプル・コード](#securing-an-iot-agent----sample-code)


<a name="securing-microservices-with-a-pep-proxy"></a>
# PEP Proxy を使用したマイクロ・サービスの保護

> "Oh, it's quite simple. If you are a friend, you speak the password, and the doors will open."
>
>  — Gandalf (The Fellowship of the Ring by J.R.R Tolkien)

[以前のチュートリアル](https://github.com/Fiware/tutorials.Securing-Access)は、アプリケーション内で自身を識別認証されたユーザに基づいて、リソースへのアクセスを許可または拒否することが可能であることを実証しました。それが `access_token` 見つからなかった場合 (レベル1 - *Authentication Access*, 認証アクセス)、または、与えられた `access_token` が適切な権利を持っていることを確認すること (レベル2 - *Basic Authorization*, 基本認可) は、さまざまラインの実行に続くコードの問題でした。FIWARE ベースの Smart Solution 内の他サービスの前に Policy Enforcement Point (PEP) を置くことで、アクセスを保護する同じ方法を適用できます。

**PEP Proxy** は、保護されたリソースの前方に位置し、"既知の" 公共の場所で見つかるエンドポイントです。リソース・アクセスのゲート・キーパーとして機能します。ユーザ、または他のアクターは、**PEP proxy** を成功させて **PEP proxy** を通過させるために、**PEP proxy** に十分な情報を提供する必要があります。**PEP proxy** は、リクエストをセキュリティ保護されたリソース自体の実際の場所に渡します。保護されたリソースの実際の場所は外部ユーザには分かりません。**PEP proxy** の背後にあるプライベート・ネットワーク または、別のマシン上にあります。

FIWARE [Wilma](https://fiware-pep-proxy.rtfd.io/) は、FIWARE [Keyrock](http://fiware-idm.readthedocs.io/) Generic Enabler で動作するように設計された **PEP proxy**  の簡単なインプリケーションです。ユーザが **PEP proxy** の背後にあるリソースにアクセスしようとするたびに、PEP はユーザの属性を Policy Decision Point (PDP) に記述し、セキュリティの決定をリクエストし、決定を実行します。許可または拒否です。許可されたユーザのアクセスが最小限になります。受信したレスポンスは、セキュリティで保護されたサービスに直接アクセスした場合と同じです。権限のないユーザには、**401 - Unauthorized** レスポンスが戻されます。

<a name="standard-concepts-of-identity-management"></a>
## ID 管理の標準概念

**Keyrock** Identity Management データベースには、次の共通オブジェクトがあります :

* **User** - 電子メールとパスワードを使用して自分自身を識別できる、登録済みのユーザ。ユーザには、個別にまたはグループとして権利を割り当てることができます
* **Application** -  一連のマイクロ・サービスで構成された任意のセキュアな FIWARE アプリケーション
* **Organization** - 一連の権利を割り当てることができるユーザのグループ。組織の権利を変更すると、その組織のすべてのユーザのアクセスが影響を受けます
* **OrganizationRole** - ユーザは組織のメンバまたは管理者になることができます。管理者は組織にユーザを追加または削除できます。メンバは組織のロールと権限を取得するだけです。これにより、各組織はメンバに対して責任を持つことができ、スーパー管理者 (super-admin) がすべての権限を管理する必要がなくなります
* **Role** - ロールは、一連のアクセス許可の説明的なバケットです。ロールは、単一のユーザまたは組織に割り当てることができます。サインインしたユーザは、自分のすべてのロールとその組織に関連付けられているすべてのロールのすべての権限を取得します
* **Permission** - システム内のリソース上で何かを行う能力

さらに、FIWARE アプリケーション内で、2つの人以外のアプリケーション (non-human application) のオブジェクトを保護することができます。

* **IoTAgent** - IoT センサと Context Broker 間のプロキシ
* **PEPProxy** - ユーザの権利を確認する Generic Enabler 間での使用のためのミドルウェア

オブジェクト間の関係を示します。赤でマークされたエンティティは、このチュートリアルで直接使用されています :

![](https://fiware.github.io/tutorials.PEP-Proxy/img/entities.png)

<a name="arrow_forward-video--introduction-to-wilma-pep-proxy"></a>
## :arrow_forward: ビデオ : Wilma PEP Proxy の紹介

[![](http://img.youtube.com/vi/8tGbUI18udM/0.jpg)](https://www.youtube.com/watch?v=8tGbUI18udM "Introduction")

紹介ビデオを見るには上記の画像をクリックしてください :

<a name="prerequisites"></a>
# 前提条件

<a name="docker"></a>
## Docker

物事を単純にするために、両方のコンポーネントが [Docker](https://www.docker.com) を使用して実行されます。**Docker** は、さまざまコンポーネントをそれぞれの環境に分離することを可能にするコンテナ・テクノロジです。

* Docker Windows にインストールするには、[こちら](https://docs.docker.com/docker-for-windows/)の手順に従ってください
* Docker Mac にインストールするには、[こちら](https://docs.docker.com/docker-for-mac/)の手順に従ってください
* Docker Linux にインストールするには、[こちら](https://docs.docker.com/install/)の手順に従ってください

**Docker Compose** は、マルチコンテナ Docker アプリケーションを定義して実行するためのツールです。[YAML file](https://raw.githubusercontent.com/Fiware/tutorials.Identity-Management/master/docker-compose.yml) ファイルは、アプリケーションのために必要なサービスを構成するために使用します。つまり、すべてのコンテナ・サービスは1つのコマンドで呼び出すことができます。Docker Compose は、デフォルトで Docker for Windows とDocker for Mac の一部としてインストールされますが、Linux ユーザは[ここ](https://docs.docker.com/compose/install/)に記載されている手順に従う必要があります。

<a name="cygwin"></a>
## Cygwin

シンプルな bash スクリプトを使用してサービスを開始します。Windows ユーザは [cygwin](http://www.cygwin.com/) をダウンロードして、Windows 上の Linux ディストリビューションと同様のコマンドライン機能を提供する必要があります。

<a name="architecture"></a>
# Architecture

このアプリケーションは、以前のチュートリアルで作成したサービスの周りに **PEP Proxy** インスタンスを追加することで、既存の在庫管理、および、センサ・ベースのアプリケーションへのアクセスを保護し、**Keyrock** が使用する **MySQL** データベースに事前入力されたデータを使用します。[Orion Context Broker](https://fiware-orion.readthedocs.io/en/latest/), [IoT Agent for UltraLight 2.0](http://fiware-iotagent-ul.readthedocs.io/en/latest/), [Keyrock](http://fiware-idm.readthedocs.io/) Generic Enabler の 4つの FIWARE コンポーネントを使用し、[Wilma](https://fiware-pep-proxy.rtfd.io/) **PEP Proxy** の 1つまたは 2つのインスタンスを追加して、どのインタフェースを保護するかを決定します。アプリケーションが *“Powered by FIWARE”* と認定されるには、Orion Context Broker を使用するだけで十分です。

Orion Context Broker と IoT Agent はオープンソースの [MongoDB](https://www.mongodb.com/) 技術を利用して、保持している情報の永続性を保ちます。[以前のチュートリアル](https://github.com/Fiware/tutorials.IoT-Sensors/)で作成した ダミー IoT デバイスも使用します。**Keyrock** は独自の [MySQL](https://www.mysql.com/) データベースを使用します。

したがって、全体的なアーキテクチャは次の要素で構成されます :

* FIWARE [Orion Context Broker](https://fiware-orion.readthedocs.io/en/latest/) は、[NGSI](https://fiware.github.io/specifications/OpenAPI/ngsiv2) を使用してリクエストを受信します
* [IoT Agent for UltraLight 2.0](http://fiware-iotagent-ul.readthedocs.io/en/latest/) は、[NGSI](https://fiware.github.io/specifications/OpenAPI/ngsiv2) を使用してサウスバウンド・リクエストを受信し、それをデバイスのために [UltraLight 2.0](http://fiware-iotagent-ul.readthedocs.io/en/latest/usermanual/index.html#user-programmers-manual) に変換します。
* FIWARE [Keyrock](http://fiware-idm.readthedocs.io/) は、以下を含んだ、補完的な ID 管理システムを提供します :
    * アプリケーションとユーザのための OAuth2 認証システム
    * ID 管理のための Web サイトのグラフィカル・フロントエンド
    * HTTP リクエストによる ID 管理用の同等の REST API
* FIWARE [Wilma](https://fiware-pep-proxy.rtfd.io/) は **Orion** および/または **IoT  Agent** マイクサービスへのアクセスを保護する PEP Proxy
* [MongoDB](https://www.mongodb.com/) データベース :
    * **Orion Context Broker** が、データ・エンティティ、サブスクリプション、レジストレーションなどのコンテキスト・データ情報を保持するために使用します
    * **IoT Agent** が、デバイスの URLs や Keys などのデバイス情報を保持するために使用します
* [MySQL](https://www.mysql.com/) データベース :
    * ユーザ ID、アプリケーション、ロール、および権限を保持するために使用されます
* **在庫管理フロントエンド**には、次のことを行います :
    * 店舗情報を表示します
    * 各店舗でどの商品を購入できるかを示します
    * ユーザが製品を"購入"して在庫数を減らすことができます
    * 許可されたユーザを制限されたエリアに入れることができます
* HTTP を介して実行されている [UltraLight 2.0](http://fiware-iotagent-ul.readthedocs.io/en/latest/usermanual/index.html#user-programmers-manual) プロトコルを使用する[ダミー IoT デバイス](https://github.com/Fiware/tutorials.IoT-Sensors)のセットとして機能する Web サーバ。特定のリソースへのアクセスが制限されています。

要素間のすべての対話は HTTP リクエストによって開始されるため、エンティティはコンテナ化され、公開されたポートから実行されます。

チュートリアルの各セクションの具体的なアーキテクチャについては、以下で説明します。

<a name="start-up"></a>
# 起動

インストールを開始するには、次の手順を実行します :

```console
git clone git@github.com:Fiware/tutorials.PEP-Proxy.git
cd tutorials.PEP-Proxy

./services create
```

>**注** Docker イメージの最初の作成には最大 3分かかります

その後、リポジトリ内で提供される [services](https://github.com/Fiware/tutorials.PEP-PRoxy/blob/master/services) Bash スクリプトを実行することによって、コマンドラインからすべてのサービスを初期化することができます :

```console
./services <command>
```

ここで、<command> は、私たちがアクティベートしたいエクササイズに応じてかわります。

>:information_source: **注:** クリーンアップをやり直したい場合は、次のコマンドを使用して再起動することができます :
>
>```console
>./services stop
>```
>

<a name="dramatis-personae"></a>
## 登場人物 (Dramatis Personae)

次の `test.com` のメンバは、アプリケーション内に正当なアカウントを持っています。

* Alice, 彼女は **Keyrock** アプリケーションの管理者になります
* Bod, スーパー・マーケット・チェーンの地域マネージャ。彼の下に数人のマネージャがいます :
  * Manager1
  * Manager2
* Charlie, スーパー・マーケット・チェーンのセキュリティ責任者。彼の下に数人の警備員がいます。
  * Detective1
  * Detective2

| 名前       | eMail                      |パスワード |
|------------|----------------------------|-----------|
| alice      | alice-the-admin@test.com   | `test`    |
| bob        | bob-the-manager@test.com   | `test`    |
| charlie    | charlie-security@test.com  | `test`    |
| manager1   | manager1@test.com          | `test`    |
| manager2   | manager2@test.com          | `test`    |
| detective1 | detective1@test.com        | `test`    |
| detective2 | detective2@test.com        | `test`   |

次の `example.com` のメンバはアカウントに登録しましたが、アクセスを許可する理由はありません。

* Eve - 盗聴者のイブ
* Mallory - 悪意のある攻撃者のマロリー
* Rob - 強盗のロブ

| 名前       | eMail                      |パスワード |
|------------|----------------------------|-----------|
| eve        | eve@example.com            | `test`    |
| mallory    | mallory@example.com        | `test`    |
| rob        | rob@example.com            | `test`    |

2つの組織が Alice によって設定されました :

| 名前       | 説明                                   | UUID                                 |
|------------|----------------------------------------|--------------------------------------|
| Security   | 店員のためのセキュリティ・グループ     |`security-team-0000-0000-000000000000`|
| Management | ストア・マネージャのための管理グループ |`managers-team-0000-0000-000000000000`|

適切なロールと権限を持つ 1つのアプリケーションも作成されました :

| キー          | 値                                     |
|---------------|----------------------------------------|
| Client ID     | `tutorial-dckr-site-0000-xpresswebapp` |
| Client Secret | `tutorial-dckr-site-0000-clientsecret` |
| URL           | `http://localhost:3000`                |
| RedirectURL   | `http://localhost:3000/login`          |

時間を節約するために、[以前のチュートリアル](https://github.com/Fiware/tutorials.Roles-Permissions)からユーザと組織を作成するデータがダウンロードされ、起動時に自動的に MySQL データベースに保存されるため、UUIDs が変更されず、データを再入力する必要もありません。


**Keyrock** MySQLデータベース は、ユーザ、パスワードなどの格納を含むアプリケーションのセキュリティのあらゆる側面を扱います。アクセス権を定義し、OAuth2 認証プロトコルを扱います。完全なデータベース関係図は[ここ](https://fiware.github.io/tutorials.Securing-Access/img/keyrock-db.png)にあります。

ユーザや組織、アプリケーションを作成する方法については、`http://localhost:3005/idm` で、アカウント `alice-the-admin@test.com` とパスワード `test` を使ってログインできます。

![](https://fiware.github.io/tutorials.PEP-Proxy/img/keyrock-log-in.png)

そして、周りを見回してください。

<a name="logging-in-to-keyrock-using-the-rest-api"></a>
## REST API を使用した Keyrock へのログイン

アプリケーションに入るには、ユーザ名とパスワードを入力します。デフォルトの Super-User は、`alice-the-admin@test.com` と `test` の値を持っています。URL ` https://localhost:3443/v1/auth/tokens` は安全なシステムでも動作するはずです。

<a name="create-token-with-password"></a>
### パスワードでトークンを作成

次の例では、Admin Super-User を使用してログインします :

#### :one: リクエスト : 
```console
curl -iX POST \
  'http://localhost:3005/v1/auth/tokens' \
  -H 'Content-Type: application/json' \
  -d '{
  "name": "alice-the-admin@test.com",
  "password": "test"
}'
```

#### レスポンス :

レスポンス・ヘッダは、誰がアプリケーションにログオンしているかを識別する `X-Subject-token` を返します。このトークンは、後続のすべてのリクエストにアクセスするために必要です。

```
HTTP/1.1 201 Created
X-Subject-Token: d848eb12-889f-433b-9811-6a4fbf0b86ca
Content-Type: application/json; charset=utf-8
Content-Length: 138
ETag: W/"8a-TVwlWNKBsa7cskJw55uE/wZl6L8"
Date: Mon, 30 Jul 2018 12:07:54 GMT
Connection: keep-alive
```
```json
{
    "token": {
        "methods": [
            "password"
        ],
        "expires_at": "2018-07-30T13:02:37.116Z"
    },
    "idm_authorization_config": {
        "level": "basic",
        "authzforce": false
    }
}
```

<a name="get-token-info"></a>
### トークン情報を取得

ユーザがログインすると、時間制限されたトークンがあれば、ユーザに関する詳細情報を見つけることができます。

このチュートリアルでは、長続きする `X-Auth-token=aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa` を使用して Alice のふりをすることができます。`{{X-Auth-token}}` と `{{X-Subject-token}}` は、Alice が自分自身について問い合わせを行っている場合に同じ値に設定することができます。

#### :two: リクエスト : 

```console
curl -X GET \
  'http://localhost:3005/v1/auth/tokens' \
  -H 'Content-Type: application/json' \
  -H 'X-Auth-token: {{X-Auth-token}}' \
  -H 'X-Subject-token: {{X-Subject-token}}'
```

#### レスポンス :

レスポンスは関連するユーザの詳細を返します :

```json
{
    "access_token": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa",
    "expires": "2036-07-30T12:04:45.000Z",
    "valid": true,
    "User": {
        "id": "aaaaaaaa-good-0000-0000-000000000000",
        "username": "alice",
        "email": "alice-the-admin@test.com",
        "date_password": "2018-07-30T11:41:14.000Z",
        "enabled": true,
        "admin": true
    }
}
```

<a name="managing-pep-proxies-and-iot-agents"></a>
# PEP Proxies と IoT Agents の管理

[以前のチュートリアル](https://github.com/Fiware/tutorials.Identity-Management)でユーザ・アカウントが作成されました。PEP Proxy などの人以外 (Non-human) のアクターも同じ方法で設定できます。各 PEP Proxy, IoT Agent または IoT センサのアカウントは、Keyrock 内のアプリケーションにリンクされたユーザ名とパスワードで構成されます。PEP Proxy アカウントと IoT Agent アカウントは、Keyrock GUI または REST API を使用して作成できます。

<a name="arrow_forward-video--wilma-pep-proxy-configuration"></a>
## :arrow_forward: ビデオ : Wilma PEP Proxy の設定

[![](http://img.youtube.com/vi/b4sYU78skrw/0.jpg)](https://www.youtube.com/watch?v=b4sYU78skrw "PEP Proxy Configuration")

上の画像をクリックすると、**Keyrock** を使用して、Wilma PEP Proxy を設定する方法のビデオが表示されます。

<a name="managing-pep-proxies-and-iot-agents---start-up"></a>
## PEP Proxies と IoT Agents の管理 - 起動

システムを起動するには、次のコマンドを実行します :

```console
./services orion
```

これにより、一連のユーザを持つ **Keyrock** を起動します。すでに 2つの既存のアプリケーションと、そのアプリケーションに関連付けられている既存の PEP Proxy アカウントがあります。

<a name="pep-proxy-crud-actions"></a>
## PEP Proxy CRUD アクション

#### GUI

ログインすると、ユーザは自分のアプリケーションに関連付けられた PEP Proxy を作成して更新することができます。

![](https://fiware.github.io/tutorials.PEP-Proxy/img/create-pep-proxy.png)

#### REST API

あるいは、`/v1/applications/{{application-id}}/pep_proxies` エンドポイント下の適切な HTTP 動詞 (POST, GET, PATCH および DELETE) に標準 CRUD アクションが割り当てられます。

<a name="create-a-pep-proxy"></a>
### PEP Proxy の作成

アプリケーション内で新しい PEP Proxy アカウントを作成するには、以前にログインした管理者のユーザから、`X-Auth-token` ヘッダ とともに `/v1/applications/{{application-id}}/pep_proxies` エンドポイントに POST リクエストを送信します。

#### :three: リクエスト :

```console
curl -iX POST \
  'http://localhost:3005/v1/applications/{{application-id}}/pep_proxies' \
  -H 'Content-Type: application/json' \
  -H 'X-Auth-token: {{X-Auth-token}}'
```

#### レスポンス :

アプリケーションに関連付けられている既存の PEP Proxy アカウントがない場合は、新しいアカウントが固有の `id` と `password` を付けて作成され、値がレスポンスに返されます。

```json
{
    "pep_proxy": {
        "id": "pep_proxy_ac80aaf8-0ac3-4bd8-8042-5e8f587679b7",
        "password": "pep_proxy_23d805e7-1b93-434a-8e69-0798dcdd6726"
    }
}
```

<a name="read-pep-proxy-details"></a>
### PEP Proxy の詳細を読み込む

`/v1/applications/{{application-id}}/pep_proxies` エンドポイントに GET リクエストを行うと、関連する PEP Proxy アカウントの詳細が返されます。`X-Auth-token` をヘッダに指定してしてください。

#### :four: リクエスト :

```console
curl -X GET \
  'http://localhost:3005/v1/applications/{{application-id}}/pep_proxies/' \
  -H 'X-Auth-token: {{X-Auth-token}}'
```

#### レスポンス : 

```json
{
    "pep_proxy": {
        "id": "pep_proxy_f84bcba2-3300-4f13-a4bb-7bdbd358b201",
        "oauth_client_id": "tutorial-dckr-site-0000-xpresswebapp"
    }
}
```

<a name="reset-password-of-a-pep-proxy"></a>
### PEP Proxy のパスワードをリセット

PEP Proxy アカウントのパスワードを更新するには、`/v1/applications/{{application-id}}/pep_proxies` エンドポイントへの PATCH リクエストを実行し、関連する PEP Proxy アカウントの詳細が返されます。`X-Auth-token` をヘッダに指定してしてください。

#### :five: リクエスト :

```console
curl -X PATCH \
  'http://localhost:3005/v1/applications/{{application-id}}/pep_proxies' \
  -H 'Content-Type: application/json' \
  -H 'X-Auth-token: {{X-Auth-token}}'
```

#### レスポンス :

レスポンスは、PEP Proxy アカウントの新しいパスワードを返します :

```json
{
    "new_password": "pep_proxy_2bc8996e-29bf-4195-ac39-d1116e429602"
}
```

<a name="delete-a-pep-proxy"></a>
### PEP Proxy の削除

既存の PEP Proxy アカウントは、`/v1/applications/{{application-id}}/pep_proxies` エンドポイントに DELETE リクエストを行うことで削除できます。`X-Auth-token` をヘッダに指定してしてください。

#### :six: リクエスト : 

```console
curl -X DELETE \
  'http://localhost:3005/v1/applications/{{application-id}}/pep_proxies' \
  -H 'Content-Type: application/json' \
  -H 'X-Auth-token: {{X-Auth-token}}'
```

<a name="iot-agent-crud-actions"></a>
## IoT Agent の CRUD アクション

#### GUI

PEP Proxy 作成と同様に、サイン・インして、ユーザはアプリケーションに関連付けられた IoT センサのアカウントを作成および更新できます。

![](https://fiware.github.io/tutorials.PEP-Proxy/img/create-iot-sensor.png)

#### REST API

あるいは、`/v1/applications/{{application-id}}/iot_agents` エンドポイント下の適切な HTTP動詞 (POST, GET, PATCH および DELETE) に標準 CRUD アクションが割り当てられます。

<a name="create-an-iot-agent"></a>
### IoT Agent を作成

アプリケーション内に新しい IoT Agent アカウントを作成するには、以前にログインした管理ユーザから、`X-Auth-token` とともに `/v1/applications/{{application-id}}/iot_agents` エンドポイントに POST リクエストを送信します。

#### :seven: リクエスト : 

```console
curl -X POST \
  'http://localhost:3005/v1/applications/{{application-id}}/iot_agents' \
  -H 'Content-Type: application/json' \
  -H 'X-Auth-token: {{X-Auth-token}}'
```

#### レスポンス :

固有の `id` と `password`を持つ新しいアカウントが作成され、値がレスポンスに返されます。

```json
{
    "iot": {
        "id": "iot_sensor_f1d0ca9e-b519-4a8d-b6ae-1246e443dd7e",
        "password": "iot_sensor_8775b438-6e66-4a6e-87c2-45c6525351ee"
    }
}
```

<a name="read-iot-agent-details"></a>
### IoT Agent の詳細を読み込む

GET リクエストを作成すると、`/v1/applications/{{application-id}}/iot_agents/{{iot-agent-id}}` エンドポイントは関連する IoT Agent アカウントの詳細を返します。`X-Auth-token` をヘッダに指定してしてください。

#### :eight: リクエスト : 

```console
curl -X GET \
  'http://localhost:3005/v1/applications/{{application-id}}/iot_agents/{{iot-agent-id}}' \
  -H 'X-Auth-token: {{X-Auth-token}}'
```

#### レスポンス : 

```json
{
    "iot": {
        "id": "iot_sensor_00000000-0000-0000-0000-000000000000",
        "oauth_client_id": "tutorial-dckr-site-0000-xpresswebapp"
    }
}
```

<a name="list-iot-agents"></a>
### IoT Agents の 一覧
`/v1/applications/{{application-id}}/iot_agents` エンドポイントに GET リクエストを実行することによって、アプリケーションに関連するすべての IoT Agents のリストを得ることができる。`X-Auth-token` をヘッダに指定してしてください。

#### :nine: リクエスト : 

```console
curl -X GET \
  'http://localhost:3005/v1/applications/{{application-id}}/iot_agents' \
  -H 'X-Auth-token: {{X-Auth-token}}'
```

#### レスポンス : 

```json
{
    "iots": [
        {
            "id": "iot_sensor_00000000-0000-0000-0000-000000000000"
        },
        {
            "id": "iot_sensor_c0fa0a77-ea9e-4a82-8118-b4d3c6b230b1"
        }
    ]
}
```

<a name="reset-password-of-an-iot-agent"></a>
### IoT Agent のパスワードをリセット

#### :one::zero: リクエスト :
 
個々の IoT Agent アカウントのパスワードを更新するには、`/v1/applications/{{application-id}}//iot_agents/{{iot-agent-id}}`  エンドポイントに PATCH リクエストを行います。`X-Auth-token` をヘッダに指定してしてください。

```console
curl -iX PATCH \
  'http://localhost:3005/v1/applications/{{application-id}}/iot_agents/{{iot-agent-id}}' \
  -H 'Content-Type: application/json' \
  -H 'X-Auth-token: {{X-Auth-token}}'
```

#### レスポンス :

レスポンスは、IoT Agent アカウントの新しいパスワードを返します。

```json
{
    "new_password": "iot_sensor_114cb79c-bf69-444a-82a1-e6e85187dacd"
}
```

<a name="delete-an-iot-agent"></a>
### IoT Agent を削除

既存の IoT Agent アカウントは、`/v1/applications/{{application-id}}/iot_agents/{{iot-agent-id}}` エンドポイントに DELETE リクエストを行うことで削除できます。`X-Auth-token` をヘッダに指定してしてください。

#### :one::one: リクエスト :

```console
curl -X DELETE \
  'http://localhost:3005/v1/applications/{{application-id}}/iot_agents/{{iot-agent-id}}' \
  -H 'X-Auth-token: {{X-Auth-token}}'
```
<a name="securing-the-orion-context-broker"></a>
# Orion Context Broker の保護

![](https://fiware.github.io/tutorials.PEP-Proxy/img/pep-proxy-orion.png)

<a name="securing-orion---pep-proxy-configuration"></a>
## Orion の保護 - PEP Proxy の設定

`orion-proxy` コンテナは FIWARE **Wilma** のインスタンスであるポート `1027` で待機し、Orion Context Broker が NGSI リクエストを待機しているデフォルトのポートである、`orion` の ポート `1026` にトラフィックを転送するように設定されます。

```yaml
  orion-proxy:
    image: fiware/pep-proxy
    container_name: fiware-orion-proxy
    hostname: orion-proxy
    networks:
      default:
        ipv4_address: 172.18.1.10
    depends_on:
      - keyrock
    ports:
      - "1027:1027"
    expose:
      - "1027"
    environment:
      - PEP_PROXY_APP_HOST=orion
      - PEP_PROXY_APP_PORT=1026
      - PEP_PROXY_PORT=1027
      - PEP_PROXY_IDM_HOST=keyrock
      - PEP_PROXY_HTTPS_ENABLED=false
      - PEP_PROXY_AUTH_ENABLED=false
      - PEP_PROXY_IDM_SSL_ENABLED=false
      - PEP_PROXY_IDM_PORT=3005
      - PEP_PROXY_APP_ID=tutorial-dckr-site-0000-xpresswebapp
      - PEP_PROXY_USERNAME=pep_proxy_00000000-0000-0000-0000-000000000000
      - PEP_PASSWORD=test
      - PEP_PROXY_PDP=idm
      - PEP_PROXY_MAGIC_KEY=1234
```

また、`PEP_PROXY_APP_ID` と `PEP_PROXY_USERNAME` は、通常、**Keyrock** のアプリケーションに新しいエントリを追加して取得しますが、このチュートリアルでは **MySQL** データベースに起動時のデータを入力することで事前定義されています。

`orion-proxy` コンテナは、単一ポートで待機しています : 

* PEP Proxyポート `1027` は、純粋にチュートリアルのアクセスのために公開されているため、cUrl または Postman は同じネットワークの一部ではなくても、**Wilma** インスタンスに直接リクエストできます。

| キー|値   |説明       |
|-----|-----|-----------|
| PEP_PROXY_APP_HOST |`orion` | PEP Proxy の背後にあるサービスのホスト名 |
| PEP_PROXY_APP_PORT |`1026` | PEP Proxy の背後にあるサービスのポート |
| PEP_PROXY_PORT |`1027` | PEP Proxy がリッスンしているポート |
| PEP_PROXY_IDM_HOST | `keyrock`| Keyrock Identity Manager のホスト名 |
| PEP_PROXY_HTTPS_ENABLED | `false`| PEP Proxy 自体が HTTPS で動作しているかどうか |
| PEP_PROXY_AUTH_ENABLED | `false`| PEP Proxy が認可をチェックしているかどうか |
| PEP_PROXY_IDM_SSL_ENABLED | `false`| Identity Manager が HTTPS で実行されているかどうか |
| PEP_PROXY_IDM_PORT | `3005`| Identity Manager インスタンスのポート |
| PEP_PROXY_APP_ID | `tutorial-dckr-site-0000-xpresswebapp`| |
| PEP_PROXY_USERNAME | `pep_proxy_00000000-0000-0000-0000-000000000000`| PEP Proxy のユーザ名 |
| PEP_PASSWORD | `test`| PEP Proxy のパスワード |
| PEP_PROXY_PDP | `idm`| Policy Decision Point を提供するサービスのタイプ |
| PEP_PROXY_MAGIC_KEY | `1234` | |

この例では、PEP Proxy は、レベル1 - *認証アクセス* をチェックし、レベル2 - *基本認可* または、レベル3 - *アドバンスド認可* をチェックしていません。

<a name="securing-orion---application-configuration"></a>
## Orion の保護 - アプリケーションの設定

チュートリアル・アプリケーションはすでに Keyrock に登録されており、プログラムではチュートリアル・アプリケーションは Orion Conext Broker の前にある Wilma PEP Proxy にリクエストを行います。すべてのリクエストに追加 の `access_token` ヘッダが含まれている必要があります。

```yaml
  tutorial-app:
    image: fiware/tutorials.context-provider
    hostname: tutorial-app
    container_name: tutorial-app
    depends_on:
        - orion-proxy
        - iot-agent
        - keyrock
    networks:
      default:
        ipv4_address: 172.18.1.7
        aliases:
          - iot-sensors
    expose:
        - "3000"
        - "3001"
    ports:
        - "3000:3000"
        - "3001:3001"
    environment:
        - "WEB_APP_PORT=3000"
        - "SECURE_ENDPOINTS=true"
        - "CONTEXT_BROKER=http://orion-proxy:1027/v2"
        - "KEYROCK_URL=http://localhost"
        - "KEYROCK_IP_ADDRESS=http://172.18.1.5"
        - "KEYROCK_PORT=3005"
        - "KEYROCK_CLIENT_ID=tutorial-dckr-site-0000-xpresswebapp"
        - "KEYROCK_CLIENT_SECRET=tutorial-dckr-site-0000-clientsecret"
        - "CALLBACK_URL=http://localhost:3000/login"
```

すべての `tutorial` コンテナ設定は、以前のチュートリアルで説明されています。ただし、以前のすべてのチュートリアルで示されているように、デフォルトのポート `1026' で **Orion** に直接アクセスするのではなく、すべての Context Broker のトラフィックが `orion-proxy` のポート `1027' に送信されるように、重要な変更が必要です。ここでは、関連する設定について詳しく説明します。

| キー| 値  | 説明      |
|-----|-----|-----------|
|WEB_APP_PORT|`3000`| ログイン画面等を表示する web-app が使用するポート |
|KEYROCK_URL|`http://localhost`| ユーザを転送するときのリダイレクトに使用される **Keyrock** Web フロント・エンド自体の URL |
|KEYROCK_IP_ADDRESS|`http://172.18.1.5`| **Keyrock** 通信の URL |
|KEYROCK_PORT|`3005` | **Keyrock** がリッスンしているポート |
|KEYROCK_CLIENT_ID|`tutorial-dckr-site-0000-xpresswebapp`| このアプリケーションで **Keyrock** によって定義されたクライアント ID |
|KEYROCK_CLIENT_SECRET|`tutorial-dckr-site-0000-clientsecret`| このアプリケーションで **Keyrock** によって定義されたクライアントのシークレット |
|CALLBACK_URL|`http://localhost:3000/login`| チャレンジが成功したときに **Keyrock** が使用するコールバック URL |

<a name="securing-orion---start-up"></a>
## Orion の保護 - 起動
**Orion** へのアクセスを保護する PEP Proxy を使用してシステムを起動するには、次のコマンドを実行します :

```console
./services orion
```

<a name="arrow_forward-video--securing-a-rest-api"></a>
### :arrow_forward: ビデオ : REST API を保護

[![](http://img.youtube.com/vi/coxFQEY0_So/0.jpg)](https://www.youtube.com/watch?v=coxFQEY0_So "Securing a REST API")

上記の画像をクリックすると、Wilma PEP Proxy を使用して REST API を保護するためのビデオが表示されます

<a name="user-logs-in-to-the-application-using-the-rest-api"></a>
## ユーザが REST API を使用してアプリケーションへのログイン

<a name="pep-proxy---no-access-to-orion-without-an-access-token"></a>
### PEP Proxy - アクセス・トークンのない Orion へのアクセス拒否

セキュアなアクセスは、セキュアなサービスへのすべてのリクエストが PEP Proxy を介して間接的に行われるようにすることで保証されます。この場合、PEP Proxy は Context Broker の前にあります。リクエストには、`X-Auth-Token` を含める必要があります。有効なトークンを提示できないと、アクセスが拒否されます。

#### :one::two: リクエスト

以下のようにアクセス・トークンなしで PEP Proxy へのリクエストが行われた場合は :

```console
curl -X GET \
  http://localhost:1027/v2/entities/urn:ngsi-ld:Store:001?options=keyValues
```

#### レスポンス

レスポンスは、以下の説明とともに **401 Unauthorized** エラーコードになります :

```
Auth-token not found in request header
```

<a name="keyrock---user-obtains-an-access-token"></a>
### Keyrock - ユーザによるアクセス・トークンの取得

#### :one::three: リクエスト

ユーザ・クレデンシャルのフローを使用してアプリケーションにログインするには、`oauth2/token` エンドポイントを使用して、`grant_type=password` とともに、**Keyrock** に POSTリクエストを送信します。例えば、Admin Alice としてログインするには : 

```console
curl -iX POST \
  'http://localhost:3005/oauth2/token' \
  -H 'Accept: application/json' \
  -H 'Authorization: Basic dHV0b3JpYWwtZGNrci1zaXRlLTAwMDAteHByZXNzd2ViYXBwOnR1dG9yaWFsLWRja3Itc2l0ZS0wMDAwLWNsaWVudHNlY3JldA==' \
  -H 'Content-Type: application/x-www-form-urlencoded' \
  --data "username=alice-the-admin@test.com&password=test&grant_type=password"
```

#### レスポンス

レスポンスは、ユーザを識別するためのアクセス・コードを返します :

```json
{
    "access_token": "a7e22dfe2bd7d883c8621b9eb50797a7f126eeab",
    "token_type": "Bearer",
    "expires_in": 3599,
    "refresh_token": "05e386edd9f95ed0e599c5004db8573e86dff874"
}
```

これは、http:/localhost に、チュートリアル・アプリケーションを入れて、OAuth2 グラントのいずれかを使用してログインすることによっても行うことができます。ログインに成功すると、アクセス・トークンが返されます。

<a name="pep-proxy---accessing-orion-with-an-access-token"></a>
### PEP Proxy - アクセス・トークンを使用して Orion にアクセス

示されているように、`X-Auth-Token` ヘッダに有効なアクセス・トークンを含めて PEP Proxy へのリクエストが行われた場合、そのリクエストは許可され、PEP Proxy の背後にあるサービス (この場合はOrion Context Broker) が期待通りにデータを返します。

#### :one::four: リクエスト

```console
curl -X GET \
  http://localhost:1027/v2/entities/urn:ngsi-ld:Store:001?options=keyValues \
  -H 'X-Auth-Token: {{X-Access-token}}'
```

#### レスポンス : 

```json
{
    "id": "urn:ngsi-ld:Store:001",
    "type": "Store",
    "address": {
        "streetAddress": "Bornholmer Straße 65",
        "addressRegion": "Berlin",
        "addressLocality": "Prenzlauer Berg",
        "postalCode": "10439"
    },
    "location": {
        "type": "Point",
        "coordinates": [
            13.3986,
            52.5547
        ]
    },
    "name": "Bösebrücke Einkauf"
}
```

<a name="securing-orion---sample-code"></a>
## Orion の保護 - サンプル・コード

ユーザがユーザ・クレデンシャル・グラントを使用してアプリケーションにログインすると、そのユーザを識別する `access_token` を取得します。`access_token` は、セッションに格納されます :

```javascript
function userCredentialGrant(req, res){
    debug('userCredentialGrant');

    const email = req.body.email;
    const password = req.body.password;

    oa.getOAuthPasswordCredentials(email, password)
    .then(results => {
        req.session.access_token =  results.access_token;
        return;
    })
}
```

後続のリクエストごとに、`access_token` は、`X-Auth-Token` ヘッダに設定されます

```javascript
function setAuthHeaders(req){
  const headers = {};
  if (req.session.access_token) {
    headers['X-Auth-Token'] = req.session.access_token;
  }
  return headers;
}
```

たとえば、アイテムを購入するときに、2つのリクエストが行われた場合、各リクエストに同じ `X-Auth-Token` ヘッダを追加する必要があります。そのため、ユーザを識別してアクセスを許可することができます。

```javascript
async function buyItem(req, res) {

  const inventory = await retrieveEntity(req.params.inventoryId, {
    options: 'keyValues',
    type: 'InventoryItem',
  }, setAuthHeaders(req));
  const count = inventory.shelfCount - 1;

  await updateExistingEntityAttributes(
    req.params.inventoryId,
    { shelfCount: { type: 'Integer', value: count } },
    {
      type: 'InventoryItem',
    }, setAuthHeaders(req)
  );
  res.redirect(`/app/store/${inventory.refStore}/till`);
}
```

<a name="securing-an-iot-agent"></a>
# IoT Agent の保護

![](https://fiware.github.io/tutorials.PEP-Proxy/img/pep-proxy-iot-agent.png)

<a name="securing-an-iot-agent---pep-proxy-configuration"></a>
## IoT Agent の保護 - PEP Proxy の設定

`iot-agent-proxy`  コンテナは FIWARE  **Wilma**  のインスタンスである、ポート `7897` で待機し、`iot-agent` のポート `7896` にトラフィックを転送するように設定され これは、Ultralight エージェントが、HTTP リクエストのために待機しているデフォルトのポートです。

```yaml
  iot-agent-proxy:
    image: fiware/pep-proxy
    container_name: fiware-iot-agent-proxy
    hostname: iot-agent-proxy
    networks:
      default:
        ipv4_address: 172.18.1.11
    depends_on:
      - keyrock
    ports:
      - "7897:7897"
    expose:
      - "7897"
    environment:
      - PEP_PROXY_APP_HOST=iot-agent
      - PEP_PROXY_APP_PORT=7896
      - PEP_PROXY_PORT=7897
      - PEP_PROXY_IDM_HOST=keyrock
      - PEP_PROXY_HTTPS_ENABLED=false
      - PEP_PROXY_AUTH_ENABLED=false
      - PEP_PROXY_IDM_SSL_ENABLED=false
      - PEP_PROXY_IDM_PORT=3005
      - PEP_PROXY_APP_ID=tutorial-dckr-site-0000-xpresswebapp
      - PEP_PROXY_USERNAME=pep_proxy_00000000-0000-0000-0000-000000000000
      - PEP_PASSWORD=test
      - PEP_PROXY_PDP=idm
      - PEP_PROXY_MAGIC_KEY=1234
```

`PEP_PROXY_APP_ID` および `PEP_PROXY_USERNAME` は、通常、**Keyrock** のアプリケーションに新しいエントリを追加することで得られます。ただし、このチュートリアルでは、**MySQL** データベースに起動時のデータを入力することで事前定義されています。

`iot-agent-proxy` コンテナは、単一ポートで待機しています :

* PEP Proxy ポート `7897` は、チュートリアル・アクセスのためだけに公開されているため、cUrl または Postman は、同じネットワークの一部ではなくても、この **Wilma** インスタンスに直接リクエストできます。

|キー |値   |説明       |
|-----|-----|-----------|
| PEP_PROXY_APP_HOST | `iot-agent`| PEP Proxy の背後にあるサービスのホスト名 |
| PEP_PROXY_APP_PORT | `7896`| PEP Proxy の背後にあるサービスのポート |
| PEP_PROXY_PORT | `7897`| PEP Proxy がリッスンしているポート |
| PEP_PROXY_IDM_HOST | `keyrock`| Identity Manager のホスト名 |
| PEP_PROXY_HTTPS_ENABLED | `false`| PEP Proxy が HTTPS で動作しているかどうか |
| PEP_PROXY_AUTH_ENABLED | `false`|  PEP Proxy が認可をチェックしているかどうか |
| PEP_PROXY_IDM_SSL_ENABLED | `false`|  Identity Manager が HTTPS で実行されているかどうか |
| PEP_PROXY_IDM_PORT | `3005`| Identity Manager インスタンスのポート |
| PEP_PROXY_APP_ID | `tutorial-dckr-site-0000-xpresswebapp`| |
| PEP_PROXY_USERNAME | `pep_proxy_00000000-0000-0000-0000-000000000000`| PEP Proxy のユーザ名 |
| PEP_PASSWORD | `test`| PEP Proxy のパスワード |
| PEP_PROXY_PDP | `idm`| Policy Decision Point を提供するサービスのタイプ |
| PEP_PROXY_MAGIC_KEY | `1234` | |

この例では、PEP Proxy は、レベル1 - *認証アクセス* をチェックし、レベル2 - *基本認可* または、レベル3 - *アドバンスド認可* をチェックしていません。

<a name="securing-an-iot-agent---application-configuration"></a>
## IoT Agent の保護 - アプリケーションの設定

このチュートリアル・アプリケーションは、ダミー IoT センサのデータを提供する役割も果たします。IoT センサは、Ultralight 構文でコマンドと測定値を含む HTTP リクエストを出しています。IoT センサのユーザ名とパスワードはすでに **Keyrock** に登録されていますが、プログラムごとに OAuth2 アクセス・トークンを取得し、**IoT Agent** の前にある2番目の **Wilma** PEP Proxy にリクエストします。

```yaml
  tutorial-app:
    image: fiware/tutorials.context-provider
    hostname: tutorial-app
    container_name: tutorial-app
    depends_on:
        - orion-proxy
        - iot-agent-proxy
        - keyrock
    networks:
      default:
        ipv4_address: 172.18.1.7
        aliases:
          - iot-sensors
    expose:
        - "3000"
        - "3001"
    ports:
        - "3000:3000"
        - "3001:3001"
    environment:
        - "IOTA_HTTP_HOST=iot-agent-proxy"
        - "IOTA_HTTP_PORT=7897"
        - "DUMMY_DEVICES_PORT=3001" # Port used by the dummy IoT devices to receive commands
        - "DUMMY_DEVICES_TRANSPORT=HTTP" # Default transport used by dummy IoT devices
        - "DUMMY_DEVICES_API_KEY=4jggokgpepnvsb2uv4s40d59ov"
        - "DUMMY_DEVICES_USER=iot_sensor_00000000-0000-0000-0000-000000000000"
        - "DUMMY_DEVICES_PASSWORD=test"
```

`tutorial` コンテナは、ダミー Ultralight センサをホストします。以前のすべてのチュートリアルに示されているように、**IoT Agent** にポート `7896` で直接アクセスするのではなく、すべてのトラフィックが、`iot-agent-proxy` の ポート `7897` に転送されます。関連する `tutorial` コンテナの設定のほとんどは、以前のチュートリアルで説明されており、`DUMMY_DEVICES_USER` および  `DUMMY_DEVICES_PASSWORD` は新しい追加項目です。

| キー| 値  | 説明      |
|-----|-----|-----------|
|IOTA_HTTP_HOST|`iot-agent-proxy`| Ultra Light 2.0 用 IoT Agent を保護する Wilma PEP Proxy のホスト名 |
|IOTA_HTTP_PORT|`7896` | IoT Agent を保護する Wilma PEP Proxy がリスンしているポート |
|DUMMY_DEVICES_PORT|`3001`| ダミー IoT デバイスによって使用されるポート |
|DUMMY_DEVICES_TRANSPORT|`HTTP`| ダミー IoT デバイスによって使用されるデフォルト転送 |
|DUMMY_DEVICES_API_KEY|`4jggokgpepnvsb2uv4s40d59ov`| UltraLight インタラクションに使用されるランダムなセキュリティキー - デバイスと IoT Agent 間のインタラクションの完全性を保証します |
|DUMMY_DEVICES_USER|`iot_sensor_00000000-0000-0000-0000-000000000000` | **Keyrock** のデバイスに割り当てられたユーザ名 |
|DUMMY_DEVICES_PASSWORD|`test` | **Keyrock** のデバイスに割り当てられたパスワード |
	
`DUMMY_DEVICES_USER` および `DUMMY_DEVICES_PASSWORD` は、通常、**Keyrock** のアプリケーションに新しいエントリを追加することで得られますが、このチュートリアルでは **MySQL** データベースに起動時のデータを入力することで事前定義されています。

<a name="securing-iot-agent---start-up"></a>
## IoT Agent のセキュリティ確保 - 起動

**Orion** と **IoT Agent** の両方へのアクセスを保護する PEP Proxies を使用してシステムを起動するには、次のコマンドを実行します :

```console
./services iot-agent
```

<a name="iot-sensor-logs-in-to-the-application-using-the-rest-api"></a>
## IoT センサが REST API を使用してアプリケーションにログイン

<a name="keyrock---iot-sensor-obtains-an-access-token"></a>
### Keyrock - IoT センサによるアクセス・トークンの取得

IoT センサとしてのログインは、ユーザと同じユーザ・クレデンシャル・フローに従います。ログインしてパスワード  `test` でセンサ `iot_sensor_00000000-0000-0000-0000-000000000000` を特定するには、`grant_type=password` で `oauth2/token` エンドポイントを使って **Keyrock** に POST リクエストを送ります：

#### :one::five: リクエスト :

```console
curl -iX POST \
  'http://localhost:3005/oauth2/token' \
  -H 'Accept: application/json' \
  -H 'Authorization: Basic dHV0b3JpYWwtZGNrci1zaXRlLTAwMDAteHByZXNzd2ViYXBwOnR1dG9yaWFsLWRja3Itc2l0ZS0wMDAwLWNsaWVudHNlY3JldA==' \
  -H 'Content-Type: application/x-www-form-urlencoded' \
  --data "username=iot_sensor_00000000-0000-0000-0000-000000000000&password=test&grant_type=password"
```

#### レスポンス

レスポンスは、デバイスを識別するためのアクセス・コードを返します :

```json
{
    "access_token": "a7e22dfe2bd7d883c8621b9eb50797a7f126eeab",
    "token_type": "Bearer",
    "expires_in": 3599,
    "refresh_token": "05e386edd9f95ed0e599c5004db8573e86dff874"
}
```

<a name="pep-proxy---accessing-iot-agent-with-an-access-token"></a>
### PEP Proxy - アクセス・トークンを使用して IoT Agent にアクセス

この例では、デバイス `motion001` からの保護されたリクエストをシミュレートします。

Ultralight IoT Agent の前にある PEP Proxy への POST リクエストは、事前にプロビジョニングされたリソース `iot/d` エンドポイントを識別し、デバイス `motion001` の測定値を渡します。`X-Auth-Token` ヘッダを追加すると、リクエスト元が Keyrock に登録されていると識別され、測定が IoT Agent 自体に正常に渡されます。

#### リクエスト :

```console
curl -X POST \
  'http://localhost:7897/iot/d?k=4jggokgpepnvsb2uv4s40d59ov&i=motion001' \
  -H 'X-Auth-Token: {{X-Access-token}}' \
  -d 'c|1'
```

<a name="securing-an-iot-agent----sample-code"></a>
## IoT Agent の保護 - サンプル・コード

IoT センサが起動すると、他のユーザと同様にログインしてアクセス・トークンを取得する必要があります :

```javascript
const DUMMY_DEVICE_HTTP_HEADERS = { 'Content-Type': 'text/plain' };
```
```javascript
function initSecureDevices(){
    Security.oa.getOAuthPasswordCredentials(process.env.DUMMY_DEVICES_USER, process.env.DUMMY_DEVICES_PASSWORD)
    .then(results => {
        DUMMY_DEVICE_HTTP_HEADERS['X-Auth-Token'] = results.access_token;
        return;
    })
    .catch(error => {
        debug(error);
        return;
    });
}
```

その後、各 HTTP リクエストには、IoT センサを識別するリクエストに `X-Auth-Token` ヘッダを含みます :

```javascript
const options = { method: 'POST',
  url: UL_URL,
  qs: { k: UL_API_KEY, i: deviceId },
  headers: DUMMY_DEVICE_HTTP_HEADERS,
  body: state };

request(options,  (error) => {
  if (error){
    debug( debugText +  " " + error.code)
  }
});
```

---

## License

[MIT](LICENSE) © FIWARE Foundation e.V.
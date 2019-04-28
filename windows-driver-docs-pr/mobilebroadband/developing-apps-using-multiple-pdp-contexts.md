---
title: 複数の PDP コンテキストを使用したアプリの開発
description: 複数の PDP コンテキストを使用したアプリの開発
ms.assetid: 6a977a69-397d-4922-890d-1810dd54dff4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5ae541384047ff1741fa50258360dc7c4fea8ed
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380305"
---
# <a name="developing-apps-using-multiple-pdp-contexts"></a>複数の PDP コンテキストを使用したアプリの開発


パケット データ プロトコル (PDP) コンテキストでは、どのデバイスとモバイルのネットワーク パケットを交換できます IP パケット データ接続を提供します。 3 gpp の標準に従って、デバイスでは、複数の PDP コンテキストが、一度にアクティブにすることができます。 Windows 8.1 および Windows 10 では、複数の PDP コンテキストは、サポートされ、アプリ Windows 8 でサポートされていた PDP コンテキストをモバイル ネットワーク、インターネットとする特別な PDP コンテキスト経由で通信を有効に。 この機能を使用すると、Windows で差別化されたエクスペリエンスと革新的なサービスを作成します。 高品質な VOIP とビデオを顧客のエクスペリエンスのストリーミングを開発するアプリの開発者と提携することができますも。

複数の PDP コンテキストは、Windows 8.1 および Windows 10 で動作を示す図を次に示します。

![図 1](images/mb-pdp-fig1.jpg)

詳細については、複数の PDP コンテキストはこのトピックでは、次のセクションを使用します。

-   [主なシナリオ](#key-scenarios)

-   [モバイル ブロード バンド アプリ](#mobile-broadband-apps)

-   [モバイル ブロード バンド デバイス](#mobile-broadband-devices)

## <a name="key-scenarios"></a>主なシナリオ


Premium サービスを有効にするのには、複数の PDP コンテキストを使用できます。

-   **課金を差別化された**– 複数の PDP コンテキストを使用して、データや課金の制限を変更できます。 たとえば、Contoso は、お客様のデータのバックアップ アプリを開発した携帯電話会社です。 モバイル オペレーターの場合は、Contoso は複数の PDP コンテキストを作成し、premium サブスクライバー向けのアプリを無料で使用できるように可能性があります。 その他のすべてのサブスクライバーは、それを使用するとは別に課金されます。

-   **Rich Communication Services** – 強化された電話帳などのリッチな通信サービスを提供する GSM アソシエーションによって作成されたグローバル initiative メッセージングが向上し、呼び出し元に情報を追加します。 Rich Communication Services は、演算子とプランで高品質で革新的なコミュニケーション サービスを配信する既存のアセット、機能を使用する新しい方法をモバイルでの相互運用性を提供します。

-   **接続を勧める**– これにより、データの月間使用量に対して移動しなくてもユーザーを特定の種類のコンテンツ。 コンテンツ プロバイダーは、携帯電話会社、収益の共有の処理を行うには、直接、お支払いがへの払い戻しを配置またはその他のいくつかのビジネス設定です。

-   **個人用ホット スポット**– モバイル演算子によって、接続は、個人用のホット スポットとして使用されているときに別の料金が課金されます。 複数の PDP コンテキストは、2 つを区別するために使用できます。

## <a name="mobile-broadband-apps"></a>モバイル ブロード バンド アプリ


UWP のモバイル ブロード バンド アプリでは、特別な PDP コンテキストをアクティブ化し、データのトラフィックをルーティングする規則を指定する複数の PDP コンテキストを利用できます。 これらのアプリでは、特定の送信先のまたはすべてのデータ トラフィックのルールを作成できます。

モバイル ブロード バンド アプリは、ネットワークとデータを交換する必要がある、使用可能な接続されたネットワークを確認します。 モバイル ブロード バンド アプリにこれらのネットワークのいずれかの特別な規則がある場合、特別な PDP コンテキストを開く、接続マネージャー API を使用します。 この接続が成功した場合は、PDP コンテキストはこの接続のルーティング規則を提供し、ネットワーク Api を使用してデータを転送します。 モバイル ブロード バンド アプリはこの手順を繰り返しますを受信した場合、 [ **NetworkStatusChanged** ](https://msdn.microsoft.com/library/windows/apps/br207299)イベントをすべての接続が変更されたかどうかと、新しい接続の PDP コンテキストを開く必要があるかどうかを参照してください。

![図 2](images/mb-pdp-fig2.jpg)

### <a name="span-idnetworkingapisspanspan-idnetworkingapisspanspan-idnetworkingapisspannetworking-apis"></a><span id="Networking_APIs"></span><span id="networking_apis"></span><span id="NETWORKING_APIS"></span>ネットワーク Api

特別な PDP コンテキストを使用してデータを送信するため、Microsoft Store アプリがネットワーク データ転送に使用する Api に基づく別のロジックを使用する必要があります。

### <a name="span-idhttp-basedapisspanspan-idhttp-basedapisspanspan-idhttp-basedapisspanhttp-based-apis"></a><span id="HTTP-based_APIs"></span><span id="http-based_apis"></span><span id="HTTP-BASED_APIS"></span>HTTP ベースの Api

HTTP ベースの Api など[ **XMLHTTPRequest**](https://msdn.microsoft.com/library/windows/apps/br229787)、 [IXHR2](https://msdn.microsoft.com/library/windows/desktop/hh831163)、 [ **Windows.Web.Syndication**](https://msdn.microsoft.com/library/windows/apps/br243632)と[ **Windows.Web.AtomPub**](https://msdn.microsoft.com/library/windows/apps/br210609)、Api は、JQuery など、Windows HTTP プロトコルに基づくと、 [ **Windows.Web.Http**](https://msdn.microsoft.com/library/windows/apps/dn279692)、特定のインターフェイスにバインドする機能はありません。 これらの Api の場合、Windows では、ポリシーを使用して、特別な PDP コンテキストへのデータのルーティングを処理します。 特別な PDP コンテキストがアクティブ化されると、アプリは、変換先および特別な PDP コンテキストに基づくルーティングの規則を指定できます。 宛先は、ドメイン名または video.fabrikam.com などの IP アドレスを指定できます。 contoso.com または 123.23.34.333 します。 ルーティング規則を指定するには、アプリで使用する場合、上記の HTTP Api のデータを転送する Windows は送信データ ルーティング ルールに基づいて特殊な PDP コンテキストにします。 アプリのデータ転送が完了するとは、特別な PDP コンテキストを切断する必要があり、ルートのポリシーを削除します。

**注**  
[**バック グラウンド転送 Api** ](https://msdn.microsoft.com/library/windows/apps/br207242)と[HTTP クライアント (C#) Api](https://msdn.microsoft.com/library/windows/apps/system.net.http.httpclient.aspx)ルーティング ポリシーを使用することはできません。

 

![図 3](images/mb-pdp-fig4.jpg)

### <a name="span-idsocket-basedapisspanspan-idsocket-basedapisspanspan-idsocket-basedapisspansocket-based-apis"></a><span id="Socket-based_APIs"></span><span id="socket-based_apis"></span><span id="SOCKET-BASED_APIS"></span>ソケット ベースの Api

ソケット ベースの Api で使用できる、 [ **Windows.Networking.Sockets** ](https://msdn.microsoft.com/library/windows/apps/br226960) TCP、UDP、およびストリームのソケットなどの名前空間は、特定のインターフェイスにバインドするためのメカニズムを提供します。 アプリでは、ソケット Api を使用する場合は、特別な PDP コンテキストへのルーティングのデータの特定のインターフェイスにバインドする必要があります。 特別な PDP コンテキストがアクティブ化される、 [ **AcquireConnectionAsync** ](https://msdn.microsoft.com/library/windows/apps/dn266103) API アプリにインターフェイスの情報を提供します。 この情報を使用して特定のインターフェイスにバインドし、データ転送を開始できです。

![図 4](images/mb-pdp-fig3.jpg)

### <a name="span-idmultiplepdpcontentapiinfospanspan-idmultiplepdpcontentapiinfospanspan-idmultiplepdpcontentapiinfospanmultiple-pdp-content-api-info"></a><span id="Multiple_PDP_content_API_info"></span><span id="multiple_pdp_content_api_info"></span><span id="MULTIPLE_PDP_CONTENT_API_INFO"></span>複数の PDP コンテンツ API 情報

Windows 8.1 および Windows 10 では、複数の PDP コンテキストをサポートするために、次の Api が追加します。

-   [**CellularApnContext** ](https://msdn.microsoft.com/library/windows/apps/dn266056)このクラスには、ネットワーク上のアクセス ポイントを指定するためのプロパティが含まれています。 **CellularApnContext**でオブジェクトが渡される、 [ **AcquireConnectionAsync** ](https://msdn.microsoft.com/library/windows/apps/dn266103)呼び出しを特定のアクセス ポイントへの接続を確立します。

-   [**ConnectivityManager::AcquireConnectionAsync** ](https://msdn.microsoft.com/library/windows/apps/dn266103)この API は、指定のアクセス ポイント名 (APN) または PDP コンテキストの新しい接続をアクティブにします。 この非同期メソッドは、適切な構成情報と、特定の APN または PDP コンテキストへの接続を要求するアプリを使用します。 特別な APN をアクティブにした後は、Windows とアプリに新しい仮想インターフェイスとして表示されます。

-   [**ConnectivityManager::AddHttpRoutePolicy** ](https://msdn.microsoft.com/library/windows/apps/dn266105)このメソッドは、ルーティングのデータに特別な PDP コンテキスト スタックの HTTP トラフィックで使用するポリシーを追加します。 アプリでは、ドメイン名と IP アドレス、および特殊な PDP コンテキストのプロファイルなどの変換先に基づくポリシーを指定できます。 Windows の HTTP スタックは、アプリがポリシーを作成したら、データを特別な PDP コンテキストにルーティングするため、ポリシーを使用します。

-   [**ConnectivityManager::RemoveHttpRoutePolicy** ](https://msdn.microsoft.com/library/windows/apps/dn266106)このメソッドは、以前に追加された HTTP ルーティング ポリシーを削除します。

次のコードは、HTTP ベースのデータ転送にこれらの Api を使用する方法を示しています。

``` syntax
var connectivity = Windows.Networking.Connectivity;
var currentRoutePolicy = null;
var currentConnectionSession = null;

//  Create PDP context/APN data 
var apnContext                      =   new connectivity.CellularApnContext();
apnContext.accessName               =   "myAPN.com";
apnContext.userName                 =   "APNusername"
apnContext.password                 =   "APNPassword";
apnContext.isCompressionEnabled     =   false;
apnContext.authenticationType       =   connectivity.CellularApnAuthenticationType.none;

//  Request a connection to Windows
connectivity.ConnectivityManager.acquireConnectionAsync(apnContext).done(onConnectionSucceeded, onConnectionFailed);


//  On successful Activation of APN, Windows returns a ConnectionSession object that encapsulates the new connection profile

function onConnectionSucceeded(result
{
    // keep the connectionSession in scope
    currentConnectionSession= result;

    //  create a route policy for the new connection
    currentRoutePolicy = new connectivity.routePolicy(currentConnectionSession.ConnectionProfile, new hostName("video.mydomain.com"),Windows.Networking.DomainNameType.suffix);

    //  indicate the new route policy to the Http stack
    connectivity.connectivityManager.addHttpRoutePolicy(currentRoutePolicy);

    // Backend data interaction with appropriate HTTP APIs (IXHR, Open IFrame etc.)


    // After completing the data transfer remove the Route Policy
    connectivity.connectivityManager.removeHttpRoutePolicy(currentRoutePolicy);
    currentRoutePolicy = null;

    // Disconnect the PDP Context to free up resources
    currentConnectionSession.close();
}
```

次のコードでは、ソケット ベースのデータ転送にこれらの Api を使用する方法を示します。

``` syntax
// Connect to Special PDP Context
var connectivity = Windows.Networking.Connectivity;
var currentRoutePolicy = null;
var currentConnectionSession = null;

// Create PDP Context/APN Data 
var apnContext = new connectivity.CellularApnContext();

// Create PDP context/APN data 
var apnContext = new connectivity.CellularApnContext();
apnContext.accessName = "myAPN.com";
apnContext.userName = "APNusername"
apnContext.password = "APNPassword";
apnContext.isCompressionEnabled = false;
apnContext.authenticationType = connectivity.CellularApnAuthenticationType.none;

// Request the connection to Windows
connectivity.ConnectivityManager.acquireConnectionAsync(apnContext).done(onConnectionSucceeded, onConnectionFailed);

// On successful activation of an APN, Windows returns a ConnectionSession object that encapsulates the new connection profile
                function onConnectionSucceeded(result) {

// keep the connectionSession in scope
currentConnectionSession = result;

var socket = new Windows.Networking.Sockets.StreamSocket();
var hostName = new Windows.Networking.HostName("www.contoso.com");
var portNumber = "1234";

// Bind the socket to new Special PDP Context Connection
socket.connectAsync(hostName, portNumber, SocketProtectionLevel.PlainSocket, currentConnectionSession.connectionProfile.networkAdapter).done(onSocketConnectionSucceeded, onSocketConnectionFailed);

function onSocketConnectionSucceeded(result)
{
    // Start transferring data using socket APIs

}

// Closing the sockets
socket.close();

// Disconnect the PDP Context to free up resources
currentConnectionSession.close();
```

アプリを処理する必要があります[ **NetworkStatusChanged** ](https://msdn.microsoft.com/library/windows/apps/br207299)特別な PDP コンテキスト接続でネットワーク移行を処理するイベントです。

### <a name="span-idscenariopremiummobilebroadbandappprovidesfreedataaccessusingspecialapnspanspan-idscenariopremiummobilebroadbandappprovidesfreedataaccessusingspecialapnspanspan-idscenariopremiummobilebroadbandappprovidesfreedataaccessusingspecialapnspanscenario-premium-mobile-broadband-app-provides-free-data-access-using-special-apn"></a><span id="Scenario__Premium_mobile_broadband_app_provides_free_data_access_using_special_APN"></span><span id="scenario__premium_mobile_broadband_app_provides_free_data_access_using_special_apn"></span><span id="SCENARIO__PREMIUM_MOBILE_BROADBAND_APP_PROVIDES_FREE_DATA_ACCESS_USING_SPECIAL_APN"></span>シナリオ:Premium モバイル ブロード バンド アプリは、特別な APN を使用して無料のデータ アクセスを提供します。

このシナリオでは、モバイル ブロード バンド アプリは、特別な PDP コンテキストを使用して無料のデータ アクセスを提供します。 アプリでは、無料、または特定のオペレーターのネットワークに接続されている場合、特別な APN を使用して、Wi-fi ネットワークなどの接続されたネットワークか使用します。 次のサンプル コードは、無料のネットワークが接続されていない場合は、特別な PDP コンテキストでデータを転送するため、アプリが複数の PDP コンテキストの Api を使用する方法を示しています。

``` syntax
// Reference the namespace
var connectivity = Windows.Networking.Connectivity;

// Current route policy
var currentRoutePolicy = null;
var currentConnectionSession = null;

function onLoad()
{
  // Register for network status change
  connectivity.networkInformation.addEventListener("networkstatuschanged", OnNetworkStatusChange);
  // Process the current status
  handleNetworkChange();
}

//  Handle newtork status changes
function onNetworkStatusChange()
{
  HandleNetworkChange();
}

// On network status change:
//  if there is no connectionPolicy, evaluate a new one
//  if there is a current connectionPolicy ==> verify it is still valid 
//      evaluate a new one if the current connectionPolicy is not valid 
function handleNetworkChange()
{
  if (isCurrentPolicyStillValid())
  {
    //the current policy is still valid.
    return;
  }

  //  No policy or current policy is not good anymore
  //  cleanup any previous configuration
  if (currentRoutePolicy)
  {
    connectivity.ConnectivityManager.removeHttpRoutePolicy(currentRoutePolicy);
    currentRoutePolicy = null;
  }

  //  if a different APN was connected, disconnect it to free up resources
  if (connectionConnectionSession != null)
  {
    connectionConnectionSession.close();
    connectionConnectionSession = null;
  }

  // evaluate connection policy
  startEvaluateConnectionPolicy();
}

//  evaluate if the current connectionPolicy is still valid
function isCurrentPolicyStillValid()
{
  if (null != currentRoutePolicy)
  {
    // a policy is currently in place, let's verify if it is still valid
    var currentProfile = currentRoutePolicy.connectionProfile();
    if (NetworkConnectivityLevel.none != currentProfile.GetNetworkConnectivityLevel())
    {
      // current policy is still good. bail out
      return true;
    }
  }
  return false;
}

// starts the evaluation of a new connection policy
function startEvaluateConnectionPolicy()
{
  // first try to get a free network if it is available
  var queryFilter = new connectivity.connectionProfileFilter();
  queryFilter.networkCostType = connectivity.networkCostType.unrestricted;
  queryFilter.isConnected = true;

  connectivity.networkInformation.findConnectionProfilesAsync(queryFilter).done(onSuccess, onFailure);
}

//  Succesfully retrieved at least one free connection profile
function onSuccess(results)
{
  if(results.count > 0)
  {
  //  Enfore the route to the http stack
  enforceHttpRoutePolicy(results[0]);

  // Backend data interaction with appropriate APIs(Open IFrame etc.)

  }
  else
  {
    onFailure();
  }
}

//  there are no free networks available at this time
function onFailure()
{
  //  create a request to connect a specific APN on the network
  // no free network available, connect
  var apnContext                      =   new connectivity.CellularApnContext();
  apnContext.accessPointName          =   "myAPN.com";
  apnContext.userName                 =   "APNusername"
  apnContext.password                 =   "APNPassword";
  apnContext.isCompressionEnabled     =   false;
  apnContext.authenticationType       =   connectivity.CellularApnAuthenticationType.none;

  //
  //  request the connection to Windows
  connectivity.connectivityManager.acquireConnectionAsync(apnContext).done(onConnectionSucceeded, onConnectionFailed);
}

//  on success Windows returns a ConnectionSession object that encapsulates the new connection profile
function onConnectionSucceeded(result)
{
  // keep the connectionSession in scope
  currentConnectionSession= result;
  //  create a route policy for the new connection
  enforceHttpRoutePolicy(currentConnectionSession.ConnectionProfile,new hostName("video.mydomain.com"),Windows.Networking.DomainNameType.suffix);

  // Backend data interaction with appropriate APIs(Open IFrame etc.)

}

//  Windows was not able to connect the specified APN
function onConnectionFailed()
{
  // display error message and just wait for Network Status Change event to try again
}

//  utility function to enforce a route policy
function enforceHttpRoutePolicy(connectionProfile,targetSuffix)
{
  //  Keep the route request global so we can close it later
  currentRoutePolicy= new connectivity.routePolicy(connectionProfile, targetSuffix);
  //  Indicate the new route policy to the Http stack
  connectivity.connectivityManager.addHttpRoutePolicy(currentRoutePolicy);
}

//  cleanup on shutdown
function onShutdown()
{
  //  Remove the route policy from HttpStack
  connectivity.connectivityManager.removeHttpRoutePolicy(currentRoutePolicy);
  currentRoutePolicy = null;

  //  If a different APN was connected, disconnect it to free up resources
  if(currentConnectionSession!= null)
  {
    currentConnectionSession.close();
  }
}
```

### <a name="span-idscenariomobilebroadbandapprequiresspecialpdpcontextforsubscriptionpurchaseandprovisioningspanspan-idscenariomobilebroadbandapprequiresspecialpdpcontextforsubscriptionpurchaseandprovisioningspanspan-idscenariomobilebroadbandapprequiresspecialpdpcontextforsubscriptionpurchaseandprovisioningspanscenario-mobile-broadband-app-requires-special-pdp-context-for-subscription-purchase-and-provisioning"></a><span id="Scenario__Mobile_broadband_app_requires_special_PDP_Context_for_subscription_purchase_and_provisioning"></span><span id="scenario__mobile_broadband_app_requires_special_pdp_context_for_subscription_purchase_and_provisioning"></span><span id="SCENARIO__MOBILE_BROADBAND_APP_REQUIRES_SPECIAL_PDP_CONTEXT_FOR_SUBSCRIPTION_PURCHASE_AND_PROVISIONING"></span>シナリオ:モバイル ブロード バンド アプリは、サブスクリプションの購入およびプロビジョニング特別な PDP コンテキストが必要です。

このシナリオで、モバイル ブロード バンド アプリは、サブスクリプションの購入およびプロビジョニング特別な PDP コンテキストが必要です。 このアプリには、接続されたネットワークに関係なく、特別な PDP コンテキストが有効になります。

``` syntax
var connectivity = Windows.Networking.Connectivity;
var currentRoutePolicy = null;
var currentConnectionSession = null;

function onLoad()
{
  // Register for network status change
  connectivity.networkInformation.addEventListener("networkstatuschanged", OnNetworkStatusChange);
  // Process the current status
  handleNetworkChange();
}

function onNetworkStatusChange()
{
  HandleNetworkChange();
}

//  Create the PDP Context/APN Data 
var apnContext                      =   new connectivity.CellularApnContext();
apnContext.providerId               =   "23545";
apnContext.accessPointName          =   "myAPN.com";
apnContext.userName                 =   "APNusername"
apnContext.password                 =   "";
apnContext.isCompressionEnabled     =  false;
apnContext.authenticationType       =   connectivity.CellularApnAuthenticationType.none;

//  Request the connection to Windows
connectivity.connectivityManager.acquireConnectionAsync(apnContext).done(onConnectionSucceeded, onConnectionFailed);

//  On successful connection to PDP Context,  Windows returns a ConnectionSession object that incapsulate the new connection profile
function onConnectionSucceeded(result)
{
  // keep the connectionSession in scope
  currentConnectionSession= result;

  //  create a route policy for the new connection
  currentRoutePolicy = new connectivity.routePolicy(currentConnectionSession.ConnectionProfile, new hostName("video.mydomain.com"),Windows.Networking.DomainNameType.suffix);

  //  indicate the new route policy to the Http stack
  connectivity.connectivityManager.addHttpRoutePolicy(currentRoutePolicy);

  // Backend data interaction with appropriate APIs(Open IFrame etc.)

  // After completing the data transfer remove the Route Policy
  connectivity.connectivityManager.removeHttpRoutePolicy(currentRoutePolicy);
  currentRoutePolicy = null;

  // Disconnect the PDP Context to free up resources
  currentConnectionSession.close();

}

function handleNetworkChange()
{
  // App behavior to handle network 
  var currentProfile = currentRoutePolicy.connectionProfile();
  if (NetworkConnectivityLevel.none != currentProfile.GetNetworkConnectivityLevel())
  {
    // The special PDP Context is disconnected, app should handle this. It can request another connection to special PDP Context or it can show error to the user.
  }
}
```

### <a name="span-idconsiderationsformobilebroadbandappsspanspan-idconsiderationsformobilebroadbandappsspanspan-idconsiderationsformobilebroadbandappsspanconsiderations-for-mobile-broadband-apps"></a><span id="Considerations_for_mobile_broadband_apps"></span><span id="considerations_for_mobile_broadband_apps"></span><span id="CONSIDERATIONS_FOR_MOBILE_BROADBAND_APPS"></span>モバイル ブロード バンド アプリに関する考慮事項

モバイル ブロード バンドのアプリでは、各 PDP コンテキストのローカル データ使用状況の情報を取得でき、特殊な PDP コンテキストのポリシーを Windows に影響することができます。

### <a name="span-idlocaldatausagespanspan-idlocaldatausagespanspan-idlocaldatausagespanlocal-data-usage"></a><span id="Local_data_usage"></span><span id="local_data_usage"></span><span id="LOCAL_DATA_USAGE"></span>ローカル データの使用状況

Windows 8 では現在のデータ使用状況を表示することのできるモバイル ブロード バンド アプリのユーザーと継続的なサブスクリプション ベースのリレーションシップを提供します。 ユーザーでは、データの現在の使用量を表示でき、その課金サイクルまたはセッション終了日を適切な判断を行うを理解することができます。 可能な限り、ネットワークの負荷を減らすためには、ネットワークとデータの使用状況を定期的に確認する必要があります。 Windows では、ユーザーに現在のデータの使用状況を表示するデータの使用状況を組み合わせて使用できるローカル データ使用量 API を提供します。

特別な PDP コンテキストは、特定のアプリケーションやサービスにデータ アクセス料金を区別する機能を提供します。 それぞれ別の PDP コンテキストは、ローカル データの使用率カウンターの別のプロファイルとして扱われます。 モバイル ブロード バンド アプリは、特定の期間中にどのようなインターネット PDP PDP コンテキストごとにローカル データの使用状況を照会できますコンテキストが Windows 8 で動作します。 この情報を使用すると、適切なデータ使用エクスペリエンスをユーザーに表示します。

次のサンプル コードでは、すべての PDP コンテキストのローカル データ使用量を読み取るネットワーク Api を使用する方法を示しています。

``` syntax
// Get the network account ID.
IReadOnlyList<string> networkAccIds = Windows.Networking.NetworkOperators.MobileBroadbandAccount.AvailableNetworkAccountIds;

if (networkAccIds.Count == 0)
{
  rootPage.NotifyUser("No network account ID found", NotifyType.ErrorMessage);
  return;
}

// For the sake of simplicity, assume we want to use the first account.
// Refer to the MobileBroadbandAccount API's how to select a specific account ID.
string networkAccountId = networkAccIds[0];

// Create mobile broadband object for specified network account ID
var mobileBroadbandAccount = Windows.Networking.NetworkOperators.MobileBroadbandAccount.CreateFromNetworkAccountId(networkAccountId);

// Get all connection profiles associated with this network account ID
var connectionProfiles = mobileBroadbandAccount.GetConnectionProfiles();

// Collect local usages for last one hour
DateTime endTime = DateTime.Now;
TimeSpan timeDiff = TimeSpan.FromHours(1);
DateTime startTime = endTime.Subtract(timeDiff);
string message = string.Empty;

foreach (var connectionProfile in connectionProfiles)
{
  // Display local usages for each connection profiles
  DataUsage localUsage = connectionProfile.GetLocalUsage(startTime, endTime);
  message += "Connection Profile Name:  " + connectionProfile.ProfileName + "\n\n";
  message += "Local Data Usage from " + startTime.ToString() + " to " + endTime.ToString() + ":\n";
  message += " Bytes Sent     : " + localUsage.BytesSent + "\n";
  message += " Bytes Received : " + localUsage.BytesReceived + "\n\n";
}

// Print the message string
```

### <a name="span-idpoliciesspanspan-idpoliciesspanspan-idpoliciesspanpolicies"></a><span id="Policies"></span><span id="policies"></span><span id="POLICIES"></span>ポリシー

いくつかの演算子は、特別な PDP コンテキストの帯域幅が制限されているが示されます。 特別な PDP コンテキストをアクティブ化するものの、特別な PDP コンテキストを使用してアクセスできないアプリには、サービス拒否攻撃を作成できます。 ビジネス関係を持つ特定のアプリに特別な APNs の使用量を制限する必要があります。 特別な APN 名を持つ Windows UWP アプリの一覧を提供することは。 Windows では、その情報を使用して、特別な APNs へのアクセスを制限します。 一覧を指定しない場合は、Windows では、特別な PDP コンテキストがすべてのアプリで開かれている前提としています。

**注**  特別な PDP コンテキストに余分なトラフィックを避けるためだけになります。 特別な PDP コンテキストへのアプリを制限するためのセキュリティ メカニズムとして、これに依存できません。 特別な PDP コンテキストへのアクセスを制限するには、ネットワーク上いくつかの認証やセキュリティ メカニズムを実装する必要があります。 たとえば、特定の PDP コンテキストの特定 IP アドレスのみを許可するフィルターを使用できます。

 

一部のモバイル ネットワークでは、複数の PDP コンテキストをサポートしていません。 かどうか、ネットワークで複数の PDP コンテキストがサポートされているかどうかをプロビジョニングすることができます。 ネットワークが複数の PDP コンテキストをサポートしていない場合 Windows が特別な APNs にオンデマンドでの接続を作成するアプリを許可しない必要があります。 既定では、Windows は、複数の PDP コンテキストをサポートすると仮定します。

次のサンプル XML ファイルには、Windows メタデータのプロビジョニングを使用して、特別な PDP コンテキストの許可されているアプリの一覧を提供する方法を示しています。

``` syntax
<?xml version="1.0" encoding="utf-8"?>
<CarrierProvisioning xmlns="http://www.microsoft.com/networking/CarrierControl/v1">
  <Global>
    <!-- Adjust the Carrier ID to fit your own ID. Refer to the documentation about Carrier ID's. -->
    <CarrierId>{11111111-1111-1111-1111-111111111111}</CarrierId>
    <!-- Adjust the Susbscriber ID. Refer to the documentation about Subscriber ID's. -->
    <SubscriberId>1234567890</SubscriberId>
  </Global>
  <Extensions>
    <Extensions_v2 xmlns="http://www.microsoft.com/networking/CarrierControl/v2">
      <AdditionalPDPContexts>
        <MultiplePDPContextPolicies MultiplePDPContextSupport="true">
          <PDPContextPolicy>
            <!-- Adjust the profile name -->
            <Name>Contoso1</Name>
            <Context>
              <!-- Adjust the access string to your APN. -->
              <AccessString>Contoso.Contoso1</AccessString>
              <!-- Adjust the UserLogonCred to fit your UserLogonCred. Refer to the documentation about UserLogonCred's. -->
              <UserLogonCred>
                <UserName>user1</UserName>
                <Password>password1</Password>
              </UserLogonCred>
            </Context>
            <AppIDList>
              <!-- Adjust the AppId to your AppId -->
              <AppID>Contoso.Sample1.CS_dsarewaj</AppID>
              <AppID>Contoso.Sample2.CPP_dsarewaj</AppID>
            </AppIDList>
          </PDPContextPolicy>
          <PDPContextPolicy>
            <!-- Adjust the profile name -->
            <Name>Contoso2</Name>
            <Context>
              <!-- Adjust the access string to your APN. -->
              <AccessString>Contoso.Contoso2</AccessString>
              <!-- Adjust the UserLogonCred to fit your UserLogonCred. Refer to the documentation about UserLogonCred. -->
              <UserLogonCred>
                <UserName>user2</UserName>
                <Password>password2</Password>
              </UserLogonCred>
            </Context>
            <AppIDList>
              <!-- Adjust the AppId to your AppId -->
              <AppID>Contoso.Sample3.CS_dsarewaj</AppID>
              <AppID>Contoso.Sample4.CPP_dsarewaj</AppID>
            </AppIDList>
          </PDPContextPolicy>
        </MultiplePDPContextPolicies>
      </AdditionalPDPContexts>
    </Extensions_v2>
  </Extensions>
</CarrierProvisioning>
```

## <a name="span-idaudioandvideostreamingspanspan-idaudioandvideostreamingspanspan-idaudioandvideostreamingspanaudio-and-video-streaming"></a><span id="Audio_and_video_streaming"></span><span id="audio_and_video_streaming"></span><span id="AUDIO_AND_VIDEO_STREAMING"></span>オーディオおよびビデオ ストリーミング


アプリのストリーミング オーディオでは、特別な PDP コンテキストを使用して、オーディオまたはビデオのストリームを再生できます。 HTTP Api と同様に、アプリで使用できる、次のロジックを使用して、オーディオまたはビデオを再生する、&lt;オーディオ&gt;または&lt;ビデオ&gt;タグ。

![アプリのストリーミングのワークフロー](images/mb-pdp-fig6.jpg)

使用することができます[Player Framework](http://playerframework.codeplex.com/)またはその他のビデオのフレームワークに基づいて、 [WinInet](https://msdn.microsoft.com/library/windows/desktop/aa385331) Api。

## <a name="span-idinstantgospanspan-idinstantgospanspan-idinstantgospaninstantgo"></a><span id="InstantGo"></span><span id="instantgo"></span><span id="INSTANTGO"></span>InstantGo


InstantGo ではインスタント、インスタント携帯電話に期待するユーザーになっているユーザー エクスペリエンスをオフします。 同様、スマート フォン、InstantGo により、システムは、適切なネットワークが利用可能な場合に、新しい、最新の状態であり、到達可能のままにします。 InstantGo 低電力 Pc プラットフォームでは、特定の Windows 認定要件を満たす必要があります。

InstantGo では、次のシナリオがサポートされています。

-   最新のコンテンツをライブ タイルを更新しています

-   電子メールを受信します。

-   ファイルをダウンロードしたり、web サイトへのアップロード

-   Web サイト上の写真などのコンテンツの共有

-   インスタント メッセージの受信

-   VoIP 呼び出しの受信

-   リアルタイムで通信します。

-   バック グラウンド オーディオおよび音楽の再生

InstantGo の詳細については、次を参照してください。 [InstantGo 概要](https://msdn.microsoft.com/library/windows/hardware/mt282515)します。

モバイル ブロード バンド アプリは、これら InstantGo シナリオをいくつかの操作を有効にするための特別な PDP コンテキストを使用できます。 次のロジックを使用して範囲外であるため、切断されている場合は、特別な PDP コンテキストに再接続する必要があります。 デバイスがコネクト スタンバイ電源状態になったとき、Windows は 10 分後に特別な PDP コンテキストへのすべての接続を切断し、アプリをもう一度接続を要求する必要があります。

バック グラウンドのモバイル ブロード バンド アプリでのネットワークを有効にする方法の詳細については、次を参照してください。[バック グラウンド タスクの概要](http://www.microsoft.com/download/details.aspx?id=27411)と[バック グラウンド ネットワーク](http://www.microsoft.com/download/details.aspx?id=28999)します。

![instantgo with pdp context](images/mb-pdp-fig5.jpg)

### <a name="span-idaudiostreaminginbackgroundspanspan-idaudiostreaminginbackgroundspanspan-idaudiostreaminginbackgroundspanaudio-streaming-in-background"></a><span id="Audio_streaming_in_background"></span><span id="audio_streaming_in_background"></span><span id="AUDIO_STREAMING_IN_BACKGROUND"></span>バック グラウンドでストリーミング オーディオ

オーディオのストリーミング アプリケーションでは、特別な PDP コンテキストを使用してバック グラウンドでと、コネクト スタンバイ電源状態でのオーディオことができます。 バック グラウンドでオーディオを再生する方法の詳細については、次を参照してください。[バック グラウンドでオーディオを再生する方法を](https://msdn.microsoft.com/library/windows/apps/hh700367)します。

### <a name="span-idreal-timecommunicationappsspanspan-idreal-timecommunicationappsspanspan-idreal-timecommunicationappsspanreal-time-communication-apps"></a><span id="Real-time_communication_apps"></span><span id="real-time_communication_apps"></span><span id="REAL-TIME_COMMUNICATION_APPS"></span>リアルタイム通信アプリ

VoIP またはチャット アプリなどのリアルタイム通信アプリでは、特別な PDP コンテキストのトリガーをウェイク アップを受信できます。 ウェイク アップ トリガーには、時間、システムがコネクト スタンバイ電源状態の場合も含むすべてのトリガーされるように、アプリができます。 ウェイク アップ トリガーを有効にする方法の詳細については、次を参照してください。[バック グラウンド ネットワーク](http://www.microsoft.com/download/details.aspx?id=28999)します。

このシナリオを有効にするモバイル ブロード バンド デバイス必要があります wake on をサポートするフィルター PDP コンテキストが特別なで説明したように、[モバイル ブロード バンド インターフェイス モデル (MBIM) 仕様](https://msdn.microsoft.com/library/windows/hardware/dn265427)します。

## <a name="mobile-broadband-devices"></a>モバイル ブロードバンド デバイス


複数の PDP コンテキストをサポートするために、モバイル ブロード バンド デバイスのファームウェア サポートする必要が複数の PDP コンテキストで定義されている、 [MBIM 仕様](https://go.microsoft.com/fwlink/?linkid=620028)します。 これは、必要がありますに渡すことも、Windows ハードウェア認定キット テスト特定複数の PDP コンテキスト。

この機能は、特定の演算子であるために、モバイル ブロード バンド デバイスでは省略可能です。 この機能を必要がある場合は、演算子の要件を次に複数の PDP コンテキスト機能を追加する必要があります。

-   デバイスのファームウェアの詳細セクション 10.5.12.1 として複数の IP データ ストリームをサポートする必要があります、 [MBIM 仕様](https://go.microsoft.com/fwlink/?linkid=620028)します。 これは、Cid のすべてのコントロールの実装のサポートが含まれています。 と IP のデータ ストリームを完全に複数の PDP コンテキストのサポート。

-   デバイスのファームウェアは、Windows で使用するため、複数のデュアル ベアラー (IPv4 と IPv6) PDP コンテキストをサポートする必要があります。

    -   ニーズに合わせてインターネット接続の 1 と、モバイル ブロード バンドのアプリの追加の PDP コンテキストが含まれます。

    -   これは、SMS のファームウェアを使用するデバイス管理の PDP コンテキストとその他の管理コンテキストには必要ありません。

-   デバイスのファームウェアは、既にそのファームウェア内で内部的にデバイスが管理されている PDP コンテキストの適切にホスト オペレーティング システムの要求を利用できる必要があります。

-   デバイスのファームウェアは、SMS PDP コンテキストを抽象化し、それらの下に使用されるベアラーに関係なく SMS Cid 経由でルーティングを続行する必要があります。

 

 






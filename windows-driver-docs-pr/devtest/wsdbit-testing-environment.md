---
title: WSDBIT のテスト環境
description: WSDBIT のテスト環境
ms.assetid: 6fa6f6f7-859a-4424-a71d-600f82b23f89
keywords:
- WSDBIT ツール WDK、テスト環境
- WSDAPI 基本的な相互運用性ツール WDK、テスト環境
- WSDBIT ツール WDK、ネットワーク トポロジ
- WSDAPI 基本的な相互運用性ツール WDK、ネットワーク トポロジ
- テスト環境の WDK WSDBIT
- WSDBIT ツール WDK、サービス
- WSDAPI 基本的な相互運用性ツール WDK、サービス
- SimpleService サービス WDK WSDBIT
- AttachmentService サービス WDK WSDBIT
- EventingService サービス WDK WSDBIT
- WSDBIT ツール WDK、テスト用のデバイス
- WSDAPI 基本的な相互運用性ツール WDK、テスト用のデバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12ab3579852663f75f141ad19844df19ce5994fc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373150"
---
# <a name="wsdbit-testing-environment"></a>WSDBIT のテスト環境


このトピックでは、物理環境と、デバイスとそのホステッド サービスの機能について説明します。

### <a name="span-idnetworkmodelspanspan-idnetworkmodelspannetwork-model"></a><span id="network_model"></span><span id="NETWORK_MODEL"></span>ネットワークのモデル

デバイスとクライアントのテスト、イーサネット ネットワーク セグメントに接続しているし、1 つの IP サブネットを形成します。 (IPv4、IPv6、またはホスト名) などのネットワークのアドレス指定スキームは関係ありません、クライアントとデバイスの両方に共通に少なくとも 1 つのスキームをサポートするだけの期間のみに 1 つのデバイスとサブネット上の 1 つのクライアントがある必要があります。

デバッグとトラブルシューティングを容易にネットワーク モニターを使用して、デバイスとクライアント間のトラフィックの交換を監視する必要があります。 すべてのトラフィックを監視するには、ネットワーク セグメントにイーサネット ハブを通じて、デバイスとクライアントを接続する必要があります。 ハブが利用できない場合は、WSDBIT を実行しているコンピューターでネットワーク モニターをインストールすることでトラフィックを監視することができます。

次の図は、デバイス、クライアント、およびハブ経由で接続すべてネットワーク モニターで構成されるネットワーク トポロジを示します。

![wsdapi 基本的な相互運用性ツール (wsdbit) をテストするためのネットワーク トポロジを示す図](images/wsdbit1.png)

### <a name="span-idtestdevicespanspan-idtestdevicespantest-device"></a><span id="test_device"></span><span id="TEST_DEVICE"></span>テスト デバイス

デバイス側のテストに参加するに次の一般的なガイドライン」の説明に従って、デバイスを実装する必要があります。 デバイスの実装の詳細については、次を参照してください。、 [WSDBIT 参照](wsdbit-reference.md)と[デバイス プロファイルの Web サービス (DPWS)](https://go.microsoft.com/fwlink/p/?linkid=163864)仕様。

次の表では、サービスと相互運用性のテスト ケース依存関係について説明します。

シナリオ SimpleService AttachmentService EventingService デバイスとサービスの検査

1 つ以上の SimpleService、AttachmentService、または EventingService

デバイス制御

x

添付ファイル

x

イベント処理

x

 

テスト デバイスには、3 つの種類のサービスをホストする必要があります。

-   http://schemas.example.org/SimpleService

-   http://schemas.example.org/AttachmentService

-   http://schemas.example.org/EventingService

### <a name="span-idsimpleservicespanspan-idsimpleservicespansimpleservice"></a><span id="simpleservice"></span><span id="SIMPLESERVICE"></span>SimpleService

**SimpleService**サービス 4 つのメソッドには。

-   **OneWay**一方向メソッドをパラメーターとして整数です。

-   **TwoWay**は、要求と応答でこれらの整数の合計で 2 つの整数で、要求-応答方法です。

-   **入力**は、要求内のさまざまな種類と、応答は、ブール値の 10 進数を含む、float、および Url の一覧で正確に同じ型の数が、要求-応答方法です。

-   **AnyCheck**応答で要求の XML フラグメントと同一のフラグメント要求-応答メソッドが返されます。

### <a name="span-idattachmentservicespanspan-idattachmentservicespanattachmentservice"></a><span id="attachmentservice"></span><span id="ATTACHMENTSERVICE"></span>AttachmentService

**AttachmentService**サービスが添付ファイルを送受信します。 送受信する添付ファイルのデータが含まれている、 \\2 つの個別のファイルとの相互運用機能のディレクトリ。Image1.jpg Image2.jpg. このサービスでは、2 つの方法があります。

-   **OneWayAttachment**をパラメーターとしてファイルが添付されたの一方向メソッドです。

-   **TwoWayAttachment**は、要求と応答の両方で添付ファイルの要求-応答方法です。

### <a name="span-ideventingservicespanspan-ideventingservicespaneventingservice"></a><span id="eventingservice"></span><span id="EVENTINGSERVICE"></span>EventingService

**EventingService**サービスには 2 種類のイベントをサブスクライブすることができます。

-   **SimpleEvent**パラメーターを指定せずイベントです。

-   **IntegerEvent**整数を返すイベントです。

### <a name="span-idimplementingtestservicesspanspan-idimplementingtestservicesspanimplementing-test-services"></a><span id="implementing_test_services"></span><span id="IMPLEMENTING_TEST_SERVICES"></span>テスト サービスを実装します。

すべての相互運用性テスト_ケースを実行するには、これらすべてのサービスを実装する必要があります。 この場合、デバイスは、初期の起動後に、これらの各サービスの 1 つのインスタンスをホストします。

ただし、これらのサービスの一部のみを実装する場合は、サービスと相互運用機能のテスト ケース依存関係については、このトピックの冒頭にある表を参照してください。

**注**  高度な相互運用性シナリオのいずれかを試行する (など[デバイス制御](device-control-scenarios.md)、[添付ファイル](attachments-scenarios.md)、および[Eventing](eventing-scenarios.md))、テスト デバイスは、少なくともをサポートする必要があります、[デバイスとサービスの検査テスト_ケース](device-and-service-inspection-scenarios.md)します。 デバイスには、このテスト_ケースが失敗した場合、高度なテスト_ケースを続行すること可能性がありますできません。

 

テスト デバイスと WSDBIT デバイス (WSDBIT\_サーバー)、次を実行できる必要があります。

-   整数の入力パラメーターの表示、 **SimpleService**一方向メソッド。

-   双方向の型チェックの要求で送信される型の値を表示します。

-   必要ですが、この検証の結果を表示する必要がありますが、よく知られている添付ファイルに対して受信した添付ファイルを確認します。

-   開始に記載されているイベントの 2 つの種類はそれぞれ、 **EventingService**を通じて手動で入力またはタイマー。

-   拡張可能で受信するデータを表示 (**xs: 任意**) のセクションでします。

-   使用して、 **xs:anyURI testdevice**として、 **wsd:Scopes**検出用の要素。

 

 






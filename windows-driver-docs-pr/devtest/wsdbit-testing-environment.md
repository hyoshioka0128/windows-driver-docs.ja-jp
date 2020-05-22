---
title: WSDBIT のテスト環境
description: WSDBIT のテスト環境
ms.assetid: 6fa6f6f7-859a-4424-a71d-600f82b23f89
keywords:
- WSDBIT tool WDK、テスト環境
- WSDAPI 基本相互運用性ツール WDK、テスト環境
- WSDBIT ツール WDK、ネットワークトポロジ
- WSDAPI 基本的な相互運用性ツール WDK、ネットワークトポロジ
- 環境のテスト WDK WSDBIT
- WSDBIT ツール WDK、サービス
- WSDAPI 基本相互運用性ツール WDK、サービス
- SimpleService サービスの WDK WSDBIT
- AttachmentService service WDK WSDBIT
- EventingService サービスの WDK WSDBIT
- WSDBIT ツール WDK、テスト用デバイス
- WSDAPI 基本相互運用性ツール WDK, テスト用デバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c7aac8738f9a687cbce79e35721290089bb873c
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769670"
---
# <a name="wsdbit-testing-environment"></a>WSDBIT のテスト環境


このトピックでは、物理環境、デバイス、およびそのホストされるサービス機能について説明します。

### <a name="span-idnetwork_modelspanspan-idnetwork_modelspannetwork-model"></a><span id="network_model"></span><span id="NETWORK_MODEL"></span>ネットワークモデル

テストするデバイスとクライアントは、イーサネットネットワークセグメントに接続され、1つの IP サブネットを形成します。 ネットワークアドレス指定スキーム (IPv4、IPv6、またはホスト名など) は、クライアントとデバイスの両方で少なくとも1つの共通のスキームがサポートされている限り、サブネット上に1つのデバイスと1つのクライアントしか存在できないため、関係ありません。

デバッグとトラブルシューティングを容易にするために、ネットワークモニターを使用して、デバイスとクライアント間のトラフィック交換を監視する必要があります。 すべてのトラフィックを監視するには、イーサネットハブ経由でデバイスとクライアントをネットワークセグメントに接続する必要があります。 ハブが使用できない場合は、WSDBIT を実行しているコンピューターにネットワークモニターをインストールすることによって、トラフィックを監視できる可能性があります。

次の図は、デバイス、クライアント、およびネットワークモニターで構成されるネットワークトポロジを示しています。これらはすべてハブを介して接続されています。

![wsdapi 基本相互運用性ツール (wsdbit) テストのネットワークトポロジを示す図](images/wsdbit1.png)

### <a name="span-idtest_devicespanspan-idtest_devicespantest-device"></a><span id="test_device"></span><span id="TEST_DEVICE"></span>テストデバイス

デバイス側のテストに参加するには、次の一般的なガイドラインに従ってデバイスを実装する必要があります。 デバイスの実装の詳細については、 [WSDBIT のリファレンス](wsdbit-reference.md)と、 [WEB サービス (dpws) 仕様のデバイスプロファイル](http://schemas.xmlsoap.org/ws/2006/02/devprof/)に関する説明を参照してください。

次の表では、サービスと相互運用性のテストケースの依存関係について説明します。

シナリオ SimpleService AttachmentService EventingService のデバイスとサービスの検査

SimpleService、AttachmentService、または EventingService の1つ以上

デバイス制御

x

[Attachments]

x

イベント

x

 

テストデバイスでは、次の3種類のサービスをホストする必要があります。

-   http://schemas.example.org/SimpleService

-   http://schemas.example.org/AttachmentService

-   http://schemas.example.org/EventingService

### <a name="span-idsimpleservicespanspan-idsimpleservicespansimpleservice"></a><span id="simpleservice"></span><span id="SIMPLESERVICE"></span>SimpleService

**Simpleservice**サービスには、次の4つの方法があります。

-   **OneWay**は、パラメーターとして整数を持つ一方向のメソッドです。

-   **TwoWay**は、要求-応答メソッドであり、要求に2つの整数が含まれ、応答でこれらの整数の合計が含まれています。

-   **TypeCheck**は、要求/応答メソッドであり、要求にはさまざまな種類があり、応答には、ブール値、decimal、float、および url のリストを含む、同じ種類の応答がまったく同じです。

-   **Anycheck**は、要求-応答メソッドであり、要求に XML フラグメントがあり、応答で同じフラグメントが返されます。

### <a name="span-idattachmentservicespanspan-idattachmentservicespanattachmentservice"></a><span id="attachmentservice"></span><span id="ATTACHMENTSERVICE"></span>AttachmentService

**Attachmentservice**サービスは添付ファイルを送受信します。 送信および受信する添付データは、 \\ image1. と Image2 という2つの個別のファイルとして interop ディレクトリに含まれます。 このサービスには、次の2つの方法があります。

-   **Oneattachments 添付ファイル**は、パラメーターとして添付ファイルを持つ一方向のメソッドです。

-   **Twowayattachment**は、要求と応答の両方に添付ファイルがある要求-応答メソッドです。

### <a name="span-ideventingservicespanspan-ideventingservicespaneventingservice"></a><span id="eventingservice"></span><span id="EVENTINGSERVICE"></span>EventingService

**Eventingservice**サービスには、次の2種類のイベントをサブスクライブできます。

-   **Simpleevent**は、パラメーターのないイベントです。

-   整数**イベント**は、整数を返すイベントです。

### <a name="span-idimplementing_test_servicesspanspan-idimplementing_test_servicesspanimplementing-test-services"></a><span id="implementing_test_services"></span><span id="IMPLEMENTING_TEST_SERVICES"></span>テストサービスの実装

すべての相互運用性テストケースを実行するには、これらすべてのサービスを実装する必要があります。 この場合、初期起動後に、デバイスはこれらの各サービスの1つのインスタンスをホストします。

ただし、これらのサービスの一部だけを実装する場合は、このトピックの冒頭にある表で、サービスと相互運用テストケースの依存関係に関する情報を参照してください。

**メモ**   高度な相互運用性のシナリオ ([デバイスの制御](device-control-scenarios.md)、[添付ファイル](attachments-scenarios.md)、[イベント](eventing-scenarios.md)など) を試すには、少なくとも[デバイスとサービス検査のテストケース](device-and-service-inspection-scenarios.md)をテストデバイスでサポートする必要があります。 デバイスがこのテストケースに失敗した場合は、高度なテストケースを続行できない可能性があります。

 

テストデバイスと WSDBIT デバイス (WSDBIT \_ サーバー) は、次の操作を実行できる必要があります。

-   **Simpleservice**の一方向メソッドの整数入力パラメーターを表示します。

-   双方向の型チェック要求で送信された型の値を表示します。

-   受信した添付ファイルが、予期されていた既知の添付ファイルと照合され、この検証の結果を表示する必要があることを確認します。

-   **Eventingservice**で説明されている2種類のイベントを、手動入力またはタイマーを使用して開始します。

-   拡張可能な (**xs: any**) セクションで受信したデータを表示します。

-   検出のために、wsd: **anyURI testdevice**を**wsd: スコープ**要素として使用します。

 

 






---
title: 制御要求の処理
description: 制御要求の処理
ms.assetid: D2096548-E3E2-4EB6-B3F2-C5AF45E8F4D5
keywords:
- NetAdapterCx に対する制御要求の処理、NetCx コントロールの処理を要求します。
ms.date: 06/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: a69a536cee452975b9c0853d4911dcc0232c78b1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372768"
---
# <a name="handling-control-requests"></a>制御要求の処理

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

NetAdapterCx モデルでは、クライアント ドライバーは、OID (オブジェクト識別子)、要求を表す、NETREQUEST オブジェクトとしてほとんどのコントロール要求を受信します。 クライアント ドライバーは、通常、コントロールの要求を管理する 1 つまたは 2 つの WDF キュー (NETREQUESTQUEUEs と呼ばれます) を設定します。

NETREQUESTQUEUE オブジェクトは、管理する各 NETREQUEST の親です。 キューが自動的に NETADAPTER オブジェクト、WDF の子があるため、各キューの削除と、アダプターが削除されたときに、関連する要求。

NetAdapterCx の既定親のすべての子リレーションシップを表示する、次を参照してください。[概要の NetAdapterCx オブジェクト](summary-of-netadaptercx-objects.md)します。

## <a name="creating-queue-objects"></a>キューのオブジェクトを作成します。

NetAdapterCx モデルでは、クライアントは、(Oid) のコントロール要求を処理するための 2 種類のキューを使用できます。
* 通常の要求 (Oid) のシーケンシャルのキューです。 NetAdapterCx では、一度に 1 つのクライアントに要求を提供します。
* 直接要求 (Oid) の並列のキューです。 NetAdapterCx は並列で要求を提供します。

これらのディスパッチ方法の詳細については、次を参照してください。 [I/O 要求のディスパッチ メソッド](../wdf/dispatching-methods-for-i-o-requests.md)します。

キューを作成するこれらのメソッドを呼び出します。

* [**NET_REQUEST_QUEUE_CONFIG_INIT_DEFAULT_SEQUENTIAL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequestqueue/nf-netrequestqueue-net_request_queue_config_init_default_sequential)
* [**NET_REQUEST_QUEUE_CONFIG_INIT_DEFAULT_PARALLEL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequestqueue/nf-netrequestqueue-net_request_queue_config_init_default_parallel)

## <a name="registering-handlers"></a>ハンドラーを登録します。

次の 3 つの主な要求の種類 (データのクエリ、データ、およびメソッド) のそれぞれについて、クライアント ドライバーは、1 つの既定のハンドラー、または 1 つまたは複数の OID に固有のハンドラーを指定できます。

どちらの方法は、スイッチ ステートメントを使用して、残りの部分を既定のハンドラーを使用しながら、いくつかの Oid のカスタム ハンドラーを提供することで同じドライバーを使用できます。

クライアント ドライバーは、OID ハンドラーを登録します。 その[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)ルーチン。

次のコントロール、クライアントが提供できる要求のハンドラーに示します。

* [*EVT_NET_REQUEST_METHOD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequestqueue/nc-netrequestqueue-evt_net_request_method)
* [*EVT_NET_REQUEST_QUERY_DATA*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequestqueue/nc-netrequestqueue-evt_net_request_query_data)
* [*EVT_NET_REQUEST_SET_DATA*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequestqueue/nc-netrequestqueue-evt_net_request_set_data)
* [*EVT_NET_REQUEST_DEFAULT_METHOD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequestqueue/nc-netrequestqueue-evt_net_request_default_method)
* [*EVT_NET_REQUEST_DEFAULT_QUERY_DATA*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequestqueue/nc-netrequestqueue-evt_net_request_default_query_data)
* [*EVT_NET_REQUEST_DEFAULT_SET_DATA*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequestqueue/nc-netrequestqueue-evt_net_request_default_set_data)

次の 3 つの主な要求の種類ごとに、OID に固有のハンドラーは、既定のハンドラーに優先します。 NetAdapterCx は、クライアントは、特定の OID のどちらを提供する場合、要求は失敗します。

データのクエリ、データ、およびメソッド以外の型の要求、クライアント ドライバーを提供できます、 [ *EVT_NET_REQUEST_DEFAULT* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequestqueue/nc-netrequestqueue-evt_net_request_default)イベント コールバック関数。

たとえば、プロトコル ドライバーに OID 要求を発行する`NDIS_REQUEST_TYPE = NdisRequestGeneric1`、NetAdapterCx 呼び出し[ *EVT_NET_REQUEST_DEFAULT*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequestqueue/nc-netrequestqueue-evt_net_request_default)します。 NetAdapterCx では、クライアント ドライバーがこのようなハンドラーを指定しない場合、要求が失敗します。

次の図は、一般的なフローを示しています。

<img src="images/netcx-adapter-request-handling-flow.png" alt="NetAdapterCx request handling flow" title="NetAdapterCx 要求の処理フロー" style="width: 800px;"/>

次のスニペットは、クライアントが既定のハンドラーを設定する方法を示しています。

```C++
NTSTATUS status;
NET_REQUEST_QUEUE_CONFIG config;
NETREQUESTQUEUE requestQueue;

NET_REQUEST_QUEUE_CONFIG_INIT_DEFAULT_SEQUENTIAL(&config, NetAdapter);
config.EvtRequestDefaultQueryData = MyDefaultQueryData;
config.EvtRequestDefaultSetData = MyDefaultSetData;
config.EvtRequestDefaultMethod = MyDefaultMethod;

config.EvtRequestDefault = MyDefault;
```

OID 固有のハンドラーを追加するには、これらのメソッドを使用します。

* [**NET_REQUEST_QUEUE_CONFIG_ADD_QUERY_DATA_HANDLER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequestqueue/nf-netrequestqueue-net_request_queue_config_add_query_data_handler)
* [**NET_REQUEST_QUEUE_CONFIG_ADD_SET_DATA_HANDLER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequestqueue/nf-netrequestqueue-net_request_queue_config_add_set_data_handler)
* [**NET_REQUEST_QUEUE_CONFIG_ADD_METHOD_HANDLER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequestqueue/nf-netrequestqueue-net_request_queue_config_add_method_handler)

次の例では[ **NET_REQUEST_QUEUE_CONFIG_ADD_QUERY_DATA_HANDLER** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequestqueue/nf-netrequestqueue-net_request_queue_config_add_query_data_handler)クライアントへのポインターを[ *EVT_NET_REQUEST_QUERY_DATA* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequestqueue/nc-netrequestqueue-evt_net_request_query_data) OID を特定のハンドラーを登録するイベントのコールバック関数。

```C++
NET_REQUEST_QUEUE_CONFIG_ADD_QUERY_DATA_HANDLER(
 &config, OID_GEN_VENDOR_DESCRIPTION,
 EvtQueryGenVendorDescription, sizeof(NIC_VENDOR_DESC));
```

## <a name="creating-the-queue"></a>キューの作成

好きなよう各 OID キューを設定したら後で呼び出す[ **NetRequestQueueCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequestqueue/nf-netrequestqueue-netrequestqueuecreate)キューを作成します。

```C++
status = NetRequestQueueCreate(&config, WDF_NO_OBJECT_ATTRIBUTES, NULL);

if(!NT_SUCCESS(status))
{
 return status;
}
```

NetAdapterCx にコントロール要求ハンドラーのドライバーのクライアントを呼び出すことができますとすぐに[ *EVT_WDF_DEVICE_PREPARE_HARDWARE* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)呼び出し時まで返します[ *EVT_WDF_DEVICE_RELEASE_HARDWARE*](https://msdn.microsoft.com/library/windows/hardware/ff540890)します。

## <a name="completing-requests"></a>要求の完了

クライアント ドライバーでは、受信した各 NETREQUEST を完了する必要があります。 それ以外の場合、コントロール要求は、保留中状態のままです。 要求は同期的に処理できない場合、クライアント ドライバーは、後で保留中の NETREQUEST を完了する必要があります。 保留中の要求を完了できなかった場合に、クライアント ドライバーが、デバイスの電源を切るときに応答しなくなる可能性があります。

元の要求が十分な大きさのバッファーを含まない場合[ **NetRequestSetBytesNeeded**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequest/nf-netrequest-netrequestsetbytesneeded)します。 コントロールの要求を完了し、完了の状態のみを指定、 [ **NetRequestCompleteWithoutInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequest/nf-netrequest-netrequestcompletewithoutinformation)次のスニペットに示すように、OID ハンドラーから。
 
```C++
 NetRequestCompleteWithoutInformation(Request, STATUS_SUCCESS);
```

元の要求に大規模なが含まれている場合だけバッファー、クライアント ドライバーの呼び出し[ **NetRequestRetrieveInputOutputBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequest/nf-netrequest-netrequestretrieveinputoutputbuffer)入力/出力バッファーを取得します。 クライアントは、データ転送し、要求の種類に応じて、次のいずれかを使用して要求を完了します。

* [**NetRequestMethodComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequest/nf-netrequest-netrequestmethodcomplete)
* [**NetRequestQueryDataComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequest/nf-netrequest-netrequestquerydatacomplete)
* [**NetRequestSetDataComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrequest/nf-netrequest-netrequestsetdatacomplete)

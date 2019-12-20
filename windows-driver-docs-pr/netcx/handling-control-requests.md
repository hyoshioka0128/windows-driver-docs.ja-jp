---
title: 制御要求の処理
description: 制御要求の処理
ms.assetid: D2096548-E3E2-4EB6-B3F2-C5AF45E8F4D5
keywords:
- NetAdapterCx 処理コントロール要求、NetCx 処理制御要求
ms.date: 06/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: e30d1259789909aeb36206ed2b2880e167e93523
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210782"
---
# <a name="handling-control-requests"></a>制御要求の処理

NetAdapterCx モデルでは、クライアントドライバーはほとんどの制御要求を NETREQUEST オブジェクトとして受信し、それぞれが OID (オブジェクト識別子) 要求を表します。 クライアントドライバーは、通常、制御要求を管理するために、1つまたは2つの WDF キュー (NETREQUESTQUEUEs) を設定します。

NETREQUESTQUEUE オブジェクトは、それが管理する各 NETREQUEST の親です。 キューは NETADAPTER オブジェクトの子であるため、WDF は、アダプターが削除されると、各キューと関連付けられているすべての要求を自動的に削除します。

NetAdapterCx のすべての既定の親子関係を表示するには、「 [NetAdapterCx オブジェクトの概要](summary-of-netadaptercx-objects.md)」を参照してください。

## <a name="creating-queue-objects"></a>キューオブジェクトの作成

NetAdapterCx モデルでは、クライアントは、次の2種類のキューを使用して制御要求 (Oid) を処理できます。
* 通常の要求 (Oid) のシーケンシャルキュー。 NetAdapterCx は、一度に1つの要求をクライアントに配信します。
* 直接要求 (Oid) の並列キュー。 NetAdapterCx は、同時に要求を配信します。

これらのディスパッチ方法の詳細については、「 [I/o 要求のメソッドのディスパッチ](../wdf/dispatching-methods-for-i-o-requests.md)」を参照してください。

キューを作成するには、次のメソッドを呼び出します。

* [**NET_REQUEST_QUEUE_CONFIG_INIT_DEFAULT_SEQUENTIAL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequestqueue/nf-netrequestqueue-net_request_queue_config_init_default_sequential)
* [**NET_REQUEST_QUEUE_CONFIG_INIT_DEFAULT_PARALLEL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequestqueue/nf-netrequestqueue-net_request_queue_config_init_default_parallel)

## <a name="registering-handlers"></a>ハンドラーの登録

クライアントドライバーは、3つの主要な要求の種類 (query data、set data、および method) ごとに、1つの既定のハンドラー、または1つ以上の OID 固有のハンドラーを提供できます。

同じドライバーで両方の方法を使用して、一部の Oid にカスタムハンドラーを提供し、その剰余に switch ステートメントを指定して既定のハンドラーを使用することができます。

クライアントドライバーは、 [*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)ルーチンに OID ハンドラーを登録します。

クライアントが提供できるコントロール要求ハンドラーを次に示します。

* [*EVT_NET_REQUEST_METHOD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequestqueue/nc-netrequestqueue-evt_net_request_method)
* [*EVT_NET_REQUEST_QUERY_DATA*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequestqueue/nc-netrequestqueue-evt_net_request_query_data)
* [*EVT_NET_REQUEST_SET_DATA*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequestqueue/nc-netrequestqueue-evt_net_request_set_data)
* [*EVT_NET_REQUEST_DEFAULT_METHOD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequestqueue/nc-netrequestqueue-evt_net_request_default_method)
* [*EVT_NET_REQUEST_DEFAULT_QUERY_DATA*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequestqueue/nc-netrequestqueue-evt_net_request_default_query_data)
* [*EVT_NET_REQUEST_DEFAULT_SET_DATA*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequestqueue/nc-netrequestqueue-evt_net_request_default_set_data)

3つの主要な要求の種類ごとに、OID 固有のハンドラーが既定のハンドラーよりも優先されます。 クライアントが指定された OID に対してどちらも指定しない場合、NetAdapterCx は要求に失敗します。

Query data、set data、および method 以外の種類の要求の場合、クライアントドライバーは[*EVT_NET_REQUEST_DEFAULT*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequestqueue/nc-netrequestqueue-evt_net_request_default)イベントのコールバック関数を提供できます。

たとえば、プロトコルドライバーが `NDIS_REQUEST_TYPE = NdisRequestGeneric1`で OID 要求を発行した場合、NetAdapterCx は[*EVT_NET_REQUEST_DEFAULT*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequestqueue/nc-netrequestqueue-evt_net_request_default)を呼び出します。 クライアントドライバーがこのようなハンドラーを提供していない場合、NetAdapterCx は要求に失敗します。

次の図は、一般的なフローを示しています。

<img src="images/netcx-adapter-request-handling-flow.png" alt="NetAdapterCx request handling flow" title="NetAdapterCx 要求処理フロー" style="width: 800px;"/>

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

OID 固有のハンドラーを追加するには、次のメソッドを使用します。

* [**NET_REQUEST_QUEUE_CONFIG_ADD_QUERY_DATA_HANDLER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequestqueue/nf-netrequestqueue-net_request_queue_config_add_query_data_handler)
* [**NET_REQUEST_QUEUE_CONFIG_ADD_SET_DATA_HANDLER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequestqueue/nf-netrequestqueue-net_request_queue_config_add_set_data_handler)
* [**NET_REQUEST_QUEUE_CONFIG_ADD_METHOD_HANDLER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequestqueue/nf-netrequestqueue-net_request_queue_config_add_method_handler)

次の例では、クライアントの[*EVT_NET_REQUEST_QUERY_DATA*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequestqueue/nc-netrequestqueue-evt_net_request_query_data)イベントコールバック関数へのポインターを使用して[**NET_REQUEST_QUEUE_CONFIG_ADD_QUERY_DATA_HANDLER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequestqueue/nf-netrequestqueue-net_request_queue_config_add_query_data_handler)を呼び出し、特定の OID のハンドラーを登録します。

```C++
NET_REQUEST_QUEUE_CONFIG_ADD_QUERY_DATA_HANDLER(
 &config, OID_GEN_VENDOR_DESCRIPTION,
 EvtQueryGenVendorDescription, sizeof(NIC_VENDOR_DESC));
```

## <a name="creating-the-queue"></a>キューの作成

各 OID キューを設定したら、 [**NetRequestQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequestqueue/nf-netrequestqueue-netrequestqueuecreate)を呼び出してキューを作成します。

```C++
status = NetRequestQueueCreate(&config, WDF_NO_OBJECT_ATTRIBUTES, NULL);

if(!NT_SUCCESS(status))
{
 return status;
}
```

NetAdapterCx は、 [*EVT_WDF_DEVICE_RELEASE_HARDWARE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)を呼び出すまで[*EVT_WDF_DEVICE_PREPARE_HARDWARE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)が返されるとすぐに、クライアントドライバーの制御要求ハンドラーを呼び出すことができます。

## <a name="completing-requests"></a>要求の完了

クライアントドライバーは、受信した各 NETREQUEST を完了する必要があります。 それ以外の場合、制御要求は保留中の状態のままになります。 要求を同期的に処理できない場合、クライアントドライバーは後で保留中の NETREQUEST を完了する必要があります。 保留中の要求を完了できないと、デバイスの電源がオフになったときにクライアントドライバーが応答しなくなることがあります。

元の要求に十分な大きさのバッファーが含まれていない場合は、 [**Netrequestsetbytesneeded**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequest/nf-netrequest-netrequestsetbytesneeded)呼び出す必要があります。 制御要求を完了して、完了状態のみを指定するには、次のスニペットに示すように、OID ハンドラーから[**Netrequestcomplete情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequest/nf-netrequest-netrequestcompletewithoutinformation)を呼び出します。
 
```C++
 NetRequestCompleteWithoutInformation(Request, STATUS_SUCCESS);
```

元の要求に十分な大きさのバッファーが含まれていた場合、クライアントドライバーは[**NetRequestRetrieveInputOutputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequest/nf-netrequest-netrequestretrieveinputoutputbuffer)を呼び出して入出力バッファーを取得します。 次に、クライアントは、要求の種類に応じて、次のいずれかを使用してデータを転送し、要求を完了します。

* [**NetRequestMethodComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequest/nf-netrequest-netrequestmethodcomplete)
* [**NetRequestQueryDataComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequest/nf-netrequest-netrequestquerydatacomplete)
* [**NetRequestSetDataComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrequest/nf-netrequest-netrequestsetdatacomplete)

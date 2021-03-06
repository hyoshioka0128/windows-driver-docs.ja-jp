---
title: VM キューの割り当て
description: VM キューの割り当て
ms.assetid: 2645a6e5-3824-469c-84d5-8e49fa01f494
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 120f2d898edbc9a16050e5434a0249008f33e30b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384418"
---
# <a name="allocating-a-vm-queue"></a>VM キューの割り当て





上位のドライバーの問題、初期構成パラメーターのセットを持つキューを割り当てるには、 [OID\_受信\_フィルター\_ALLOCATE\_キュー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-allocate-queue)メソッド要求の OID。 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体は、初期状態へのポインターを含む、 [**NDIS\_受信\_キュー\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)構造体。 OID メソッドの要求から正常に戻った後、 **InformationBuffer**のメンバー、 **NDIS\_OID\_要求**構造体にはへのポインターが含まれています、 **NDIS\_受信\_キュー\_パラメーター**新しいキューの id と、MSI X テーブルのエントリを持つ構造体。

[ **NDIS\_受信\_キュー\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)で構造が使用される、 [OID\_受信\_フィルター\_割り当てる\_キュー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-allocate-queue) OID と[OID\_受信\_フィルター\_キュー\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-queue-parameters) OID。 VM キュー パラメーターの詳細については、次を参照してください。 [VM キュー パラメーターの更新の取得と](obtaining-and-updating-vm-queue-parameters.md)します。

上にあるドライバーを初期化します、 [ **NDIS\_受信\_キュー\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)次のキュー構成パラメーターを含む構造体。

-   キューの種類 (**NdisReceiveQueueTypeVMQueue**から、 [ **NDIS\_受信\_キュー\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ne-ntddndis-_ndis_receive_queue_type)列挙します)。

-   キューのプロセッサの関係。

-   キュー名と仮想マシンの名前。

-   先読み分割パラメーター。

    **注**  NDIS 6.30 以降、パケット データを別の lookahead バッファーに分割することは現在サポートされていません。

     

**注**  上にあるドライバーは、NDIS を設定できる\_受信\_キュー\_パラメーター\_1 秒あたり\_キュー\_受信\_を示す値とNDIS\_受信\_キュー\_パラメーター\_先読み\_分割\_で必須フラグ、**フラグ**のメンバー[ **NDIS\_受信\_キュー\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)構造体。 その他のフラグは、キューの割り当ては使用されません。

 

NDIS は、受信キューを割り当てる OID 要求を受信、キューのパラメーターを確認します。 NDIS は、必要なリソースとキューの id を割り当て後、は、基になるミニポート ドライバーに OID 要求を送信します。 キューの id は、関連付けられているネットワーク アダプターに固有です。

ミニポート ドライバーは、受信キューに、必要なソフトウェアとハードウェア リソースを割り当てることができますが正常に場合、に、成功のステータスの OID 要求を完了します。

NDIS がキュー識別子を割り当てます NDIS ミニポート ドライバーに OID 要求を送信する前に、 **QueueId**のメンバー、 [ **NDIS\_受信\_キュー\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)構造体であり、ミニポート ドライバーにメソッド要求を渡します。 ミニポート ドライバー MSI X テーブルのエントリを提供する、 **MSIXTableEntry**メンバー。

ミニポート ドライバーでは、割り当てられた受信キューのキューの識別子を保持する必要があります。 NDIS は、ミニポート ドライバーに後続の呼び出しの受信キューのキューの id を使用して受信キューで受信フィルターを設定、受信キュー パラメーターを変更または無料の受信キュー。

**注**  既定のキュー (キューの id 0) が常に割り当てられ、解放することはできません。

 

上にあるドライバーは、キュー パラメーターを変更またはキューを解放するなど、NDIS が提供、OID の後続の要求でキューの id を使用する必要があります。 キューの id はすべての OOB データにも含まれています。 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)キューに関連付けられている構造体。 ドライバーを使用して、 [ **NET\_バッファー\_一覧\_受信\_キュー\_ID** ](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-receive-queue-id) NETでキューのidを取得するマクロ\_バッファー\_リスト構造体。

**注**  プロトコル ドライバーは、キューが正常に割り当てられ、キューが削除される前に、いつでもの VMQ フィルターを設定できます。

 

プロトコル ドライバーの問題、 [OID\_受信\_フィルター\_キュー\_割り当て\_完了](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-queue-allocation-complete)メソッド OID 要求のキューの割り当てを完了します。 割り当てが完了すると、ミニポート ドライバーは共有メモリおよびその他のリソースを割り当てることができます。 共有メモリ リソース割り当ての詳細については、次を参照してください。[共有メモリ リソース割り当て](shared-memory-resource-allocation.md)します。

ミニポート後は、ドライバーは OID を受け取ります。\_受信\_フィルター\_キュー\_割り当て OID 要求とハンドルが正常にキュー内にある、 *Allocated*状態。 キューの状態の詳細については、次を参照してください。[キューの状態と操作](queue-states-and-operations.md)します。

これを発行する必要があります、上にあるドライバーを割り当てる後、1 つまたは複数のキューの受信 (および必要に応じて、最初のフィルターを設定) [OID\_受信\_フィルター\_キュー\_割り当て\_完全な](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-queue-allocation-complete)割り当てが受信キューの現在のバッチの完了したミニポート ドライバーに通知する OID 要求を設定します。

フィルターがそのキューに設定されていない場合、ミニポート ドライバーは受信キュー内のすべてのパケットを保持する必要があります。 キューのなかった、フィルターを設定またはすべてのフィルターをクリア、キューを空にする必要があり、すべてのパケットを破棄する必要があります。 ドライバー スタックを示されたまたは、キューに保持されますができません。

後続のドライバーが使用、 [OID\_受信\_フィルター\_FREE\_キュー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue) OID を割り当て、キューを解放します。 キューを解放する方法の詳細については、次を参照してください。 [VM キューの解放](freeing-a-vm-queue.md)します。

 

 






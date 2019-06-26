---
title: OID_RECEIVE_FILTER_GLOBAL_PARAMETERS
description: 上にあるドライバーでは、グローバルを取得する OID_RECEIVE_FILTER_GLOBAL_PARAMETERS の要求がネットワーク アダプターのフィルターのパラメーターを受け取る OID クエリを発行します。
ms.assetid: be6f7210-d1f9-4490-838a-806488df41da
ms.date: 08/08/2017
keywords: -OID_RECEIVE_FILTER_GLOBAL_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 38199a74d053ee45aab50c216be88cce168d1a4c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359223"
---
# <a name="oidreceivefilterglobalparameters"></a>OID\_受信\_フィルター\_GLOBAL\_パラメーター


上にあるドライバーは、OID の OID クエリ要求を発行\_受信\_フィルター\_GLOBAL\_グローバルを取得するパラメーターは、ネットワーク アダプターのフィルターのパラメーターを受信します。

OID のクエリ要求から正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体ポインターが含まれています、 [ **NDIS\_受信\_フィルター\_GLOBAL\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_global_parameters)構造体。

<a name="remarks"></a>注釈
-------

NDIS フィルターが表示される次の NDIS インターフェイスで使用されます。

-   [NDIS パケット結合](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-packet-coalescing)します。 使用する方法の詳細についてはこのインターフェイスでフィルターが表示されるを参照してください[管理パケット結合受信フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/managing-packet-coalescing-receive-filters)します。

-   [シングル ルート I/O 仮想化 (SR-IOV)](https://docs.microsoft.com/windows-hardware/drivers/network/single-root-i-o-virtualization--sr-iov-)します。 使用する方法の詳細についてはこのインターフェイスでフィルターが表示されるを参照してください[仮想ポートで受信フィルターを設定](https://docs.microsoft.com/windows-hardware/drivers/network/setting-a-receive-filter-on-a-virtual-port)します。

-   [バーチャル マシン キュー (VMQ)](https://docs.microsoft.com/windows-hardware/drivers/network/virtual-machine-queue--vmq--in-ndis-6-20)。 使用する方法の詳細についてはこのインターフェイスでフィルターが表示されるを参照してください[設定および VMQ のフィルターをクリアする](https://docs.microsoft.com/windows-hardware/drivers/network/setting-and-clearing-vmq-filters)します。

プロトコル ドライバー以降 NDIS 6.20 が動作では、OID を使用\_受信\_フィルター\_GLOBAL\_パラメーターの現在のグローバル構成パラメーターをクエリには、ネットワーク アダプターでフィルター処理を受信します。 プロトコル ドライバーがこの OID を使用して、受信の種類をフィルター処理するかどうかを判断または受信するなど、キューを有効または無効にします。

### <a name="return-status-codes"></a>リターン状態コード

OID の OID のクエリ要求を処理する NDIS\_受信\_フィルター\_GLOBAL\_ミニポート ドライバー、および次のステータス コードを返します。 1 つのパラメーター。

<a href="" id="ndis-status-success"></a>NDIS\_状態\_成功  
要求は正常に完了しました。

<a href="" id="ndis-status-pending"></a>NDIS\_状態\_PENDING  
完了待ちになっています。 NDIS 渡します最終的な状態コードと結果を呼び出し元の OID 要求の完了ハンドラーに要求が完了した後。

<a href="" id="ndis-status-invalid-length"></a>NDIS\_状態\_無効な\_長さ  
情報バッファーが小さすぎます。 NDIS セット、**データ。クエリ\_情報。BytesNeeded**内のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体に必要な最小バッファー サイズ。

<a href="" id="ndis-status-invalid-parameter"></a>NDIS\_状態\_無効な\_パラメーター  
基になるネットワーク アダプターがサポートされていない機能を有効にしようとした要求が失敗しました。

<a href="" id="ndis-status-failure"></a>NDIS\_状態\_エラー  
他の理由から、要求が失敗しました。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>以降では、NDIS 6.20 が動作をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_RECEIVE\_FILTER\_GLOBAL\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_global_parameters)

 

 





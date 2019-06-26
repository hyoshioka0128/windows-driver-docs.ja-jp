---
title: OID_RECEIVE_FILTER_CURRENT_CAPABILITIES
description: 上にあるドライバーでは、現在有効にするための OID_RECEIVE_FILTER_CURRENT_CAPABILITIES 要求受信ネットワーク アダプターのフィルター機能 OID クエリを発行します。
ms.assetid: bd4f5b9b-e33b-42ba-a430-b3b6108c80b1
ms.date: 08/08/2017
keywords: -OID_RECEIVE_FILTER_CURRENT_CAPABILITIES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 4bcad5c518e36f8f410f3cd1cd826eab7129f11e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371190"
---
# <a name="oidreceivefiltercurrentcapabilities"></a>OID\_受信\_フィルター\_現在\_機能


上にあるドライバーは、OID の OID クエリ要求を発行\_受信\_フィルター\_現在\_現在有効にするための機能は、ネットワーク アダプターのフィルター機能を受信します。

OID のクエリ要求から正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体ポインターが含まれています、 [ **NDIS\_受信\_フィルター\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)構造体。

<a name="remarks"></a>注釈
-------

NDIS フィルターが表示される次の NDIS インターフェイスで使用されます。

-   [NDIS パケット結合](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-packet-coalescing)します。 使用する方法の詳細についてはこのインターフェイスでフィルターが表示されるを参照してください[管理パケット結合受信フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/managing-packet-coalescing-receive-filters)します。

-   [シングル ルート I/O 仮想化 (SR-IOV)](https://docs.microsoft.com/windows-hardware/drivers/network/single-root-i-o-virtualization--sr-iov-)します。 使用する方法の詳細についてはこのインターフェイスでフィルターが表示されるを参照してください[仮想ポートで受信フィルターを設定](https://docs.microsoft.com/windows-hardware/drivers/network/setting-a-receive-filter-on-a-virtual-port)します。

-   [バーチャル マシン キュー (VMQ)](https://docs.microsoft.com/windows-hardware/drivers/network/virtual-machine-queue--vmq--in-ndis-6-20)。 使用する方法の詳細についてはこのインターフェイスでフィルターが表示されるを参照してください[設定および VMQ のフィルターをクリアする](https://docs.microsoft.com/windows-hardware/drivers/network/setting-and-clearing-vmq-filters)します。

受信ネットワーク アダプターのフィルタ リングのハードウェア機能を現在有効なレジスタ NDIS 6.20、以降のミニポート ドライバーとその[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数が呼び出されます。 ミニポート ドライバーでは、次の手順でこれらの機能を登録します。

1.  ドライバーの初期化、 [ **NDIS\_受信\_フィルター\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)構造体で現在有効になっている受信フィルタ リングのハードウェア機能。

2.  ドライバーの初期化、 [ **NDIS\_ミニポート\_アダプター\_ハードウェア\_支援\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)構造と設定、**CurrentReceiveFilterCapabilities**メンバーへのポインターを[ **NDIS\_受信\_フィルター\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)構造体。

3.  ミニポート ドライバーの呼び出し、 [ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)関数とセット、 *MiniportAttributes*パラメーターへのポインターを[ **NDIS\_ミニポート\_アダプター\_ハードウェア\_支援\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)構造体。

OID の OID クエリ要求を発行する上位のプロトコルとフィルター ドライバーがいない\_受信\_フィルター\_現在\_機能します。 NDIS は、現在有効になっている次のようにこれらのドライバーをフィルター処理機能を受け取る用意されています。

-   NDIS には、現在有効な受信でプロトコル ドライバーに関連する、基になるネットワーク アダプターのフィルター処理機能、 **ReceiveFilterCapabilities**のメンバー、 [ **NDIS\_バインド\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)バインド操作中に構造体。

-   NDIS には、現在有効になっている受信のフィルター ドライバーに関連する、基になるネットワーク アダプターのフィルター処理機能、 **ReceiveFilterCapabilities**のメンバー、 [ **NDIS\_フィルター\_アタッチ\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_filter_attach_parameters) attach 操作中に構造体。

### <a name="return-status-codes"></a>リターン状態コード

OID の OID のクエリ要求を処理する NDIS\_受信\_フィルター\_現在\_ミニポート ドライバー、および次のステータス コードを返します。 1 つの機能。

<a href="" id="ndis-status-success"></a>NDIS\_状態\_成功  
要求は正常に完了しました。 **InformationBuffer**を指す、 [ **NDIS\_受信\_フィルター\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)構造体。

<a href="" id="ndis-status-pending"></a>NDIS\_状態\_PENDING  
完了待ちになっています。 NDIS 渡します最終的な状態コードと結果を呼び出し元の OID 要求の完了ハンドラーに、要求が完了した後。

<a href="" id="ndis-status-invalid-length"></a>NDIS\_状態\_無効な\_長さ  
情報バッファーが小さすぎます。 NDIS セット、**データ。クエリ\_情報。BytesNeeded**内のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体に必要な最小バッファー サイズ。

<a href="" id="ndis-status-not-supported"></a>NDIS\_状態\_いない\_サポートされています。  
ネットワーク アダプターがサポートしていない受信フィルター処理します。

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


[**NDIS\_バインド\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)

[**NDIS\_ミニポート\_アダプター\_ハードウェア\_支援\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_受信\_フィルター\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)

 

 





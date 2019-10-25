---
title: OID_RECEIVE_FILTER_CURRENT_CAPABILITIES
description: 後続のドライバーは、ネットワークアダプターの現在有効な受信フィルター機能を取得するために、OID_RECEIVE_FILTER_CURRENT_CAPABILITIES の OID クエリ要求を発行します。
ms.assetid: bd4f5b9b-e33b-42ba-a430-b3b6108c80b1
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_RECEIVE_FILTER_CURRENT_CAPABILITIES ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: a30d9be370ff0a2ce4cb0dfa5d44c7aecf32e05e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844017"
---
# <a name="oid_receive_filter_current_capabilities"></a>OID\_現在の\_機能\_受信\_フィルター処理


これまでのドライバーは oid クエリ要求 oid を発行\_、現在の\_機能を受信\_フィルター\_処理して、現在有効になっているネットワークアダプターの受信フィルター機能を取得します。

OID クエリ要求から正常に返された後、 [**ndis\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、 [**ndis\_受信\_フィルター\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)へのポインターが含まれています。データ.

<a name="remarks"></a>注釈
-------

NDIS 受信フィルターは、次の NDIS インターフェイスで使用されます。

-   [NDIS パケット合体](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-packet-coalescing)。 このインターフェイスで受信フィルターを使用する方法の詳細については、「[パケット合体受信フィルターの管理](https://docs.microsoft.com/windows-hardware/drivers/network/managing-packet-coalescing-receive-filters)」を参照してください。

-   [シングルルート I/o 仮想化 (sr-iov)](https://docs.microsoft.com/windows-hardware/drivers/network/single-root-i-o-virtualization--sr-iov-)。 このインターフェイスで受信フィルターを使用する方法の詳細については、「[仮想ポートでの受信フィルターの設定](https://docs.microsoft.com/windows-hardware/drivers/network/setting-a-receive-filter-on-a-virtual-port)」を参照してください。

-   [仮想マシン キュー (VMQ)](https://docs.microsoft.com/windows-hardware/drivers/network/virtual-machine-queue--vmq--in-ndis-6-20)。 このインターフェイスで受信フィルターを使用する方法の詳細については、「 [VMQ フィルターの設定とクリア](https://docs.microsoft.com/windows-hardware/drivers/network/setting-and-clearing-vmq-filters)」を参照してください。

NDIS 6.20 以降、ミニポートドライバーは、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数が呼び出されたときに、ネットワークアダプターの現在有効になっている受信フィルター処理ハードウェア機能を登録します。 ミニポートドライバーは、次の手順に従ってこれらの機能を登録します。

1.  このドライバーは、現在有効になっている受信フィルターのハードウェア機能を使用して、 [ **\_フィルター\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)の構造を受信する NDIS\_を初期化します。

2.  このドライバーは、 [**ndis\_ミニポート\_アダプター\_ハードウェア\_サポートし\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)構造を提供し、 **Currentreceivefiltercapabilities**メンバーを[**ndis\_RECEIVE へのポインターに設定します。\_フィルター\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)の構造です。

3.  ミニポートドライバーは、 [**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)関数を呼び出し、 *miniportattributes*パラメーターを NDIS\_ミニポート\_アダプターへのポインターに設定します[ **\_ハードウェア\_サポート\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)データ.

プロトコルドライバーとフィルタードライバーは、現在の\_の機能\_受信\_フィルターを受け取る oid のクエリ要求を\_発行する必要はありません。 NDIS は、次のように、これらのドライバーに対して現在有効になっている受信フィルター処理機能を提供します。

-   NDIS では、基になるネットワークアダプターの現在有効になっている受信フィルター機能を、 [**ndis\_\_BIND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)の**receivefiltercapabilities**メンバー内のプロトコルドライバーに提供します。バインド操作です。

-   NDIS は、基になるネットワークアダプターの現在有効になっている受信フィルター機能を、Ndis\_フィルターの**Receivefiltercapabilities**メンバー内のフィルタードライバーに追加して、 [ **\_パラメーターをアタッチ\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)ます。アタッチ操作中の構造体。

### <a name="return-status-codes"></a>ステータスコードを返す

NDIS は、\_oid の OID クエリ要求を処理し、ミニポートドライバーの現在の\_機能\_受信\_フィルター処理して、次のいずれかのステータスコードを返します。

<a href="" id="ndis-status-success"></a>NDIS\_状態\_成功  
要求は正常に完了しました。 **Informationbuffer**は、 [ **\_フィルター\_機能の構造を受け取る NDIS\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)を参照します。

<a href="" id="ndis-status-pending"></a>NDIS\_状態\_保留中  
要求は完了待ちです。 NDIS は、要求が完了した後に、最終的なステータスコードと結果を呼び出し元の OID 要求完了ハンドラーに渡します。

<a href="" id="ndis-status-invalid-length"></a>NDIS\_の状態\_無効な\_の長さです  
情報バッファーが短すぎます。 NDIS はデータを設定**します。クエリ\_情報。** 必要な最小バッファーサイズに対して、 [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体のメンバーが必要です。

<a href="" id="ndis-status-not-supported"></a>NDIS\_の状態\_\_サポートされていません  
ネットワークアダプターは、受信フィルター処理をサポートしていません。

<a href="" id="ndis-status-failure"></a>NDIS\_状態\_エラー  
他の理由で要求が失敗しました。

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
<td><p>NDIS 6.20 以降でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_バインド\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)

[**NDIS\_ミニポート\_アダプター\_ハードウェア\_サポート\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_受信\_フィルター\_の機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)

 

 





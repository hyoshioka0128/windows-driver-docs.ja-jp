---
title: OID_RECEIVE_FILTER_HARDWARE_CAPABILITIES
description: 後続のドライバーは、ネットワークアダプターの受信フィルター処理ハードウェア機能を取得するために、OID_RECEIVE_FILTER_HARDWARE_CAPABILITIES の OID クエリ要求を発行します。
ms.assetid: 2b80944e-5309-4cb0-a69a-331f8fd3f7a4
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_RECEIVE_FILTER_HARDWARE_CAPABILITIES
ms.localizationpriority: medium
ms.openlocfilehash: 596f198e3252a7a365d07a436dabd1cc1ce893c5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844007"
---
# <a name="oid_receive_filter_hardware_capabilities"></a>OID\_ハードウェア\_機能\_\_フィルターを受け取る


これまでのドライバーは oid クエリ要求 oid を発行\_、ハードウェア\_機能を受信\_フィルター\_処理して、ネットワークアダプターの受信フィルター処理ハードウェア機能を取得します。

OID クエリ要求から正常に戻った後、 [**ndis\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、[**ndis\_RECEIVE\_FILTER\_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)構造体へのポインターが含まれています。

<a name="remarks"></a>注釈
-------

NDIS 受信フィルターは、次の NDIS インターフェイスで使用されます。

-   [NDIS パケット合体](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-packet-coalescing)。 このインターフェイスで受信フィルターを使用する方法の詳細については、「[パケット合体受信フィルターの管理](https://docs.microsoft.com/windows-hardware/drivers/network/managing-packet-coalescing-receive-filters)」を参照してください。

-   [シングルルート I/o 仮想化 (sr-iov)](https://docs.microsoft.com/windows-hardware/drivers/network/single-root-i-o-virtualization--sr-iov-)。 このインターフェイスで受信フィルターを使用する方法の詳細については、「[仮想ポートでの受信フィルターの設定](https://docs.microsoft.com/windows-hardware/drivers/network/setting-a-receive-filter-on-a-virtual-port)」を参照してください。

-   [仮想マシン キュー (VMQ)](https://docs.microsoft.com/windows-hardware/drivers/network/virtual-machine-queue--vmq--in-ndis-6-20)。 このインターフェイスで受信フィルターを使用する方法の詳細については、「 [VMQ フィルターの設定とクリア](https://docs.microsoft.com/windows-hardware/drivers/network/setting-and-clearing-vmq-filters)」を参照してください。

[**NDIS\_受信\_フィルター\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)の構造には、ネットワークアダプターの受信フィルターハードウェア機能に関する情報が含まれています。 これらの機能には、現在 INF ファイルの設定によって無効になっているハードウェア機能や、 **[詳細設定**] プロパティページがあります。

**注**  ネットワークアダプターのすべての受信フィルター処理ハードウェア機能は、機能が有効になっているか無効になっているかに関係なく、\_フィルター\_ハードウェア\_機能\_受信する oid クエリ要求によって返されます。

 

NDIS 6.20 以降、ミニポートドライバーは、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数が呼び出されたときに、ネットワークアダプターの現在有効になっている受信フィルター処理ハードウェア機能を登録します。 ミニポートドライバーは、次の手順に従ってこれらの機能を登録します。

1.  このドライバーは、受信フィルター処理ハードウェア機能を使用して、 [ **\_フィルター\_機能の構造を受け取る NDIS\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)を初期化します。

2.  このドライバーは、 [**ndis\_ミニポート\_アダプター\_ハードウェア\_サポートし\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)の構造体を初期化し、 **Currentreceivefiltercapabilities**メンバーを[**ndis\_RECEIVE\_FILTER\_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)構造体へのポインターに設定します。

3.  ミニポートドライバーは、 [**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)関数を呼び出し、 *miniportattributes*パラメーターを[**NDIS\_ミニポート\_アダプター\_ハードウェア\_サポート\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)構造へのポインターに設定します。

### <a name="return-status-codes"></a>ステータスコードを返す

NDIS は、\_oid の OID クエリ要求を処理し、ミニポートドライバーのハードウェア\_機能\_を受信\_フィルター処理して、次のいずれかのステータスコードを返します。

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

 

 





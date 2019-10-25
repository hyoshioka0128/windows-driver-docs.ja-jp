---
title: OID_RECEIVE_FILTER_GLOBAL_PARAMETERS
description: その後のドライバーは、ネットワークアダプターのグローバル受信フィルターパラメーターを取得するために、OID_RECEIVE_FILTER_GLOBAL_PARAMETERS の OID クエリ要求を発行します。
ms.assetid: be6f7210-d1f9-4490-838a-806488df41da
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_RECEIVE_FILTER_GLOBAL_PARAMETERS ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 5d5d7bb47fce54f51b0b6a26b41c7d13e669ed62
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844010"
---
# <a name="oid_receive_filter_global_parameters"></a>グローバル\_パラメーター\_\_フィルターを受け取る OID\_


これまでのドライバーは oid クエリ要求 oid を発行\_、グローバル\_パラメーター\_受信\_フィルターを適用して、ネットワークアダプターのグローバル受信フィルターパラメーターを取得します。

OID クエリ要求から正常に返された後、 [**ndis\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、ndis へのポインターが含まれています。これには、 [ **\_グローバル\_\_受信\_フィルターが含まれPARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_global_parameters)構造体。

<a name="remarks"></a>注釈
-------

NDIS 受信フィルターは、次の NDIS インターフェイスで使用されます。

-   [NDIS パケット合体](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-packet-coalescing)。 このインターフェイスで受信フィルターを使用する方法の詳細については、「[パケット合体受信フィルターの管理](https://docs.microsoft.com/windows-hardware/drivers/network/managing-packet-coalescing-receive-filters)」を参照してください。

-   [シングルルート I/o 仮想化 (sr-iov)](https://docs.microsoft.com/windows-hardware/drivers/network/single-root-i-o-virtualization--sr-iov-)。 このインターフェイスで受信フィルターを使用する方法の詳細については、「[仮想ポートでの受信フィルターの設定](https://docs.microsoft.com/windows-hardware/drivers/network/setting-a-receive-filter-on-a-virtual-port)」を参照してください。

-   [仮想マシン キュー (VMQ)](https://docs.microsoft.com/windows-hardware/drivers/network/virtual-machine-queue--vmq--in-ndis-6-20)。 このインターフェイスで受信フィルターを使用する方法の詳細については、「 [VMQ フィルターの設定とクリア](https://docs.microsoft.com/windows-hardware/drivers/network/setting-and-clearing-vmq-filters)」を参照してください。

NDIS 6.20 以降では、プロトコルドライバーは、グローバル\_パラメーター\_受信\_フィルターを使用して、ネットワークアダプターの受信フィルター処理のために現在のグローバル構成パラメーターを照会\_ます。 たとえば、プロトコルドライバーは、この OID を使用して、受信フィルターの種類または受信キューを有効にするか無効にするかを決定できます。

### <a name="return-status-codes"></a>ステータスコードを返す

NDIS は、ミニポートドライバーのグローバル\_パラメーター\_受信\_フィルター処理する oid の OID クエリ要求を処理し、次のいずれかのステータスコードを返します\_します。

<a href="" id="ndis-status-success"></a>NDIS\_状態\_成功  
要求は正常に完了しました。

<a href="" id="ndis-status-pending"></a>NDIS\_状態\_保留中  
要求は完了待ちです。 NDIS は、要求が完了した後に、最終的なステータスコードと結果を呼び出し元の OID 要求完了ハンドラーに渡します。

<a href="" id="ndis-status-invalid-length"></a>NDIS\_の状態\_無効な\_の長さです  
情報バッファーが短すぎます。 NDIS はデータを設定**します。クエリ\_情報。** 必要な最小バッファーサイズに対して、 [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体のメンバーが必要です。

<a href="" id="ndis-status-invalid-parameter"></a>NDIS\_の状態\_無効な\_パラメーターです  
基になるネットワークアダプターでサポートされていない機能を有効にしようとしたため、要求は失敗しました。

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


[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_グローバル\_パラメーター\_を受け取る\_フィルター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_global_parameters)

 

 





---
title: OID_RECEIVE_FILTER_ENUM_FILTERS
description: ネットワークアダプターに構成されているすべてのフィルターの一覧を取得するために、OID_RECEIVE_FILTER_ENUM_FILTERS の OID メソッド要求を発行しているドライバーがあります。
ms.assetid: 498c1e96-c3ee-4f5d-b0f2-6e88921187e5
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_RECEIVE_FILTER_ENUM_FILTERS ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 5752c74412f3150fbe2b2153d3234b0b40eb7897
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844011"
---
# <a name="oid_receive_filter_enum_filters"></a>OID\_受信\_フィルター\_列挙型\_フィルター


ネットワークアダプター上で構成されているすべてのフィルターの一覧を取得するために、その後のドライバーが oid の OID メソッド要求を発行して、列挙\_フィルター\_列挙型フィルターを\_\_します。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_受信\_フィルター\_情報\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)構造体へのポインターが含まれています。

OID メソッド要求から正常に戻った後、 [**NDIS\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、バッファーへのポインターが含まれています。 このバッファーは、次のものが含まれるように書式設定されます。

-   NDIS\_は、ミニポートドライバーで現在構成されている受信フィルターの一覧を指定する[ **\_フィルター\_情報\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)構造体を受け取ります。

-   [ **\_フィルター\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info)の構造体を受け取る NDIS\_の配列。 各構造体は、現在ミニポートドライバーで構成されている受信フィルターのパラメーターを指定します。

<a name="remarks"></a>注釈
-------

NDIS 受信フィルターは、次の NDIS インターフェイスで使用されます。

-   [NDIS パケット合体](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-packet-coalescing)。 このインターフェイスで受信フィルターを使用する方法の詳細については、「[パケット合体受信フィルターの管理](https://docs.microsoft.com/windows-hardware/drivers/network/managing-packet-coalescing-receive-filters)」を参照してください。

-   [シングルルート I/o 仮想化 (sr-iov)](https://docs.microsoft.com/windows-hardware/drivers/network/single-root-i-o-virtualization--sr-iov-)。 このインターフェイスで受信フィルターを使用する方法の詳細については、「[仮想ポートでの受信フィルターの設定](https://docs.microsoft.com/windows-hardware/drivers/network/setting-a-receive-filter-on-a-virtual-port)」を参照してください。

-   [仮想マシン キュー (VMQ)](https://docs.microsoft.com/windows-hardware/drivers/network/virtual-machine-queue--vmq--in-ndis-6-20)。 このインターフェイスで受信フィルターを使用する方法の詳細については、「 [VMQ フィルターの設定とクリア](https://docs.microsoft.com/windows-hardware/drivers/network/setting-and-clearing-vmq-filters)」を参照してください。

それ以降のドライバーまたはアプリケーションは、oid による OID メソッド要求を発行\_、列挙\_フィルター\_列挙型フィルターを\_受信して、ネットワークアダプターに設定されている受信フィルターを列挙します。 これには、SR-IOV 仮想ポート (VPort) または VMQ 受信キューで設定された受信フィルターが含まれます。

### <a name="additional-guidelines-for-the-ndis-packet-coalescing-interface"></a>NDIS パケット合体インターフェイスに関する追加のガイドライン

Windows Server 2012 以降では、NDIS パケット合体はネットワークアダプターの既定の受信キューのみをサポートしています。

パケット合体受信フィルターを列挙するには、その後のドライバーで、Ndis の**Queueid**メンバーを設定する必要があります。これは、 [ **\_情報\_配列構造の\_フィルター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)を ndis に受信する\_、既定\_受信\_\_キュー\_ID。

### <a name="additional-guidelines-for-the-sr-iov-interface"></a>Sr-iov インターフェイスに関するその他のガイドライン

Windows Server 2012 以降の sr-iov インターフェイスでは、仮想ポート (VPort) の既定の受信キューのみがサポートされています。

VPort 受信フィルターを列挙するには、前のドライバーで、Ndis の**Queueid**メンバーを設定する必要があります。この場合、 [ **\_INFO\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)構造を NDIS\_DEFAULT\_RECEIVE\_QUEUE に受信\_フィルターを\_\_ID。

### <a name="additional-guidelines-for-the-vmq-interface"></a>VMQ インターフェイスに関する追加のガイドライン

それより後のドライバーは oid の OID メソッド要求を発行して、\_フィルター\_列挙\_フィルターを使用して、VMQ 受信キューに設定された受信フィルターを列挙\_ことができます。 前のドライバーによって NDIS が初期化されると、 [ **\_\_フィルター\_情報\_配列構造が受信さ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)れ、 **queueid**メンバーが次のいずれかの値に設定されます。

-   既定以外の受信キューのキュー識別子の値。 これまでのドライバーは、以前の oid メソッド要求からキュー識別子の入力値を取得して、\_キューまたは oid の OID クエリ要求[\_\_フィルター](oid-receive-filter-allocate-queue.md)を受け取ることによって、 [\_フィルターを受信\_\_します。8_ 列挙\_キュー](oid-receive-filter-enum-queues.md)です。

-   既定の受信キューを指定する、NDIS\_のキュー識別子の値\_既定では\_キュー\_ID が使用されます。

### <a name="return-status-codes"></a>ステータスコードを返す

NDIS は、OID の OID メソッド要求を処理します。これは、ミニポートドライバーのフィルター\_列挙\_フィルターを受信\_フィルターを\_、次のいずれかのステータスコードを返します。

<a href="" id="ndis-status-success"></a>NDIS\_状態\_成功  
要求は正常に完了しました。 **Informationbuffer**は、 [ **\_フィルター\_情報\_配列構造を受け取る NDIS\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)を指します。

<a href="" id="ndis-status-pending"></a>NDIS\_状態\_保留中  
要求は完了待ちです。 NDIS は、要求が完了した後に、最終的なステータスコードと結果を呼び出し元の OID 要求完了ハンドラーに渡します。

<a href="" id="ndis-status-invalid-length"></a>NDIS\_の状態\_無効な\_の長さです  
情報バッファーが短すぎます。 NDIS はデータを設定**します。クエリ\_情報。** 必要な最小バッファーサイズに対して、 [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体のメンバーが必要です。

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

[**NDIS\_受信\_フィルター\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info)

[**NDIS\_受信\_フィルター\_情報\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)

[OID\_受信\_フィルター\_割り当て\_キュー](oid-receive-filter-allocate-queue.md)

[OID\_受信\_フィルター\_列挙型\_キュー](oid-receive-filter-enum-queues.md)

[OID\_受信\_フィルター\_設定\_フィルター](oid-receive-filter-set-filter.md)

 

 





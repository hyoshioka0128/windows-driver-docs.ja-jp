---
title: OID_RECEIVE_FILTER_PARAMETERS
description: ネットワークアダプター上のフィルターの現在の構成パラメーターを取得するために、OID_RECEIVE_FILTER_PARAMETERS の OID メソッド要求を発行しているドライバーがあります。
ms.assetid: 1bb12945-0dad-47b9-9f44-e05efe292979
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_RECEIVE_FILTER_PARAMETERS ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: d971f7c9722fd89e0b2cc62aad3e5a38507266ad
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844001"
---
# <a name="oid_receive_filter_parameters"></a>OID\_受信\_フィルター\_パラメーター


ネットワークアダプター上のフィルターの現在の構成パラメーターを取得するために、\_フィルター\_パラメーターを受け取る oid の OID メソッド要求が、後のドライバーによって発行され\_。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_受信\_フィルター\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)構造体へのポインターが含まれています。 NDIS では、入力構造の**Filterid**メンバーを使用してフィルターを識別します。

OID メソッド要求から正常に戻った後、 [**NDIS\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、バッファーへのポインターが含まれています。 このバッファーは、次のものが含まれるように書式設定されます。

-   Ndis\_は、NDIS 受信フィルターのパラメーターを指定する[ **\_フィルター\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)構造を受け取ります。

-   ネットワークパケットヘッダー内のフィールドのフィルターテスト条件を指定する、 [ **\_フィルター\_フィールド\_パラメーター構造を受け取る NDIS\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)の配列。

<a name="remarks"></a>注釈
-------

NDIS 受信フィルターは、次の NDIS インターフェイスで使用されます。

-   [NDIS パケット合体](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-packet-coalescing)。 このインターフェイスで受信フィルターを使用する方法の詳細については、「[パケット合体受信フィルターの管理](https://docs.microsoft.com/windows-hardware/drivers/network/managing-packet-coalescing-receive-filters)」を参照してください。

-   [シングルルート I/o 仮想化 (sr-iov)](https://docs.microsoft.com/windows-hardware/drivers/network/single-root-i-o-virtualization--sr-iov-)。 このインターフェイスで受信フィルターを使用する方法の詳細については、「[仮想ポートでの受信フィルターの設定](https://docs.microsoft.com/windows-hardware/drivers/network/setting-a-receive-filter-on-a-virtual-port)」を参照してください。

-   [仮想マシン キュー (VMQ)](https://docs.microsoft.com/windows-hardware/drivers/network/virtual-machine-queue--vmq--in-ndis-6-20)。 このインターフェイスで受信フィルターを使用する方法の詳細については、「 [VMQ フィルターの設定とクリア](https://docs.microsoft.com/windows-hardware/drivers/network/setting-and-clearing-vmq-filters)」を参照してください。

これまでのドライバーは oid メソッドの oid 要求を発行\_、ネットワークアダプターに設定されている受信フィルターの構成パラメーターを取得するために\_パラメーターを受信\_フィルター処理します。 これには、VMQ 受信キューまたは SR-IOV 仮想ポート (VPort) に設定された受信フィルターと、ミニポートドライバーにダウンロードされたパケット合体フィルターが含まれます。

これまでのドライバーは、以前の oid メソッドの oid 要求からフィルター id を取得し、 [\_フィルターを設定](oid-receive-filter-set-filter.md)するか、oid の oid 要求からフィルター [\_列挙型\_受信\_フィルター\_列挙\_設定されたフィルター識別子を受信し\_\_ます。フィルター](oid-receive-filter-enum-filters.md)。

### <a name="return-status-codes"></a>ステータスコードを返す

NDIS は、ミニポートドライバーのパラメーター\_フィルター\_パラメーターを受け取る OID の OID 要求を処理し、次のステータスコードのいずれかを返します\_します。

<a href="" id="ndis-status-success"></a>NDIS\_状態\_成功  
要求は正常に完了しました。 **Informationbuffer**は、 [ **\_フィルター\_PARAMETERS 構造体を受け取る NDIS\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)を指します。

<a href="" id="ndis-status-pending"></a>NDIS\_状態\_保留中  
要求は完了待ちです。 NDIS は、要求が完了した後に、最終的なステータスコードと結果を呼び出し元の OID 要求完了ハンドラーに渡します。

<a href="" id="ndis-status-invalid-parameter"></a>NDIS\_の状態\_無効な\_パラメーターです  
前のドライバーまたはアプリケーションに無効なフィルター識別子が指定されました。 フィルター識別子は、0の場合、または未定義のフィルターを指定した場合は無効です。

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

[OID\_受信\_フィルター\_列挙型\_フィルター](oid-receive-filter-enum-filters.md)

[**NDIS\_受信\_フィルター\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)

[OID\_受信\_フィルター\_設定\_フィルター](oid-receive-filter-set-filter.md)

 

 





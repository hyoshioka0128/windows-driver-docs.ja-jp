---
title: OID_RECEIVE_FILTER_ENUM_FILTERS
description: 上にある、ドライバーは、ネットワーク アダプターで構成されているすべてのフィルターの一覧を取得する OID_RECEIVE_FILTER_ENUM_FILTERS の OID メソッド要求を発行します。
ms.assetid: 498c1e96-c3ee-4f5d-b0f2-6e88921187e5
ms.date: 08/08/2017
keywords: -OID_RECEIVE_FILTER_ENUM_FILTERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 4eead4c8515dad96047aad47035da06f5304752b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349415"
---
# <a name="oidreceivefilterenumfilters"></a>OID\_受信\_フィルター\_ENUM\_フィルター


OID の OID メソッド要求を発行する上位のドライバー\_受信\_フィルター\_ENUM\_ネットワーク アダプターで構成されているすべてのフィルターの一覧を取得するフィルター。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、 [ **NDIS\_受信\_フィルター\_情報\_配列**](https://msdn.microsoft.com/library/windows/hardware/ff567179)構造体。

OID メソッドの要求から正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体バッファーへのポインターが含まれています。 このバッファーは、以下を格納する形式です。

-   [ **NDIS\_受信\_フィルター\_情報\_配列**](https://msdn.microsoft.com/library/windows/hardware/ff567179)で現在構成されている受信フィルターの一覧を指定する構造体、ミニポート ドライバー。

-   配列の[ **NDIS\_受信\_フィルター\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff567176)構造体。 各構造体には、ミニポート ドライバーで現在構成されている受信フィルターのパラメーターを指定します。

<a name="remarks"></a>注釈
-------

NDIS フィルターが表示される次の NDIS インターフェイスで使用されます。

-   [NDIS パケット結合](https://msdn.microsoft.com/library/windows/hardware/hh451601)します。 使用する方法の詳細についてはこのインターフェイスでフィルターが表示されるを参照してください[管理パケット結合受信フィルター](https://msdn.microsoft.com/library/windows/hardware/hh464026)します。

-   [シングル ルート I/O 仮想化 (SR-IOV)](https://msdn.microsoft.com/library/windows/hardware/hh440235)します。 使用する方法の詳細についてはこのインターフェイスでフィルターが表示されるを参照してください[仮想ポートで受信フィルターを設定](https://msdn.microsoft.com/library/windows/hardware/hh440224)します。

-   [バーチャル マシン キュー (VMQ)](https://msdn.microsoft.com/library/windows/hardware/ff571035)。 使用する方法の詳細についてはこのインターフェイスでフィルターが表示されるを参照してください[設定および VMQ のフィルターをクリアする](https://msdn.microsoft.com/library/windows/hardware/ff570780)します。

上にあるドライバーやアプリケーションは、OID の OID メソッド要求を発行\_受信\_フィルター\_ENUM\_ネットワーク アダプターに設定された受信フィルターを列挙するフィルター。 これが含まれています、SR-IOV 仮想ポート (VPort) に設定されたフィルターを受信または、VMQ キューの受信します。

### <a name="additional-guidelines-for-the-ndis-packet-coalescing-interface"></a>インターフェイスを結合する NDIS パケットに関する追加のガイドライン

Windows Server 2012、結合のみをサポートする NDIS パケット以降で既定の受信ネットワーク アダプターのキューに登録します。

パケットを列挙する結合フィルターを受信上にあるドライバーを設定する必要があります、 **QueueId**のメンバー、 [ **NDIS\_受信\_フィルター\_情報\_配列**](https://msdn.microsoft.com/library/windows/hardware/ff567179) NDIS 構造\_既定\_受信\_キュー\_id。

### <a name="additional-guidelines-for-the-sr-iov-interface"></a>SR-IOV インターフェイスに関する追加のガイドライン

既定の仮想ポート (VPort) のキュー受信以降では、Windows Server 2012、SR-IOV インターフェイスのみをサポートします。

VPort を列挙するためにフィルターが表示される、上にあるドライバーを設定する必要があります、 **QueueId**のメンバー、 [ **NDIS\_受信\_フィルター\_情報\_配列**](https://msdn.microsoft.com/library/windows/hardware/ff567179) NDIS 構造\_既定\_受信\_キュー\_id。

### <a name="additional-guidelines-for-the-vmq-interface"></a>VMQ インターフェイスに関する追加のガイドライン

上にある、ドライバーは、OID の OID メソッド要求を発行できます\_受信\_フィルター\_ENUM\_受信キューに、VMQ に設定された受信フィルターを列挙するフィルター。 上にあるドライバーを初期化すると、 [ **NDIS\_受信\_フィルター\_情報\_配列**](https://msdn.microsoft.com/library/windows/hardware/ff567179)設定構造、 **QueueId**値は次のいずれかにメンバー。

-   既定以外のキューの識別子の値には、キューが表示されます。 上にあるドライバーの以前の OID メソッド要求からキューの識別子の入力値を取得した[OID\_受信\_フィルター\_ALLOCATE\_キュー](oid-receive-filter-allocate-queue.md)またはの OID のクエリ要求[OID\_受信\_フィルター\_ENUM\_キュー](oid-receive-filter-enum-queues.md)します。

-   キューの識別子値 NDIS\_既定\_受信\_キュー\_ID で、既定の受信キューを指定します。

### <a name="return-status-codes"></a>リターン状態コード

OID の OID メソッド要求を処理する NDIS\_受信\_フィルター\_ENUM\_ミニポート ドライバー、および次のステータス コードを返します。 1 つのフィルター。

<a href="" id="ndis-status-success"></a>NDIS\_状態\_成功  
要求は正常に完了しました。 **InformationBuffer**を指す、 [ **NDIS\_受信\_フィルター\_情報\_配列**](https://msdn.microsoft.com/library/windows/hardware/ff567179)構造体。

<a href="" id="ndis-status-pending"></a>NDIS\_状態\_PENDING  
完了待ちになっています。 NDIS 渡します最終的な状態コードと結果を呼び出し元の OID 要求の完了ハンドラーに、要求が完了した後。

<a href="" id="ndis-status-invalid-length"></a>NDIS\_状態\_無効な\_長さ  
情報バッファーが小さすぎます。 NDIS セット、**データ。クエリ\_情報。BytesNeeded**内のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体に必要な最小バッファー サイズ。

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


[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_受信\_フィルター\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff567176)

[**NDIS\_受信\_フィルター\_情報\_配列**](https://msdn.microsoft.com/library/windows/hardware/ff567179)

[OID\_受信\_フィルター\_ALLOCATE\_キュー](oid-receive-filter-allocate-queue.md)

[OID\_受信\_フィルター\_ENUM\_キュー](oid-receive-filter-enum-queues.md)

[OID\_受信\_フィルター\_設定\_フィルター](oid-receive-filter-set-filter.md)

 

 





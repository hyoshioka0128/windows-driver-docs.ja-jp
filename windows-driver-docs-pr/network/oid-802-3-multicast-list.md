---
title: OID_802_3_MULTICAST_LIST
description: セットの要求として NDIS と上位のプロトコル ドライバーはミニポート アダプターの現在のマルチキャスト アドレスの一覧を置換するのに OID_802_3_MULTICAST_LIST OID 要求を使用します。
ms.assetid: 601f38e1-26ae-4d72-9d72-91bd58f81bba
ms.date: 08/08/2017
keywords: -OID_802_3_MULTICAST_LIST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: cc96f2f9a32a4c440ca80502809389dda12f029c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360244"
---
# <a name="oid8023multicastlist"></a>OID\_802\_3\_マルチキャスト\_一覧


セットの要求では、NDIS と上位のプロトコルのドライバーを使用、OID\_802\_3\_マルチキャスト\_一覧 OID ミニポート アダプターの現在のマルチキャスト アドレスの一覧を交換するよう依頼します。 アドレスがリストに存在する場合は、マルチキャスト パケットの受信には、そのアドレスは有効になっています。

NDIS およびプロトコルのドライバーが、OID を使用するクエリの要求として\_802\_3\_マルチキャスト\_一覧 OID 要求の現在のマルチキャスト アドレスの一覧を取得します。




NDIS 処理 OID\_802\_3\_マルチキャスト\_リスト クエリのクエリ要求のミニポート ドライバーは、ミニポート ドライバーこれら受信しないように要求します。

マルチキャスト アドレスのリストをサポートするミニポート ドライバーは、OID をサポートする必要があります\_802\_3\_マルチキャスト\_一覧は、要求を設定します。

セットの要求を**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造にはとしてマルチキャスト アドレスの一覧が含まれています、アドレスの配列。

-   各アドレスは、6 バイトの配列です。
-   **InformationBufferLength**メンバーがの長さ (バイト単位) を含む、 **InformationBuffer**配列。
-   リストに重複するアドレスがある場合、 **InformationBuffer**メンバー、NDIS、OID を送信する前に重複は削除\_802\_3\_マルチキャスト\_リストに要求を設定します。ミニポート ドライバー。
-   場合、 **InformationBufferLength**メンバーが 0 で、ミニポート ドライバーは、マルチキャスト アドレスの一覧をクリアする必要があります。
-   場合、 **InformationBufferLength**メンバーが 0 より大きい、ミニポート ドライバーが一覧に既存のマルチキャスト アドレス一覧を置き換える必要があります、 **InformationBuffer**メンバー。

ミニポート アダプタのマルチキャスト アドレスの一覧は、ミニポート アダプターにバインドされているすべてのプロトコル ドライバーで共有されます。 NDIS は、この一覧へのアクセスを制御します。 NDIS がまとめて 1 つの OID の要求を複数のプロトコル ドライバーは、同時に、リストを変更すると、\_802\_3\_マルチキャスト\_リスト設定要求は、ミニポート ドライバーに送信します。

ミニポート アダプターが初期化されるときに、マルチキャスト アドレスの一覧がゼロであるために、NIC をリセットします。 プロトコル ドライバーにマルチキャスト パケットの受信を許可しないように、NDIS はまた、パケット フィルターを初期化します。

マルチキャスト パケットを受信するには、プロトコル ドライバーに行う必要があります後で、次のいずれか。

-   パケット フィルターを設定、 **NDIS\_パケット\_型\_マルチキャスト**フラグ。 いつでも、このフラグをキャンセルすることでマルチキャスト パケットの受信を無効にしても。 プロトコル ドライバーにマルチキャスト パケットの受信ができるようにする順序は重要ではありません。 詳細については、次を参照してください。、 [OID\_GEN\_現在\_パケット\_フィルター](oid-gen-current-packet-filter.md) OID 要求。
-   パケット フィルターを設定、 **NDIS\_パケット\_型\_すべて\_マルチキャスト**フラグ、すべてのマルチキャスト パケットを有効にして、フィルター自体を実行します。

ミニポート ドライバーは、マルチキャスト アドレスの一覧に含めることができるマルチキャスト アドレスの数に上限を設定することができます。 NDIS 返します**NDIS\_状態\_マルチキャスト\_完全**プロトコル ドライバーがこの制限を超えた場合、または無効なマルチキャスト アドレスを指定する場合。

クエリ要求の場合は、NDIS は、すべてのプロトコル バインドのすべてのマルチキャスト アドレス リストの和集合を表すマルチキャスト アドレス一覧を返します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_802\_3\_追加\_マルチキャスト\_アドレス](oid-802-3-add-multicast-address.md)

[OID\_802\_3\_削除\_マルチキャスト\_アドレス](oid-802-3-delete-multicast-address.md)

[OID\_802\_3\_最大\_一覧\_サイズ](oid-802-3-maximum-list-size.md)

[OID\_GEN\_現在\_パケット\_フィルター](oid-gen-current-packet-filter.md)

 

 





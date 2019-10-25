---
title: OID_802_3_MULTICAST_LIST
description: 設定要求として、NDIS およびそれ以降のプロトコルドライバーは、OID_802_3_MULTICAST_LIST OID 要求を使用して、ミニポートアダプターの現在のマルチキャストアドレス一覧を置き換えます。
ms.assetid: 601f38e1-26ae-4d72-9d72-91bd58f81bba
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_802_3_MULTICAST_LIST ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 39e6ff3725355fdc798e6b2d01a127dd0416470a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834552"
---
# <a name="oid_802_3_multicast_list"></a>OID\_802\_3\_マルチキャスト\_リスト


設定要求として、NDIS およびそれ以降のプロトコルドライバーは、OID\_802\_3\_マルチキャスト\_リスト OID 要求を使用して、ミニポートアダプターの現在のマルチキャストアドレスリストを置き換えます。 アドレスが一覧に存在する場合、そのアドレスはマルチキャストパケットを受信できるようになります。

NDIS およびプロトコルドライバーは、クエリ要求として OID\_802\_3\_マルチキャスト\_リスト OID 要求を使用して、現在のマルチキャストアドレスリストを取得します。




NDIS は OID\_802\_3\_マルチキャスト\_リストのミニポートドライバーに対するクエリ要求を一覧表示するため、ミニポートドライバーはこれらのクエリ要求を受信しません。

マルチキャストアドレスリストをサポートするミニポートドライバーは、OID\_802\_3\_マルチキャスト\_リストセット要求をサポートする必要があります。

Set 要求の場合、 [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、マルチキャストアドレスリストがアドレスの配列として含まれています。

-   各アドレスは、6バイトの配列です。
-   **Informationbufferlength**メンバーには、 **informationbuffer**配列の長さがバイト単位で格納されます。
-   **Informationbuffer**メンバーの一覧に重複するアドレスがある場合、NDIS は、OID\_802\_3\_マルチキャスト\_リストセット要求をミニポートドライバーに送信する前に重複を削除します。
-   **Informationbufferlength**メンバーが0の場合、ミニポートドライバーはマルチキャストアドレス一覧をクリアする必要があります。
-   **Informationbufferlength**メンバーが0より大きい場合、ミニポートドライバーは、既存のマルチキャストアドレスリストを**informationbuffer**メンバーの一覧に置き換える必要があります。

ミニポートアダプターのマルチキャストアドレス一覧は、ミニポートアダプターにバインドされているすべてのプロトコルドライバーによって共有されます。 NDIS は、このリストへのアクセスを制御します。 複数のプロトコルドライバーが同時に一覧を変更しようとすると、NDIS は、要求を1つの OID\_802\_3\_マルチキャスト\_リストセット要求に結合して、ミニポートドライバーに送信します。

ミニポートアダプターが初期化されると、マルチキャストアドレス一覧がゼロになるように NIC がリセットされます。 また、NDIS はパケットフィルターを初期化して、プロトコルドライバーがマルチキャストパケットを受信できないようにします。

マルチキャストパケットを受信するには、プロトコルドライバーが後で次のいずれかを実行する必要があります。

-   **NDIS\_packet\_TYPE\_マルチキャスト**フラグを含めるようにパケットフィルターを設定します。 このフラグをキャンセルすることで、いつでもマルチキャストパケットの受信を無効にすることができます。 プロトコルドライバーがマルチキャストパケットの受信を有効にする順序は重要ではありません。 詳細については、「 [oid\_GEN\_現在の\_パケット\_フィルター](oid-gen-current-packet-filter.md) oid 要求」を参照してください。
-   すべてのマルチキャストパケットを有効にし、フィルター自体を使用して、 **NDIS\_packet\_TYPE\_すべての\_マルチキャスト**フラグを含めるようにパケットフィルターを設定します。

ミニポートドライバーでは、マルチキャストアドレス一覧に含めることができるマルチキャストアドレスの数に制限を設定できます。 プロトコルドライバーがこの制限を超えた場合、または無効なマルチキャストアドレスを指定した場合、NDIS は**ndis\_STATUS\_マルチキャスト\_完全**を返します。

クエリ要求の場合、NDIS は、すべてのプロトコルバインドのすべてのマルチキャストアドレス一覧の和集合であるマルチキャストアドレス一覧を返します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_802\_3\_\_マルチキャスト\_アドレスの追加](oid-802-3-add-multicast-address.md)

[OID\_802\_3\_\_のマルチキャスト\_アドレスの削除](oid-802-3-delete-multicast-address.md)

[OID\_802\_3\_最大\_リスト\_サイズ](oid-802-3-maximum-list-size.md)

[OID\_GEN\_現在の\_パケット\_フィルター](oid-gen-current-packet-filter.md)

 

 





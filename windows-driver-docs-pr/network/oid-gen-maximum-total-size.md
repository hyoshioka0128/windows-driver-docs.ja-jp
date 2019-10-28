---
title: OID_GEN_MAXIMUM_TOTAL_SIZE
description: クエリとして、OID_GEN_MAXIMUM_TOTAL_SIZE OID は、NIC がサポートする最大パケット長 (バイト単位) を指定します。
ms.assetid: 4973b4bd-58a5-4242-b33f-1ff8c3a7ec4b
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_GEN_MAXIMUM_TOTAL_SIZE ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 89089a839e2acd692410f6de483b395edc0e202b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843066"
---
# <a name="oid_gen_maximum_total_size"></a>OID\_GEN\_最大\_合計\_サイズ


クエリとして、OID\_GEN\_最大\_合計\_サイズ OID は、NIC がサポートする最大パケット長 (バイト単位) を指定します。 この仕様には、ヘッダーが含まれています。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 以降のバージョンの Windows  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 以降のミニポートドライバー  
必ず.

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 ミニポートドライバー  
必ず.

<a href="" id="windows-xp"></a>Windows XP  
サポートされています。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 ミニポートドライバー  
必ず.

<a name="remarks"></a>注釈
-------

返される長さは、基になるメディアの最大パケットサイズを指定します。 したがって、返される長さは、特定のメディアによって異なります。 プロトコルドライバーでは、この返された長さをゲージとして使用して、ミニポートドライバーがプロトコルドライバーに転送できる最大サイズパケットを決定できます。 プロトコルドライバーによってバッファーが事前された場合は、それに応じてバッファーが割り当てられます。 返される長さは、プロトコルドライバーが[**NdisSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissendnetbufferlists)関数に渡すことができる最大パケット数も指定します。

NIC のミニポートドライバーによって[802.1 p パケット優先順位](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff562331(v=vs.85))が有効になっている (つまり、ミニポートドライバーによって、 [oid\_GEN\_mac\_OPTIONS](oid-gen-mac-options.md) OID の 8021P\_priority ビット\_priority ビットが\_\_指定されている場合)。ビットマスク) では、ミニポートドライバーは、ネットワーク経由で送受信されるパケットの最大サイズを4バイト未満の最大パケット長として指定する必要があります。 たとえば、802.1 p パケット優先度が有効になっている NIC で受信し、長さが1514バイトのパケットを送信する場合、NIC のミニポートドライバーは、最大パケット長を1510バイトとして報告する必要があります。 ミニポートドライバーでは、ネットワーク経由で受信した、バインドされたプロトコルドライバーパケットのうち、OID\_\_GEN によって指定されたパケットサイズを超えていて、最大\_合計\_サイズを超えていることを示すことはできません。 つまり、ミニポートドライバーが、優先順位の値でマークされていないが、基になるメディアでサポートされている最大サイズのままであるネットワーク経由でパケットを受信した場合でも、ミニポートドライバーは、サイズを超えていないパケットのみを示すことができます。OID\_GEN によって指定されます。\_合計\_サイズ\_ます。

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


[**NdisSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissendnetbufferlists)

[OID\_GEN\_MAC\_オプション](oid-gen-mac-options.md)

 

 





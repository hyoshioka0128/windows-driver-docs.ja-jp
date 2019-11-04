---
title: OID_GEN_RCV_DISCARDS
description: クエリとして、NDIS およびそれ以降のドライバーは、OID_GEN_RCV_DISCARDS OID を使用して、ミニポートアダプターでの受信破棄の回数を決定します。
ms.assetid: 638d2961-d327-490d-925b-3f6c30a13a89
ms.date: 11/01/2019
keywords: -Windows Vista 以降の OID_GEN_RCV_DISCARDS ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 264766e26fa1a3088429ead9e3e4bcda7ed2e282
ms.sourcegitcommit: b8876f616ac625bb3f38218a32b2dc35ac7b3399
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/02/2019
ms.locfileid: "73443016"
---
# <a name="oid_gen_rcv_discards"></a>OID\_GEN\_RCV\_破棄


クエリとして、NDIS およびそれ以降のドライバーでは、\_GEN\_\_の OID が使用されます。この OID は、ミニポートアダプターでの受信破棄の回数を決定するために OID を破棄します。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 以降のバージョンの Windows  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 以降のミニポートドライバー  
要求されていません。 (「解説」を参照してください)

<a name="remarks"></a>注釈
-------

NDIS は、この OID をミニポートドライバー用に処理します。 統計の詳細については、 [oid\_GEN\_statistics](oid-gen-statistics.md) oid を参照してください。

このカウントは、RFC 2863 で説明されている*ifInDiscards*カウンターと同じです。

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


[OID\_GEN\_の統計情報](oid-gen-statistics.md)

 

 





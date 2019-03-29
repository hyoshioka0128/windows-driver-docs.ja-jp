---
title: OID_GEN_BYTES_RCV
description: クエリとして NDIS および上にあるドライバーはミニポート アダプターが受信したバイトの合計数を決定するのに OID_GEN_BYTES_RCV OID を使用します。
ms.assetid: e613e155-e4ff-48e4-8087-20ecad3c4644
ms.date: 08/08/2017
keywords: -OID_GEN_BYTES_RCV ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 8bc492c7c2a3605925401dbc0cb0b16a375a1f96
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580066"
---
# <a name="oidgenbytesrcv"></a>OID\_GEN\_バイト\_受信


クエリ、NDIS と関連付けたドライバーを使用、OID\_GEN\_バイト\_ミニポート アダプターが受信したバイトの合計数を決定する受信の OID。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista および Windows の以降のバージョン  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
要求されません。 (「解説」を参照してください セクション)

<a name="remarks"></a>コメント
-------

NDIS は、ミニポート ドライバーには、この OID を処理します。 参照してください、 [OID\_GEN\_統計](oid-gen-statistics.md)統計情報の詳細については OID。

合計バイト数は、受信主導のバイト数、受信マルチキャスト バイト数およびブロードキャストの受信バイト数の合計です。 この値は、によって返される値の合計と同じ、 [OID\_GEN\_ダイレクト\_バイト\_受信](oid-gen-directed-bytes-rcv.md)、 [OID\_GEN\_マルチキャスト\_バイト\_受信](oid-gen-multicast-bytes-rcv.md)、および[OID\_GEN\_ブロードキャスト\_バイト\_受信](oid-gen-broadcast-bytes-rcv.md)Oid。

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


[OID\_GEN\_ブロードキャスト\_バイト\_受信](oid-gen-broadcast-bytes-rcv.md)

[OID\_GEN\_ダイレクト\_バイト\_受信](oid-gen-directed-bytes-rcv.md)

[OID\_GEN\_マルチキャスト\_バイト\_受信](oid-gen-multicast-bytes-rcv.md)

[OID\_GEN\_統計情報](oid-gen-statistics.md)

 

 





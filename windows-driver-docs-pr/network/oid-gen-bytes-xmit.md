---
title: OID_GEN_BYTES_XMIT
description: クエリとして NDIS および上にあるドライバーはミニポート アダプターが送信された合計バイト数を決定するのに OID_GEN_BYTES_XMIT OID を使用します。
ms.assetid: 95b89a01-39e0-4e13-b960-32923e47a88d
ms.date: 08/08/2017
keywords: -OID_GEN_BYTES_XMIT ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 23f59d11ee505a0477b08f1172fdc393df6c6635
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323653"
---
# <a name="oidgenbytesxmit"></a>OID\_GEN\_バイト\_XMIT


クエリ、NDIS と関連付けたドライバーを使用、OID\_GEN\_バイト\_ミニポート アダプターが送信された合計バイト数を決定する XMIT OID。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista および Windows の以降のバージョン  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
要求されません。 (「解説」を参照してください セクション)

<a name="remarks"></a>注釈
-------

NDIS は、ミニポート ドライバーには、この OID を処理します。 参照してください、 [OID\_GEN\_統計](oid-gen-statistics.md)統計情報の詳細については OID。

合計バイト数は、転送送信バイト数、送信マルチキャスト バイト数およびブロードキャスト送信バイト数の合計です。 この値は、によって返される値の合計と同じ、 [OID\_GEN\_ダイレクト\_バイト\_XMIT](oid-gen-directed-bytes-xmit.md)、 [OID\_GEN\_マルチキャスト\_バイト\_XMIT](oid-gen-multicast-bytes-xmit.md)、および[OID\_GEN\_ブロードキャスト\_バイト\_XMIT](oid-gen-broadcast-bytes-xmit.md) Oid。

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


[OID\_GEN\_ブロードキャスト\_バイト\_XMIT](oid-gen-broadcast-bytes-xmit.md)

[OID\_GEN\_ダイレクト\_バイト\_XMIT](oid-gen-directed-bytes-xmit.md)

[OID\_GEN\_マルチキャスト\_バイト\_XMIT](oid-gen-multicast-bytes-xmit.md)

[OID\_GEN\_統計情報](oid-gen-statistics.md)

 

 





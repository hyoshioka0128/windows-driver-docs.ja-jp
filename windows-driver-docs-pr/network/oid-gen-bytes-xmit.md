---
title: OID_GEN_BYTES_XMIT
description: クエリとして、NDIS およびそれ以降のドライバーは、OID_GEN_BYTES_XMIT OID を使用して、ミニポートアダプターが送信した合計バイト数を確認します。
ms.assetid: 95b89a01-39e0-4e13-b960-32923e47a88d
ms.date: 11/01/2019
keywords: -Windows Vista 以降の OID_GEN_BYTES_XMIT ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 7ae58ebd9f7456278d14968911348aaf66294302
ms.sourcegitcommit: b8876f616ac625bb3f38218a32b2dc35ac7b3399
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/02/2019
ms.locfileid: "73442985"
---
# <a name="oid_gen_bytes_xmit"></a>OID\_GEN\_BYTES\_XMIT


クエリとして、NDIS およびそれ以降のドライバーは、XMIT OID\_OID\_GEN\_バイトを使用して、ミニポートアダプターが送信した合計バイト数を特定します。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 以降のバージョンの Windows  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 以降のミニポートドライバー  
要求されていません。 (「解説」を参照してください)

<a name="remarks"></a>注釈
-------

NDIS は、この OID をミニポートドライバー用に処理します。 統計の詳細については、 [oid\_GEN\_statistics](oid-gen-statistics.md) oid を参照してください。

合計バイト数は、送信方向のバイト数、送信/マルチキャストのバイト数、および送信/ブロードキャストのバイト数の合計です。 この値は、Oid\_GEN によって返される値の合計と同じになります。これは、XMIT、 [oid\_gen\_マルチキャスト\_bytes\_XMIT](oid-gen-multicast-bytes-xmit.md)に指定された[\_バイト\_転送\_](oid-gen-directed-bytes-xmit.md)ます。、および[oid\_GEN\_ブロードキャスト\_バイト\_XMIT](oid-gen-broadcast-bytes-xmit.md) oid です。

このカウントは、RFC 2863 で説明されている*ifOutOctets*カウンターと同じです。

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


[OID\_GEN\_ブロードキャスト\_バイト\_XMIT](oid-gen-broadcast-bytes-xmit.md)

[OID\_GEN\_ダイレクト\_バイト\_XMIT](oid-gen-directed-bytes-xmit.md)

[OID\_GEN\_マルチキャスト\_バイト\_XMIT](oid-gen-multicast-bytes-xmit.md)

[OID\_GEN\_の統計情報](oid-gen-statistics.md)

 

 





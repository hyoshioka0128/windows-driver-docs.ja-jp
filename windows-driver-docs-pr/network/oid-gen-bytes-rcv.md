---
title: OID_GEN_BYTES_RCV
description: クエリとして、NDIS およびそれ以降のドライバーは、OID_GEN_BYTES_RCV OID を使用して、ミニポートアダプターが受信した合計バイト数を確認します。
ms.assetid: e613e155-e4ff-48e4-8087-20ecad3c4644
ms.date: 11/01/2019
keywords: -Windows Vista 以降の OID_GEN_BYTES_RCV ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 0df977f94e4ae3fd7ce85f45609f0049322bc6cc
ms.sourcegitcommit: b8876f616ac625bb3f38218a32b2dc35ac7b3399
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/02/2019
ms.locfileid: "73443007"
---
# <a name="oid_gen_bytes_rcv"></a>OID\_GEN\_BYTES\_RCV


クエリとして、NDIS およびそれ以降のドライバーは、\_GEN\_バイト\_RCV OID を使用して、ミニポートアダプターが受信した合計バイト数を決定します。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 以降のバージョンの Windows  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 以降のミニポートドライバー  
要求されていません。 (「解説」を参照してください)

<a name="remarks"></a>注釈
-------

NDIS は、この OID をミニポートドライバー用に処理します。 統計の詳細については、 [oid\_GEN\_statistics](oid-gen-statistics.md) oid を参照してください。

合計バイト数は、受信方向のバイト数、受信マルチキャストのバイト数、および受信/ブロードキャストのバイト数の合計です。 この値は、Oid\_GEN によって返される値の合計と同じであり、 [\_バイト\_rcv](oid-gen-directed-bytes-rcv.md)、 [oid\_GEN\_マルチキャスト\_バイト\_RCV](oid-gen-multicast-bytes-rcv.md)\_送られます。、および[OID\_GEN\_ブロードキャスト\_バイト\_RCV](oid-gen-broadcast-bytes-rcv.md) oid です。

このカウントは、RFC 2863 で説明されている*ifInOctets*カウンターと同じです。

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


[OID\_GEN\_ブロードキャスト\_バイト\_RCV](oid-gen-broadcast-bytes-rcv.md)

[OID\_GEN\_ダイレクト\_バイト\_RCV](oid-gen-directed-bytes-rcv.md)

[OID\_GEN\_マルチキャスト\_バイト\_RCV](oid-gen-multicast-bytes-rcv.md)

[OID\_GEN\_の統計情報](oid-gen-statistics.md)

 

 





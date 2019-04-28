---
title: OID_GEN_RCV_DISCARDS
description: クエリとして NDIS および上にあるドライバーはミニポート アダプターの受信の数の破棄を決定するのに OID_GEN_RCV_DISCARDS OID を使用します。
ms.assetid: 638d2961-d327-490d-925b-3f6c30a13a89
ms.date: 08/08/2017
keywords: -OID_GEN_RCV_DISCARDS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 962c63cb3dc0a4d6f71260e80466de31e5fd5a1f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367704"
---
# <a name="oidgenrcvdiscards"></a>OID\_GEN\_受信\_破棄


クエリ、NDIS と関連付けたドライバーを使用、OID\_GEN\_受信\_ミニポート アダプターの受信の数を決定する破棄の OID を破棄します。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista および Windows の以降のバージョン  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
要求されません。 (「解説」を参照してください セクション)

<a name="remarks"></a>注釈
-------

NDIS は、ミニポート ドライバーには、この OID を処理します。 参照してください、 [OID\_GEN\_統計](oid-gen-statistics.md)統計情報の詳細については OID。

カウントは、RFC 2863」の説明に従って削除-受信-バッファーのエラーの数です。

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


[OID\_GEN\_統計情報](oid-gen-statistics.md)

 

 





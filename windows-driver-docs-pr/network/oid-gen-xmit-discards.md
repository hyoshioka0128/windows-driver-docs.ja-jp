---
title: OID_GEN_XMIT_DISCARDS
description: クエリとして NDIS および上にあるドライバーはミニポート アダプターの送信の数の破棄を決定するのに OID_GEN_XMIT_DISCARDS OID を使用します。
ms.assetid: f6265262-c485-441c-bb89-fa1d302608d2
ms.date: 08/08/2017
keywords: -OID_GEN_XMIT_DISCARDS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 5e28c7d4ca38bb09a9ee8ca6c517bc3ddbc12bc9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354182"
---
# <a name="oidgenxmitdiscards"></a>OID\_GEN\_XMIT\_破棄


クエリ、NDIS と関連付けたドライバーを使用、OID\_GEN\_XMIT\_ミニポート アダプターの送信の数を決定する破棄の OID を破棄します。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista および Windows の以降のバージョン  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
要求されません。 (「解説」を参照してください セクション)

<a name="remarks"></a>注釈
-------

NDIS は、ミニポート ドライバーには、この OID を処理します。 参照してください、 [OID\_GEN\_統計](oid-gen-statistics.md)統計情報の詳細については OID。

この OID を表す数は、インターフェイスによって破棄されるパケットの数です。

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
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_GEN\_統計情報](oid-gen-statistics.md)

 

 





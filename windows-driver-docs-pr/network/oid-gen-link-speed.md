---
title: OID_GEN_LINK_SPEED
description: OID_GEN_LINK_SPEED OID をクエリとしてには、NIC の最大速度を指定します
ms.assetid: f8ee887a-969e-4167-9b39-9ee6ef8b1fbc
ms.date: 08/08/2017
keywords: -OID_GEN_LINK_SPEED ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: c364b7a156b9496828881e08796079417b30073d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369060"
---
# <a name="oidgenlinkspeed"></a>OID\_GEN\_リンク\_速度


クエリ、OID として\_GEN\_リンク\_速度の OID は、NIC の最大速度を指定します

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista および Windows の以降のバージョン  
使われていません。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
使われていません。 (「解説」を参照してください セクション)

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
必須。

<a href="" id="windows-xp"></a>Windows XP  
サポートされています。

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
必須。

<a name="remarks"></a>注釈
-------

[OID\_GEN\_リンク\_状態](oid-gen-link-state.md)は、NDIS 6.0 とこの OID 以降およびそれ以降に相当します。 NDIS 6.0 とそれ以降のミニポート ドライバーを使用する必要がありますが、 [ **NDIS\_状態\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)状態を示す値をリンクの速度を示すために変更します。

測定単位は 100,000 の値が 10 Mbps のハードウェア ビット レートを表すためにの 100 bps です。

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


[**NDIS\_状態\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)

[OID\_GEN\_リンク\_状態](oid-gen-link-state.md)

 

 





---
title: OID_GEN_RCV_NO_BUFFER
description: クエリとしては、OID_GEN_RCV_NO_BUFFER OID は、受信バッファー領域の NIC が NIC の不足により受信できないフレームの数を指定します。
ms.assetid: 0fcbc7cc-439b-450f-b256-3584b29909fb
ms.date: 08/08/2017
keywords: -OID_GEN_RCV_NO_BUFFER ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 9565b066f12b8644204ce836b7efdc8209fec583
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531012"
---
# <a name="oidgenrcvnobuffer"></a>OID\_GEN\_受信\_いいえ\_バッファー


クエリ、OID として\_GEN\_受信\_いいえ\_バッファー OID は、受信バッファー領域の NIC が NIC の不足により受信できないフレームの数を指定します。 一部の Nic が失敗したフレームの正確な数にはできません。少なくとも 1 つのフレームが実行されなかった回数のみを提供します。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista および Windows の以降のバージョン  
使われていません。

<a href="" id="ndis-6-0-and-later-drivers"></a>NDIS 6.0 とそれ以降のドライバー  
要求されません。 使用[OID\_GEN\_統計](oid-gen-statistics.md)代わりにします。

<a href="" id="ndis-5-1-drivers"></a>5.1 の NDIS ドライバー  
必須。

<a href="" id="windows-xp"></a>Windows XP  
サポートされています。

<a href="" id="ndis-5-1-drivers"></a>5.1 の NDIS ドライバー  
必須。

<a name="remarks"></a>注釈
-------

Oid の統計に関する概要については、次を参照してください。 [General Statistics](https://msdn.microsoft.com/library/windows/hardware/ff552485)します。

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

 

 





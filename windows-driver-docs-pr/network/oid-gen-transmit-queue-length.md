---
title: OID_GEN_TRANSMIT_QUEUE_LENGTH
description: クエリとして OID_GEN_TRANSMIT_QUEUE_LENGTH OID には、現在キューに入れられた伝送、NIC であるかどうか、またはドライバーの内部キューでパケットの数を指定します。
ms.assetid: 042a7df3-a204-45f8-b147-96def7438b4a
ms.date: 08/08/2017
keywords: -OID_GEN_TRANSMIT_QUEUE_LENGTH ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: dd17076dfd7b0743409e37e6ad6ad2479a30e5cb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548913"
---
# <a name="oidgentransmitqueuelength"></a>OID\_GEN\_送信\_キュー\_長さ


クエリ、OID として\_GEN\_送信\_キュー\_長さ OID が現在キューに入れられた伝送、NIC であるかどうか、またはドライバーの内部キューでパケットの数を指定します。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista および Windows の以降のバージョン  
サポートされています。

<a href="" id="ndis-6-0-and-later-drivers"></a>NDIS 6.0 とそれ以降のドライバー  
(省略可能)。

<a href="" id="ndis-5-1-drivers"></a>5.1 の NDIS ドライバー  
(省略可能)。

<a href="" id="windows-xp"></a>Windows XP  
サポートされています。

<a href="" id="ndis-5-1-drivers"></a>5.1 の NDIS ドライバー  
(省略可能)。

<a name="remarks"></a>注釈
-------

クエリでは、常にパケットの合計数現在キューに置かれます数が返されます。 この数は、NDIS ライブラリで要求がキューに未送信の送信を含めることができます。

Oid の統計に関する概要については、[General Statistics](https://msdn.microsoft.com/library/windows/hardware/ff552485)を参照してください。

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

 

 





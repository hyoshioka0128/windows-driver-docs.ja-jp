---
title: OID_GEN_TRANSMIT_QUEUE_LENGTH
description: クエリとして OID_GEN_TRANSMIT_QUEUE_LENGTH OID には、現在キューに入れられた伝送、NIC であるかどうか、またはドライバーの内部キューでパケットの数を指定します。
ms.assetid: 042a7df3-a204-45f8-b147-96def7438b4a
ms.date: 08/08/2017
keywords: -OID_GEN_TRANSMIT_QUEUE_LENGTH ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 8624ec39678dde434a1bf1661e137b623f4d8a88
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385738"
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

Oid の統計に関する概要については、次を参照してください。 [General Statistics](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-general-statistics-oids)します。

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

 

 





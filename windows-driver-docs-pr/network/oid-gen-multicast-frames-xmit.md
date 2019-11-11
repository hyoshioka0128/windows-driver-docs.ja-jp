---
title: OID_GEN_MULTICAST_FRAMES_XMIT
description: クエリとして、OID_GEN_MULTICAST_FRAMES_XMIT OID は、エラーが発生することなく転送されるマルチキャスト/機能パケットの数を指定します。
ms.assetid: 780763a5-6220-44ad-a6e7-ed63e89baaed
ms.date: 11/01/2019
keywords: -Windows Vista 以降の OID_GEN_MULTICAST_FRAMES_XMIT ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: fe9cc124767cbf64ba9f3604180ad3d2ca984282
ms.sourcegitcommit: b8876f616ac625bb3f38218a32b2dc35ac7b3399
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/02/2019
ms.locfileid: "73443018"
---
# <a name="oid_gen_multicast_frames_xmit"></a>OID\_GEN\_マルチキャスト\_フレーム\_XMIT


クエリとして、OID\_GEN\_マルチキャスト\_フレーム\_XMIT OID は、エラーが発生することなく転送されるマルチキャスト/機能パケットの数を指定します。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 以降のバージョンの Windows  
使われていません。

<a href="" id="ndis-6-0-and-later-drivers"></a>NDIS 6.0 以降のドライバー  
要求されていません。 代わりに、 [OID\_GEN\_の統計](oid-gen-statistics.md)を使用してください。

<a href="" id="ndis-5-1-drivers"></a>NDIS 5.1 ドライバー  
(省略可能)。

<a href="" id="windows-xp"></a>Windows XP  
サポートされています。

<a href="" id="ndis-5-1-drivers"></a>NDIS 5.1 ドライバー  
(省略可能)。

<a name="remarks"></a>注釈
-------

この OID からのカウントと、 [OID_GEN_BROADCAST_FRAMES_XMIT](oid-gen-broadcast-frames-xmit.md)からのカウントは、RFC 2863 で説明されている*ifOutNUcastPkts*カウンターと同じです。

統計の Oid に関する一般的な情報については、「 [General statistics](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-general-statistics-oids)」を参照してください。

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


[OID\_GEN\_の統計情報](oid-gen-statistics.md)

 

 





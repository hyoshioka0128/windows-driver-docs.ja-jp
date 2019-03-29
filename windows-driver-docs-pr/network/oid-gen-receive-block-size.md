---
title: OID_GEN_RECEIVE_BLOCK_SIZE
description: としてクエリです。
ms.assetid: 92a7a388-4a41-41cf-96e5-a65b5559553d
ms.date: 08/08/2017
keywords: -OID_GEN_RECEIVE_BLOCK_SIZE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: f320cf7bebb06e6a861c9835cee573b1024f0edf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581591"
---
# <a name="oidgenreceiveblocksize"></a>OID\_GEN\_受信\_ブロック\_サイズ


としてクエリです。 OID\_GEN\_受信\_ブロック\_サイズ OID は、NIC の受信バッファー領域内に 1 つのパケットが占めるをバイト単位で、記憶域の容量を指定します

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista および Windows の以降のバージョン  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
必須。

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
必須。

<a href="" id="windows-xp"></a>Windows XP  
サポートされています。

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
必須。

<a name="remarks"></a>コメント
-------

OID\_GEN\_受信\_ブロック\_サイズ OID は、NIC の受信バッファー領域内に 1 つのパケットが占めるをバイト単位で、記憶域の容量を指定します

現在、最大から同じ情報を取得できます*先読み*サイズ。 ただし、他のことを確認する必要があるこれらの Oid の 1 つができます。 また、基になるドライバーが値を比較して完全なパケットを受信を示すかどうかプロトコル ドライバーが判断のドライバーを返します、 [OID\_GEN\_現在\_先読み](oid-gen-current-lookahead.md)と OID\_GEN\_受信\_ブロック\_サイズ Oid。

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


[OID\_GEN\_現在\_先読み](oid-gen-current-lookahead.md)

 

 





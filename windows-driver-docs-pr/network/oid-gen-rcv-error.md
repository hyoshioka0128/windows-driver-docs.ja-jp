---
title: OID_GEN_RCV_ERROR
description: クエリとして、OID_GEN_RCV_ERROR OID は NIC が受信するフレームの数を指定しますが、エラーが原因でプロトコルには示されません。
ms.assetid: 0481f225-869f-4313-9bc5-7af1de0b7d2d
ms.date: 11/01/2019
keywords: -Windows Vista 以降の OID_GEN_RCV_ERROR ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 784834bbdf94baa97e5a895c7086d76f2d8bcc4a
ms.sourcegitcommit: b8876f616ac625bb3f38218a32b2dc35ac7b3399
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/02/2019
ms.locfileid: "73443014"
---
# <a name="oid_gen_rcv_error"></a>OID\_GEN\_RCV\_エラー


クエリとして、OID\_GEN\_RCV\_ERROR OID は、NIC が受信するフレームの数を指定しますが、エラーが原因でプロトコルには示されません。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 以降のバージョンの Windows  
使われていません。

<a href="" id="ndis-6-0-and-later-drivers"></a>NDIS 6.0 以降のドライバー  
要求されていません。 代わりに、 [OID\_GEN\_の統計](oid-gen-statistics.md)を使用してください。

<a href="" id="ndis-5-1-drivers"></a>NDIS 5.1 ドライバー  
必ず.

<a href="" id="windows-xp"></a>Windows XP  
サポートされています。

<a href="" id="ndis-5-1-drivers"></a>NDIS 5.1 ドライバー  
必ず.

<a name="remarks"></a>注釈
-------

このカウントは、RFC 2863 で説明されている*ifInErrors*カウンターと同じです。

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

 

 





---
title: OID_GEN_DIRECTED_BYTES_RCV
description: クエリとして、OID_GEN_DIRECTED_BYTES_RCV OID は、エラーを発生させずに受信するダイレクトパケットのバイト数を指定します。
ms.assetid: 435941b5-647f-4c5f-84ef-7b4b832c452e
ms.date: 11/01/2019
keywords: -Windows Vista 以降の OID_GEN_DIRECTED_BYTES_RCV ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 75834c9e8bc32f3bbf1714b4a94d66302f5f2b57
ms.sourcegitcommit: b8876f616ac625bb3f38218a32b2dc35ac7b3399
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/02/2019
ms.locfileid: "73443004"
---
# <a name="oid_gen_directed_bytes_rcv"></a>OID\_GEN\_ダイレクト\_バイト\_RCV


クエリとして、OID\_GEN\_有\_バイト\_RCV OID は、受信したパケットのバイト数をエラーなしで指定します。

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

このカウントは、RFC 2863 で説明されている*ifInUcastPkts*カウンターと同じです。

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

 

 





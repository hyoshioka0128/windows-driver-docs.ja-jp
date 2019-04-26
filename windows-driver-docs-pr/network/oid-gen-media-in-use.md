---
title: OID_GEN_MEDIA_IN_USE
description: クエリとして OID_GEN_MEDIA_IN_USE OID には、NIC が現在使用しているメディアの種類の完全な一覧を指定します。
ms.assetid: 3b8db63d-07e0-4a5c-9848-57e594e3dd54
ms.date: 08/08/2017
keywords: -OID_GEN_MEDIA_IN_USE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 09b3af88cf9cb83c88ba9acd94721ee4bd242c10
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348148"
---
# <a name="oidgenmediainuse"></a>OID\_GEN\_メディア\_IN\_使用


クエリ、OID として\_GEN\_メディア\_IN\_OID を使用して、NIC が現在使用しているメディアの種類の完全な一覧を指定します。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista および Windows の以降のバージョン  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
使われていません。

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
必須。

<a href="" id="windows-xp"></a>Windows XP  
サポートされています。

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
必須。

<a name="remarks"></a>注釈
-------

NDIS 6.0 とそれ以降のミニポート ドライバーでは、この OID 要求は表示されません。 NDIS は、ミニポート ドライバーが初期化中に指定するキャッシュされた値を持つこの OID を処理します。

この OID と同じ情報を提供する、 [OID\_GEN\_メディア\_サポートされている](oid-gen-media-supported.md)OID。

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


[OID\_GEN\_メディア\_サポートされています。](oid-gen-media-supported.md)

 

 





---
title: OID_GEN_MAXIMUM_LOOKAHEAD
description: クエリとして OID_GEN_MAXIMUM_LOOKAHEAD OID には、NIC を先読みデータとして提供するバイトの最大数を指定します。
ms.assetid: 086581f7-c0a5-4355-82fe-22f53201b540
ms.date: 08/08/2017
keywords: -OID_GEN_MAXIMUM_LOOKAHEAD ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: f73390c6a8ec9289b122865a914ea898c20e1e22
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537642"
---
# <a name="oidgenmaximumlookahead"></a>OID\_GEN\_最大\_先読み


クエリ、OID として\_GEN\_最大\_先読み OID 先読みデータとして、NIC を提供するバイトの最大数を指定します。 この仕様では、ヘッダーは含まれません。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista および Windows の以降のバージョン  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
要求されません。

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
必須。

<a href="" id="windows-xp"></a>Windows XP  
サポートされています。

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
必須。

<a name="remarks"></a>注釈
-------

NDIS 6.0 とそれ以降のミニポート ドライバーでは、この OID 要求は表示されません。 NDIS は、ミニポート ドライバーが初期化中に指定するキャッシュされた値を持つこの OID を処理します。

上位層のドライバーでは、クライアントの 1 つ以上の先読みデータに関連付けられているパケットが対象として かどうかを判断する先読みデータを調べます。

基になるドライバー multipacket をサポートしている場合は、インジケーターが表示される、すべてを示す値をバインド プロトコル ドライバーに完全な net パケットが与えられます。 そのため、この値はに対して返されるのと同じ[OID\_GEN\_受信\_ブロック\_サイズ](oid-gen-receive-block-size.md)します。

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


[OID\_GEN\_受信\_ブロック\_サイズ](oid-gen-receive-block-size.md)

 

 





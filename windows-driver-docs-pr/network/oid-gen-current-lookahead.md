---
title: OID_GEN_CURRENT_LOOKAHEAD
description: クエリとして OID_GEN_CURRENT_LOOKAHEAD OID はプロトコル ドライバーに示されるデータを受信したパケットのバイト数を返します。
ms.assetid: ccfcb5ca-04bd-416b-91ec-690e78daeda0
ms.date: 08/08/2017
keywords: -OID_GEN_CURRENT_LOOKAHEAD ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 245d4dbee3cf8173d1164ad1d8b9bda1223114ca
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529025"
---
# <a name="oidgencurrentlookahead"></a>OID\_GEN\_現在\_先読み


クエリ、OID として\_GEN\_現在\_先読み OID がプロトコル ドライバーに示されるデータを受信したパケットのバイト数を返します。 この仕様では、ヘッダーは含まれません。

OID、セットとして\_GEN\_現在\_先読み OID プロトコル ドライバーに示す必要があります、ミニポート ドライバーの受信パケット データのバイト数を指定します。 この仕様では、ヘッダーは含まれません。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista および Windows の以降のバージョン  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
必須。 (「解説」を参照してください セクション)

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
必須。

<a href="" id="windows-xp"></a>Windows XP  
サポートされています。

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
必須。

<a name="remarks"></a>注釈
-------

NDIS は、NDIS 6.0 とそれ以降のミニポート ドライバーのクエリとセットが失敗した要求を処理します。 NDIS は、初期化とミニポート アダプタの再起動時に、ミニポート ドライバーから情報を取得します。 ただし、NDIS は、ミニポート ドライバーに有効なセット要求を送信します。

クエリの場合は、NDIS は、すべてのバインディングの中から最大の先読みサイズを返します。 プロトコル ドライバーは、そのバインディングで使用されるバイト数の推奨値を設定できます。ただし、基になるミニポート ドライバーでは、値のセットをその表示を制限する必要はありません。

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

 

 





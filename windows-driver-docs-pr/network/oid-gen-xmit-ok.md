---
title: OID_GEN_XMIT_OK
description: クエリとして OID_GEN_XMIT_OK OID にはエラーなしで送信されるフレームの数を指定します。
ms.assetid: ac7120a3-58bb-4047-b4b7-ad9fbaf14e4f
ms.date: 08/08/2017
keywords: -OID_GEN_XMIT_OK ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: d97a14765112a61347797a6283dd6f5431c492b3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385733"
---
# <a name="oidgenxmitok"></a>OID\_GEN\_XMIT\_OK


クエリ、OID として\_GEN\_XMIT\_OK OID がエラーなしで送信されるフレームの数を指定します。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista および Windows の以降のバージョン  
サポートされています。

<a href="" id="ndis-6-0-and-later-drivers"></a>NDIS 6.0 とそれ以降のドライバー  
必須。

<a href="" id="ndis-5-1-drivers"></a>5.1 の NDIS ドライバー  
必須。

<a href="" id="windows-xp"></a>Windows XP  
サポートされています。

<a href="" id="ndis-5-1-drivers"></a>5.1 の NDIS ドライバー  
必須。

<a name="remarks"></a>注釈
-------

OID\_GEN\_XMIT\_[ok] をエラーなしで送信されるフレームの数を指定します。 ただし、 [OID\_GEN\_統計](oid-gen-statistics.md)この情報は含まれません。

注: 統計の Oid は NDIS は、それを処理しない限り、NDIS 6.0 とそれ以降のミニポート ドライバーの必須です。 Oid の統計に関する概要については、次を参照してください。 [General Statistics](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-general-statistics-oids)します。

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

 

 





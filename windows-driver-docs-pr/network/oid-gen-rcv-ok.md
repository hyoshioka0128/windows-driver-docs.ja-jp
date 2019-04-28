---
title: OID_GEN_RCV_OK
description: クエリとして OID_GEN_RCV_OK OID には、NIC がエラーなしで受信し、バインド プロトコルに示すフレームの数を指定します。
ms.assetid: 737ac1a5-9f7a-422b-9ccf-42a3176639bc
ms.date: 08/08/2017
keywords: -OID_GEN_RCV_OK ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 7ad86f3b513cbf91574e31ba000a721f95ac1646
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367539"
---
# <a name="oidgenrcvok"></a>OID\_GEN\_受信\_OK


クエリ、OID として\_GEN\_受信\_OID の [ok] を NIC がエラーなしで受信し、プロトコルのバインドを示すフレームの数を指定します。

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

OID\_GEN\_受信\_[ok] をエラーなしで受信したフレームの数を指定します。 ただし、 [OID\_GEN\_統計](oid-gen-statistics.md)この情報は含まれません。

注: 統計の Oid は NDIS は、それを処理しない限り、NDIS 6.0 とそれ以降のミニポート ドライバーの必須です。 Oid の統計に関する概要については、次を参照してください。 [General Statistics](https://msdn.microsoft.com/library/windows/hardware/ff552485)します。

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

 

 





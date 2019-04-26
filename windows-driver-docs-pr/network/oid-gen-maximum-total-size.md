---
title: OID_GEN_MAXIMUM_TOTAL_SIZE
description: クエリとして OID_GEN_MAXIMUM_TOTAL_SIZE OID (バイト)、NIC がサポートする合計パケットの最大の長さを指定します。
ms.assetid: 4973b4bd-58a5-4242-b33f-1ff8c3a7ec4b
ms.date: 08/08/2017
keywords: -OID_GEN_MAXIMUM_TOTAL_SIZE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 27d2ba749322220f7efde2885ff452c09877ca99
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358858"
---
# <a name="oidgenmaximumtotalsize"></a>OID\_GEN\_最大\_合計\_サイズ


クエリ、OID として\_GEN\_最大\_合計\_OID のサイズを合計パケットの最大の長さを指定します (バイト単位)、NIC をサポートしています。 この仕様には、ヘッダーが含まれています。

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

<a name="remarks"></a>注釈
-------

返される長さは、中程度の基になる最大パケット サイズを指定します。 そのため、返される長さは、特定のメディアに依存します。 プロトコル ドライバーは、ミニポート ドライバーでしたプロトコル ドライバーに転送するパケットの最大サイズを決定するのにゲージとして返されるこの長さを使用可能性があります。 プロトコル ドライバーにバッファーが事前に割り当てる場合は、バッファーを適宜割り当てます。 返される長さは最大のパケットを渡すことができるプロトコル ドライバーも指定します、 [ **NdisSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff564535)関数。

場合、NIC のミニポート ドライバーを有効[802.1 p のパケットの優先順位](https://msdn.microsoft.com/library/windows/hardware/ff562331)(つまり、ミニポート ドライバーは、NDIS を指定\_MAC\_オプション\_8021 P\_の優先順位ビット[OID\_GEN\_MAC\_オプション](oid-gen-mac-options.md)OID ビットマスク)、ミニポート ドライバーが 4 バイトとしてその合計パケットの最大長を指定する必要がありますしより小さいパケットの最大サイズは、受信または経由で送信しますネットワーク。 たとえばを有効になっている、802.1 p パケットの優先順位を持つ NIC は、受信し、1514 バイト長である、ネットワーク上でパケットを送信して、NIC のミニポート ドライバーする必要があります、合計パケットの最大の長さ 1510 バイトとしてレポート。 ミニポート ドライバーがネットワーク経由で受信した OID で指定されたパケット サイズを超えているバインド プロトコル ドライバー パケットまで示す必要がありますしない\_GEN\_最大\_合計\_サイズ。 つまり、ミニポート ドライバーでは、優先度の値でマークされていないが、基になるメディアをサポートする最大サイズではまだネットワーク上でパケットを受信する場合でも、ミニポート ドライバーを示すことしかパケット サイズを超えています。OID で指定された\_GEN\_最大\_合計\_サイズ。

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


[**NdisSendNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff564535)

[OID\_GEN\_MAC\_オプション](oid-gen-mac-options.md)

 

 





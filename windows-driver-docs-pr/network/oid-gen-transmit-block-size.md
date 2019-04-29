---
title: OID_GEN_TRANSMIT_BLOCK_SIZE
description: OID_GEN_TRANSMIT_BLOCK_SIZE OID はクエリとして、NIC の送信バッファー領域の 1 つのネットワーク パケットを占有するバイト数の最小数を指定します
ms.assetid: 81874999-029a-4e7e-8dbe-fc8e34bcae67
ms.date: 08/08/2017
keywords: -OID_GEN_TRANSMIT_BLOCK_SIZE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 128b017418cbc9d1dc7f7d2c6464845acab3f235
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387887"
---
# <a name="oidgentransmitblocksize"></a>OID\_GEN\_送信\_ブロック\_サイズ


クエリ、OID として\_GEN\_送信\_ブロック\_サイズ OID は、NIC の送信バッファーの領域で 1 つのネットワーク パケットを占有するバイト数の最小数を指定します

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

OID\_GEN\_送信\_ブロック\_サイズ OID は、NIC の送信バッファーの領域で 1 つのネットワーク パケットを占有するバイト数の最小数を指定します たとえば、256 バイト部分に分かれています送信領域のある NIC は 256 バイトの送信のブロック サイズになります。 このような NIC の合計送信バッファー領域を計算するには、そのドライバーは、送信ブロック サイズで NIC での送信バッファーの数を乗算します。

他の Nic の送信のブロック サイズは、その最大パケット サイズと同じです。

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

 

 





---
title: OID_GEN_TRANSMIT_BUFFER_SPACE
description: クエリとして OID_GEN_TRANSMIT_BUFFER_SPACE OID をメモリの量を指定します (バイト単位)、バッファリングに使用される NIC でデータを送信します。
ms.assetid: 23d242fc-8447-4660-ab84-b8cbdb638a71
ms.date: 08/08/2017
keywords: -OID_GEN_TRANSMIT_BUFFER_SPACE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 3fe56b00adf67686e5c510961039d3245dc54efc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539173"
---
# <a name="oidgentransmitbufferspace"></a>OID\_GEN\_送信\_バッファー\_領域


クエリ、OID として\_GEN\_送信\_バッファー\_領域 OID をメモリの量を指定します (バイト単位)、バッファリングに使用される NIC でデータを送信します。

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

プロトコルは、量のサイズ調整をガイドとしてこの OID を使用することができます送信ごとのデータを送信します。

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

 

 





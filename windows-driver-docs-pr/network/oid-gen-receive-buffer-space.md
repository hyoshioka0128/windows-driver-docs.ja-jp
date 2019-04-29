---
title: OID_GEN_RECEIVE_BUFFER_SPACE
description: クエリとして OID_GEN_RECEIVE_BUFFER_SPACE OID を受信データのバッファリング用に使用される NIC でのメモリの量を指定します。
ms.assetid: 6eec18fa-22cd-4f65-acf4-0dd438dea2ff
ms.date: 08/08/2017
keywords: -OID_GEN_RECEIVE_BUFFER_SPACE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 2ea0f96e6949e58a17333e6cf0f6e742d6533acb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391030"
---
# <a name="oidgenreceivebufferspace"></a>OID\_GEN\_受信\_バッファー\_領域


クエリ、OID として\_GEN\_受信\_バッファー\_領域 OID は、受信データのバッファリング用に使用される NIC でメモリの量を指定します。

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

プロトコル ドライバーは広告のためのガイドとしてこの OID を使用することができます、リモート ノードとのセッションを確立した後で、ウィンドウを表示します。

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

 

 





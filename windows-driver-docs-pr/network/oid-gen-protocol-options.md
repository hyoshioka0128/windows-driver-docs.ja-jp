---
title: OID_GEN_PROTOCOL_OPTIONS
description: セットとして OID_GEN_PROTOCOL_OPTIONS OID にプロトコル ドライバーの省略可能なプロパティを定義するビットマスクを指定します。
ms.assetid: 48c3468b-2d8b-48cb-9a25-19470923f582
ms.date: 08/08/2017
keywords: -OID_GEN_PROTOCOL_OPTIONS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: c4fbfd8d7bf456986065325881f9740c4c3c1b7c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367714"
---
# <a name="oidgenprotocoloptions"></a>OID\_GEN\_プロトコル\_オプション


OID、セットとして\_GEN\_プロトコル\_オプション OID プロトコル ドライバーの省略可能なプロパティを定義するビットマスクを指定します。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista および Windows の以降のバージョン  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
要求されません。 この OID はプロトコル ドライバー用です。

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
必須。

<a href="" id="windows-xp"></a>Windows XP  
サポートされています。

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
必須。

<a name="remarks"></a>注釈
-------

プロトコルは、これらのオプションで利用できますが、そのプロパティの NDIS を通知します。 プロトコル ドライバーがバインディングでそのフラグを設定しない場合、NDIS すべてクリアが前提としています。

次のフラグは現在定義されています。

<a href="" id="ndis-prot-option-estimated-length"></a>NDIS\_ポート\_オプション\_推定\_長さ  
このプロトコルには正確な値ではなく、パケット サイズの最悪の場合の推定値でパケットを示すことができますを指定します。

<a href="" id="ndis-prot-option-no-loopback"></a>NDIS\_ポート\_オプション\_いいえ\_ループバック  
プロトコルにバインディングでループバックのサポートが必要ないことを指定します。

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

 

 





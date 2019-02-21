---
title: OID_GEN_MAXIMUM_FRAME_SIZE
description: クエリとして OID_GEN_MAXIMUM_FRAME_SIZE OID (バイト単位)、NIC をサポートする最大ネットワーク パケット サイズを指定します。
ms.assetid: 4c81f3a6-6f66-466d-8d22-67841a5a8320
ms.date: 08/08/2017
keywords: -OID_GEN_MAXIMUM_FRAME_SIZE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 8079f279baa2e230301db058eb0f6671c97270e9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528779"
---
# <a name="oidgenmaximumframesize"></a>OID\_GEN\_最大\_フレーム\_サイズ


クエリ、OID として\_GEN\_最大\_フレーム\_サイズ OID (バイト単位)、NIC をサポートする最大ネットワーク パケット サイズを指定します。 この仕様では、ヘッダーは含まれません。

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

ミニポート ドライバーでは、初期化中にされ、再起動中に、最大フレーム サイズが用意されています。 NDIS は、NDIS 6.0 とそれ以降のミニポート ドライバーのこの OID クエリを処理します。

このクエリを要求しているトランスポートからの応答、ミニポート ドライバーには、ヘッダーを除く、トランスポートを送信できる最大フレーム サイズが示されます。 トランスポートへのバインディングのもう 1 つのメディアの種類をエミュレートするミニポート ドライバーでは、プロトコルが指定したネットワーク パケットの最大フレーム サイズが中程度のトゥルー ネットワーク サイズの制限を超えていないことを確認する必要があります。 フレームでフィールドを挿入することが必要な NIC をサポートするミニポート ドライバーについても同様です。 たとえば、最大転送単位 (MTU) を確認するのにトランスポートこのクエリを送信 NIC

ミニポート ドライバーには、802.1 p のパケットの優先順位と 802.1Q サポートしているかどうか、ミニポート ドライバーでは、優先度の値が削除されると、前に、フレームに古いネットワークを走査する必要がありますが必要な場合は、前のアクションに基づいて仮想 LAN (VLAN) タグ ミニポート ドライバーがある可能性があります、このクエリに対する応答の値を小さくします。

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

 

 





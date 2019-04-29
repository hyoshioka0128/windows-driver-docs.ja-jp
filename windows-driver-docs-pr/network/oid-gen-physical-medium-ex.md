---
title: OID_GEN_PHYSICAL_MEDIUM_EX
description: クエリとして OID_GEN_PHYSICAL_MEDIUM_EX OID には、ミニポート アダプターをサポートする物理メディアの種類を指定します。
ms.assetid: cbac8c9b-d7fe-4588-8a64-599d04a77a72
ms.date: 08/08/2017
keywords: -OID_GEN_PHYSICAL_MEDIUM_EX ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 0c0f0b934035cbe6cfac6e9f2cb82f6ee5efb277
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324462"
---
# <a name="oidgenphysicalmediumex"></a>OID\_GEN\_物理\_MEDIUM\_例


クエリ、OID として\_GEN\_物理\_MEDIUM\_EX OID ミニポート アダプターをサポートする物理メディアの種類を指定します。

<a name="remarks"></a>注釈
-------

NDIS は、NDIS 6.0 とそれ以降のミニポート ドライバーのこの OID を処理します。 ミニポート ドライバーでは、初期化中に物理中程度の値を提供します。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造に含まれる、NDIS\_物理\_中程度の列挙値。

**注**  OID の違い\_GEN\_物理\_MEDIUM\_EX と[OID\_GEN\_物理\_中](oid-gen-physical-medium.md) OID は\_GEN\_物理\_MEDIUM\_EX バージョンがオーバーライドしません、 **NdisPhysicalMedium802\_3** と型**NdisPhysicalMediumUnspecified**は OID\_GEN\_物理\_中は引き続きは。 6.x のすべてのドライバーが、EX バージョンを使用することをお勧めします。 OID\_GEN\_物理\_MEDIUM\_EX が WMI GUID を介して公開されます。

 

ミニポート ドライバーでサポートするために宣言されているメディアから、物理メディアを区別するために、物理メディアの種類のレポート、 [OID\_GEN\_メディア\_サポートされている](oid-gen-media-supported.md)OID クエリ。

NDIS サポート、OID\_GEN\_物理\_MEDIUM\_ミニポート アダプターがこれらのネットワーク オペレーティング システムおよび NDIS として表示されるパケットを転送する場合でも、新しいネットワークをサポートするための EX OID標準的なよく知られているメディアの種類。

新しいネットワークでは、標準のメディアのように表示される可能性がありますが、新しい機能や、標準のわずかな違いがある可能性がありますのパケットを転送します。 この OID には、上位層のためのドライバーが存在して、アプリケーションは、NIC が接続する実際のネットワークを確認できます。 基になるネットワークに関する情報を取得するには、後に上位層のドライバーとアプリケーションはこのようなドライバーとアプリケーションの動作を変更するのにこの情報を使用できます。

ありませんし、定義されている物理メディアの種類、NDIS 6.0 以降およびそれ以降のバージョン、エミュレートされた 802.3 NIC から NIC、802.3 を明確に区別するためにレポートを 802.3 ミニポート ドライバーを必要とする**NdisPhysicalMedium802\_3**メディアの種類。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>以降では、NDIS 6.20 が動作をサポートします。 ミニポート ドライバーには要求されません。 (「解説」の「」を参照).</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[OID\_GEN\_メディア\_サポートされています。](oid-gen-media-supported.md)

[OID\_GEN\_物理\_中](oid-gen-physical-medium.md)

 

 





---
title: MB アダプターの一般的な属性要件
description: MB アダプターの一般的な属性要件
ms.assetid: c2bfb625-3455-41e0-abdd-ab7204eaae0a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8fed7316b18bf2a5cb8a534ac0d867d6365ce385
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387291"
---
# <a name="mb-adapter-general-attribute-requirements"></a>MB アダプターの一般的な属性要件


次の表に、ミニポート ドライバー メンバー設定する必要がありますの変数値、 [ **NDIS\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)構造体をします。 呼び出し時に、MB ミニポート ドライバーがこれらの値を使用する必要があります[ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)からその[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数では、ミニポート ドライバーの初期化中にします。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">INF ファイル内のフィールド</th>
<th align="left">推奨値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>IfType</p></td>
<td align="left"><p>GSM ベースのデバイスでは、IF_TYPE_WWANPP を指定する必要があります。</p>
<p>CDMA ベースのデバイスでは、IF_TYPE_WWANPP2 を指定します。</p>
<p>値が一致する必要があります、*、ミニポート ドライバーの INF ファイルで指定された IfType 値。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MediaType</p></td>
<td align="left"><p>値が一致する必要があります、*、ミニポート ドライバーの INF ファイルで指定された MediaType の値。 たとえば、いずれか<strong>NdisMediumWirelessWan</strong>または<strong>NdisMedium802_3</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PhysicalMediumType</p></td>
<td align="left"><p>値が一致する必要があります、*、ミニポート ドライバーの INF ファイルで指定された PhysicalMediaType 値。 値がある必要があります<strong>NdisPhysicalMediumWirelessWan</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>AccessType</p></td>
<td align="left"><p>MediaType の値が指定されて場合<strong>NdisMediumWirelessWan</strong>、指定<strong>NET_IF_ACCESS_POINT_TO_POINT</strong> AccessType の。 メディアの種類が場合<strong>NdisMedium802_3</strong>NET_IF_ACCESS_BROADCAST を指定します。</p></td>
</tr>
</tbody>
</table>

 

 

 






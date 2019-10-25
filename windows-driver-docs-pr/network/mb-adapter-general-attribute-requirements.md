---
title: MB アダプターの一般的な属性要件
description: MB アダプターの一般的な属性要件
ms.assetid: c2bfb625-3455-41e0-abdd-ab7204eaae0a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25f6aef763437311a8721f37bb5564df007c23e0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844299"
---
# <a name="mb-adapter-general-attribute-requirements"></a>MB アダプターの一般的な属性要件


次の表では、ミニポートドライバーが[**NDIS\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)構造体のメンバー変数をに設定する必要がある値について説明します。 ミニポートドライバーの初期化中に、MB のミニポートドライバーが[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数から[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)を呼び出す場合は、これらの値を使用する必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">INF ファイルのフィールド</th>
<th align="left">推奨値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>IfType</p></td>
<td align="left"><p>GSM ベースのデバイスでは、IF_TYPE_WWANPP を指定する必要があります。</p>
<p>CDMA ベースのデバイスでは、IF_TYPE_WWANPP2 を指定します。</p>
<p>値は、ミニポートドライバーの INF ファイルで指定された * IfType 値と一致している必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MediaType</p></td>
<td align="left"><p>値は、ミニポートドライバーの INF ファイルで指定されている * MediaType 値と一致している必要があります。 たとえば、 <strong>NdisMediumWirelessWan</strong>または<strong>NdisMedium802_3</strong>のいずれかです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PhysicalMediumType</p></td>
<td align="left"><p>値は、ミニポートドライバーの INF ファイルで指定されている * PhysicalMediaType の値と一致する必要があります。 値は<strong>NdisPhysicalMediumWirelessWan</strong>である必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>AccessType</p></td>
<td align="left"><p>MediaType の値が<strong>NdisMediumWirelessWan</strong>として指定されている場合は、AccessType に<strong>NET_IF_ACCESS_POINT_TO_POINT</strong>を指定します。 MediaType が<strong>NdisMedium802_3</strong>の場合は、NET_IF_ACCESS_BROADCAST を指定します。</p></td>
</tr>
</tbody>
</table>

 

 

 






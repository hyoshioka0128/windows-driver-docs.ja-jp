---
title: MB アダプターの一般的な属性要件
description: MB アダプターの一般的な属性要件
ms.assetid: c2bfb625-3455-41e0-abdd-ab7204eaae0a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 183dd81a4bfb7e5c9383e0cabc4e740cffcb4f45
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343456"
---
# <a name="mb-adapter-general-attribute-requirements"></a>MB アダプターの一般的な属性要件


次の表に、ミニポート ドライバー メンバー設定する必要がありますの変数値、 [ **NDIS\_ミニポート\_アダプター\_全般\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)構造体をします。 呼び出し時に、MB ミニポート ドライバーがこれらの値を使用する必要があります[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)からその[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数では、ミニポート ドライバーの初期化中にします。

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

 

 

 






---
title: WDI_TLV_LSO_V1_CAPABILITIES (0xCC)
description: WDI_TLV_LSO_V1_CAPABILITIES では、大規模なオフロード V1 の送信機能を含む TLV です。
ms.assetid: 22C5778A-F551-4931-A19C-7AA399221B3D
ms.date: 07/18/2017
keywords:
- WDI_TLV_LSO_V1_CAPABILITIES (0 xcc) ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 366fde51f9f3cea9fec6b4c97e0ba14b4164715c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357240"
---
# <a name="wditlvlsov1capabilities-0xcc"></a>WDI\_TLV\_LSO\_V1\_機能 (0 xcc)


WDI\_TLV\_LSO\_V1\_機能は、大規模なオフロード V1 の送信機能を含む TLV します。

記載されている機能の値が報告[ **NDIS\_TCP\_IP\_チェックサム\_オフロード**](https://msdn.microsoft.com/library/windows/hardware/ff567878)します。 NDIS を使用して、\_オフロード\_いない\_サポートと NDIS\_オフロード\_を介して機能を指定する際にサポートされている[OID\_WDI\_GET\_アダプター\_機能](https://msdn.microsoft.com/library/windows/hardware/dn925838)します。

## <a name="tlv-type"></a>TLV 型


0xCC

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>型</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UINT32</td>
<td>カプセル化の種類。 有効な値は次のとおりです。
<ul>
<li>WDI_ENCAPSULATION_IEEE_802_11</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>最大サイズをオフロードします。 1 パケットあたり TCP ユーザー データのバイトの最大数で指定します。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>大きな TCP パケットとトランスポートで割り切れる必要がありますセグメントの最小数をセグメント化のためにハードウェアにオフロードできます。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>TCP オプションがこのオフロード用にサポートされているかどうかを指定します。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>IP のオプションがこのオフロード用にサポートされているかどうかを指定します。</td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 





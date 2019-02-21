---
title: WDI_TLV_RADIO_STATE
description: WDI_TLV_RADIO_STATE では、ハードウェアとソフトウェア無線の状態を含む TLV です。
ms.assetid: 0DAE1D0A-4EEC-4054-A67C-EC3B5EDF77A5
ms.date: 07/18/2017
keywords:
- WDI_TLV_RADIO_STATE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 0907fb119a7f48afbad2d66f0ec15b6d5e88d762
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558947"
---
# <a name="wditlvradiostate"></a>WDI\_TLV\_ラジオ\_状態


WDI\_TLV\_ラジオ\_状態は、ハードウェアとソフトウェア無線の状態を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0xA1

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
<th>種類</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UINT8</td>
<td>ハードウェア無線の現在の状態。
<p>有効な値とは、0 および 1 です。</p></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>ソフトウェアのオプションの現在の状態。
<p>有効な値とは、0 および 1 です。</p></td>
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

 

 





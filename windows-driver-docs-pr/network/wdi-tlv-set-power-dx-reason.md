---
title: WDI_TLV_SET_POWER_DX_REASON
description: WDI_TLV_SET_POWER_DX_REASON では、セット power Dx の理由を含む TLV です。
ms.assetid: 339F3461-3478-4C54-B6FB-9F5541859C76
ms.date: 07/18/2017
keywords:
- WDI_TLV_SET_POWER_DX_REASON ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: fdc4a0e25ae474c0fa3be35debba07661b91ed09
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539523"
---
# <a name="wditlvsetpowerdxreason"></a>WDI\_TLV\_設定\_POWER\_DX\_理由


WDI\_TLV\_設定\_POWER\_DX\_理由は、セット power Dx の理由を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x103

## <a name="length"></a>長さ


Uint32 型のサイズをバイト単位で。

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
<td>UINT32</td>
<td>セット power Dx の理由です。
<p>有効な値は次のとおりです。</p>
<ul>
<li><p>WDI_SET_POWER_DX_REASON_SELETIVE_SUSPEND (1)</p>
<p>この値を設定すると、関心のある外部イベントなしで、ことを示します。 明示的な<a href="wdi-tlv-enable-wake-events.md" data-raw-source="[&lt;strong&gt;WDI_TLV_ENABLE_WAKE_EVENTS&lt;/strong&gt;](wdi-tlv-enable-wake-events.md)"> <strong>WDI_TLV_ENABLE_WAKE_EVENTS</strong></a>します。 これは、場所、デバイス機能に透過的にエンドユーザーに D0 を使用した場合とアイドル状態の省電力です。 参照してください<a href="https://msdn.microsoft.com/library/windows/hardware/mt269159" data-raw-source="[WDI USB remote wake sequence](https://msdn.microsoft.com/library/windows/hardware/mt269159)">WDI USB リモート ウェイク シーケンス</a>詳細についてはします。</p></li>
</ul></td>
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

 

 





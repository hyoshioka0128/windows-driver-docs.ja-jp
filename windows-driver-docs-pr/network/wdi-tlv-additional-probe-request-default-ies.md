---
title: WDI_TLV_ADDITIONAL_PROBE_REQUEST_DEFAULT_IES
description: WDI_TLV_ADDITIONAL_PROBE_REQUEST_DEFAULT_IES では、追加のプローブ要求 IEs を含む TLV です。
ms.assetid: E364B1BC-5A78-42C8-B04D-31BD21141477
ms.date: 07/18/2017
keywords:
- WDI_TLV_ADDITIONAL_PROBE_REQUEST_DEFAULT_IES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 4c6c46ce66ae9a393438fdf96f8e43c2e468cc35
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552286"
---
# <a name="wditlvadditionalproberequestdefaulties"></a>WDI\_TLV\_追加\_プローブ\_要求\_既定\_IES


WDI\_TLV\_追加\_プローブ\_要求\_既定\_IES は追加のプローブ要求 IEs を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x70

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

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
<td>UINT8[]</td>
<td>Probe 要求 IEs の配列。 Wi-Fi Direct のポートは、送信されたプローブ要求パケットにこれらの追加 IEs を追加する必要があります。
<div class="alert">
<strong>注</strong>  A Wi-Fi Direct 検出要求は、既定のプローブ要求 IEs をオーバーライドします。
</div>
<div>
 
</div></td>
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

 

 





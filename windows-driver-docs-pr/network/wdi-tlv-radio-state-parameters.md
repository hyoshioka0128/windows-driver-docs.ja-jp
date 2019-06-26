---
title: WDI_TLV_RADIO_STATE_PARAMETERS
description: WDI_TLV_RADIO_STATE_PARAMETERS は、OID_WDI_TASK_SET_RADIO_STATE の無線状態パラメーターを含む TLV です。
ms.assetid: D977DF8A-146C-4921-AE7C-5FBEC7FBA4C8
ms.date: 07/18/2017
keywords:
- WDI_TLV_RADIO_STATE_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 84c5929034c5035357134743d666c5bab3ee860a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366511"
---
# <a name="wditlvradiostateparameters"></a>WDI\_TLV\_ラジオ\_状態\_パラメーター


WDI\_TLV\_ラジオ\_状態\_パラメーターがのラジオ状態パラメーターを含む TLV [OID\_WDI\_タスク\_設定\_ラジオ\_状態](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-set-radio-state)します。

## <a name="tlv-type"></a>TLV 型


0xA0

## <a name="length"></a>長さ


UINT8 のサイズをバイト単位で。

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
<td>UINT8</td>
<td>必要なオプションの状態。
<p>有効な値は 0 (オプションはオフになっている) および 1 (オプションは有効ですです)。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>必要条件
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

 

 





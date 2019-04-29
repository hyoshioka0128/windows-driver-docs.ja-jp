---
title: WDI_TLV_IHV_TASK_DEVICE_CONTEXT
description: WDI_TLV_IHV_TASK_DEVICE_CONTEXT は、NDIS_STATUS_WDI_INDICATION_IHV_TASK_REQUEST の IHV で提供されるデバイス コンテキストを含む TLV です。
ms.assetid: FBFE8931-DF29-4605-A14D-12CEC0433086
ms.date: 07/18/2017
keywords:
- WDI_TLV_IHV_TASK_DEVICE_CONTEXT ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: b9f42ab8d6b3213e04229945447cbd1b28283fd3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392377"
---
# <a name="wditlvihvtaskdevicecontext"></a>WDI\_TLV\_IHV\_タスク\_デバイス\_コンテキスト


WDI\_TLV\_IHV\_タスク\_デバイス\_コンテキストがの IHV で提供されるデバイス コンテキストを含む TLV [NDIS\_状態\_WDI\_INDICATION\_IHV\_タスク\_要求](https://msdn.microsoft.com/library/windows/hardware/dn925637)します。

## <a name="tlv-type"></a>TLV 型


0xE0

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 型      | 説明                                                                    |
|-----------|--------------------------------------------------------------------------------|
| UINT8\[\] | IHV タスクに転送されるデバイスを IHV で提供されるコンテキスト情報。 |

 

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

 

 





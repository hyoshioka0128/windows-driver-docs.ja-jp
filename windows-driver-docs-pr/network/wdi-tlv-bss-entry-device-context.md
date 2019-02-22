---
title: WDI_TLV_BSS_ENTRY_DEVICE_CONTEXT
description: WDI_TLV_BSS_ENTRY_DEVICE_CONTEXT は、BSS エントリのデバイス コンテキストを含んでいる TLV です。
ms.assetid: 5672294B-C6C0-43A3-9553-D6309F64F4A6
ms.date: 07/18/2017
keywords:
- WDI_TLV_BSS_ENTRY_DEVICE_CONTEXT ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: bb67a5d4108599a2389da46c3bf3ad339d9ae10a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536913"
---
# <a name="wditlvbssentrydevicecontext"></a>WDI\_TLV\_BSS\_エントリ\_デバイス\_コンテキスト


WDI\_TLV\_BSS\_エントリ\_デバイス\_コンテキストが BSS エントリのデバイス コンテキストを含んでいる TLV します。

## <a name="tlv-type"></a>TLV 型


0 xd

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 種類      | 説明                                                                                                                                                                                                                                                                                |
|-----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8\[\] | コンテキスト データを指定する UINT8 要素の配列。 このコンテキストは IHV コンポーネントによって提供され、IHV コンポーネントが維持する必要がある BSS ごとのエントリの状態を格納するために使用できます。 有効期間管理を回避するためには、問題と、IHV コンポーネントは、この TLV でポインターを使用しない必要があります。 |

 

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

 

 





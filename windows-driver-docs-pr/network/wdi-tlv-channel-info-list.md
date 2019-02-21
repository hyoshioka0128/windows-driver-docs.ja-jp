---
title: WDI_TLV_CHANNEL_INFO_LIST
description: WDI_TLV_CHANNEL_INFO_LIST では、チャネルのリストを含む TLV です。
ms.assetid: D1B82F4F-6722-4D54-B6FF-B7F1309F8C0E
ms.date: 07/18/2017
keywords:
- WDI_TLV_CHANNEL_INFO_LIST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 7bfd6f2954c03c795c2e64eb8ae1a62fccaa8cfb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536972"
---
# <a name="wditlvchannelinfolist"></a>WDI\_TLV\_チャネル\_情報\_一覧


WDI\_TLV\_チャネル\_情報\_リストは、チャネルのリストを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x41

## <a name="length"></a>長さ


WDI の配列のサイズをバイト単位で\_チャネル\_数 (UINT32) 構造体。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 種類       | 説明                 |
|------------|-----------------------------|
| UINT32\[\] | Wi-fi のチャネルの配列。 |

 

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

 

 





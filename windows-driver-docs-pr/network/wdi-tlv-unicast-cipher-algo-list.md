---
title: WDI_TLV_UNICAST_CIPHER_ALGO_LIST
description: WDI_TLV_UNICAST_CIPHER_ALGO_LIST では、ユニキャスト暗号アルゴリズムの一覧を含む TLV です。
ms.assetid: 67FAEE8A-1CD6-4430-92C1-84E9F43BEF63
ms.date: 07/18/2017
keywords:
- WDI_TLV_UNICAST_CIPHER_ALGO_LIST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 8c8436230dcde0526cd3084b9d3baf913282a8be
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67357323"
---
# <a name="wditlvunicastcipheralgolist"></a>WDI\_TLV\_ユニキャスト\_暗号\_ALGO\_一覧


WDI\_TLV\_ユニキャスト\_暗号\_ALGO\_リストがユニキャスト暗号アルゴリズムの一覧を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x3E

## <a name="length"></a>長さ


配列のサイズをバイト単位で[ **WDI\_暗号\_アルゴリズム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_cipher_algorithm)構造体。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 型                                                            | 説明                            |
|-----------------------------------------------------------------|----------------------------------------|
| [**WDI\_暗号\_アルゴリズム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_cipher_algorithm)\[\] | ユニキャスト暗号アルゴリズムの配列。 |

 

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

 

 





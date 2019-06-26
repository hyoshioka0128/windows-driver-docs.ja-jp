---
title: WDI_TLV_AUTH_ALGO_LIST
description: WDI_TLV_AUTH_ALGO_LIST では、認証アルゴリズムの一覧を含む TLV です。
ms.assetid: 6F5EC21B-C923-45ED-B62E-302D916AABE5
ms.date: 07/18/2017
keywords:
- WDI_TLV_AUTH_ALGO_LIST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: b8043fceaf8e6ce8b59d05eaf2a43580b9387b3e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386960"
---
# <a name="wditlvauthalgolist"></a>WDI\_TLV\_AUTH\_ALGO\_一覧


WDI\_TLV\_AUTH\_ALGO\_リストは、認証アルゴリズムの一覧を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x3c です.

## <a name="length"></a>長さ


配列のサイズをバイト単位で[ **WDI\_AUTH\_アルゴリズム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_auth_algorithm)構造体。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 型                                                        | 説明                            |
|-------------------------------------------------------------|----------------------------------------|
| [**WDI\_AUTH\_アルゴリズム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_auth_algorithm)\[\] | 認証アルゴリズムの配列。 |

 

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

 

 





---
title: WDI_TLV_MULTICAST_CIPHER_ALGO_LIST
description: WDI_TLV_MULTICAST_CIPHER_ALGO_LIST は、マルチキャスト暗号アルゴリズムの一覧を含む TLV です。
ms.assetid: 55CDD295-6BDA-4F3A-B01F-FC9D5FB38355
ms.date: 07/18/2017
keywords:
- WDI_TLV_MULTICAST_CIPHER_ALGO_LIST ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: aae75b2ca8f73b478d14d475939ab6ca259f2f26
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842878"
---
# <a name="wdi_tlv_multicast_cipher_algo_list"></a>WDI\_TLV\_マルチキャスト\_暗号\_ALGO\_一覧


WDI\_TLV\_マルチキャスト\_暗号\_ALGO\_LIST は、マルチキャスト暗号アルゴリズムの一覧を含む TLV です。

## <a name="tlv-type"></a>TLV 型


0x3D

## <a name="length"></a>長さ


[**WDI\_暗号\_アルゴリズム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_cipher_algorithm)構造体の配列のサイズ (バイト単位)。 配列には1つ以上の要素が含まれている必要があります。

## <a name="values"></a>値


| タスクバーの検索ボックスに                                                            | 説明                              |
|-----------------------------------------------------------------|------------------------------------------|
| [**WDI\_暗号\_アルゴリズム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_cipher_algorithm)\[\] | マルチキャスト暗号アルゴリズムの配列。 |

 

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
<td>Wditypes</td>
</tr>
</tbody>
</table>

 

 





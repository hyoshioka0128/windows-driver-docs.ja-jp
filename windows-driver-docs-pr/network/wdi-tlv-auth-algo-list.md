---
title: WDI_TLV_AUTH_ALGO_LIST
description: WDI_TLV_AUTH_ALGO_LIST は、認証アルゴリズムの一覧を含む TLV です。
ms.assetid: 6F5EC21B-C923-45ED-B62E-302D916AABE5
ms.date: 07/18/2017
keywords:
- WDI_TLV_AUTH_ALGO_LIST ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 2666c667b90c1f3faec4e9e525d2a4f7c545d464
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842880"
---
# <a name="wdi_tlv_auth_algo_list"></a>WDI\_TLV\_AUTH\_ALGO\_LIST


WDI\_TLV\_AUTH\_ALGO\_LIST は、認証アルゴリズムの一覧を含む TLV です。

## <a name="tlv-type"></a>TLV 型


0X3c です

## <a name="length"></a>長さ


[**WDI\_AUTH\_アルゴリズム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_auth_algorithm)構造体の配列のサイズ (バイト単位)。 配列には1つ以上の要素が含まれている必要があります。

## <a name="values"></a>値


| タスクバーの検索ボックスに                                                        | 説明                            |
|-------------------------------------------------------------|----------------------------------------|
| [**WDI\_AUTH\_ALGORITHM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_auth_algorithm)\[\] | 認証アルゴリズムの配列。 |

 

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

 

 





---
title: WDI_TLV_COUNTRY_REGION_LIST
description: WDI_TLV_COUNTRY_REGION_LIST では、国または地域コードの一覧を含む TLV です。
ms.assetid: 675C176F-EE7A-41E0-9770-4D810F29E7BF
ms.date: 07/18/2017
keywords:
- WDI_TLV_COUNTRY_REGION_LIST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: defc626f88ee4d9ba0d14e0f0e1a7107c784bf78
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348188"
---
# <a name="wditlvcountryregionlist"></a>WDI\_TLV\_国\_リージョン\_一覧


WDI\_TLV\_国\_リージョン\_リストは、国または地域コードの一覧を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x12

## <a name="length"></a>長さ


WDI の配列のサイズをバイト単位で\_国\_リージョン\_リストの要素。 配列には、1 つ以上の要素を含める必要があります。

**注**  WDI\_国\_リージョン\_一覧が WDI 構造ではありません。 WDI TLV パーサー ジェネレーターで定義されているし、ドキュメントの目的でのみ使用されます。

 

## <a name="values"></a>値


| 型                           | 説明                          |
|--------------------------------|--------------------------------------|
| WDI\_国\_リージョン\_一覧\[\] | 国または地域コードの配列。 |

 

WDI\_国\_リージョン\_リストは、次の要素で構成されます。

| 種類       | 説明               |
|------------|---------------------------|
| UINT8\[3\] | 国または地域コード。 |

 

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

 

 





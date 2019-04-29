---
title: WDI_TLV_HESSID_INFO
description: WDI_TLV_HESSID_INFO は、HESSIDs、ネットワーク アクセスの種類、およびホット スポットを示す値の要素の一覧を含む HESSID 情報を含む TLV です。
ms.assetid: 60D130AC-8249-4B60-B46C-8B83FDDB148F
ms.date: 07/18/2017
keywords:
- WDI_TLV_HESSID_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 097f074b8be8f68614e6b760bb7e987d0f34fd5d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324411"
---
# <a name="wditlvhessidinfo"></a>WDI\_TLV\_HESSID\_情報


WDI\_TLV\_HESSID\_情報が HESSIDs、ネットワーク アクセスの種類、およびホット スポットを示す値の要素の一覧を含む HESSID 情報を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0 xff の場合

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                                                 | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                                              |
|--------------------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_ACCESS\_NETWORK\_TYPE**](wdi-tlv-access-network-type.md)               |                                |          | 接続されているネットワークのプローブ要求で使用するアクセスのネットワークの種類。 |
| [**WDI\_TLV\_HESSID**](wdi-tlv-hessid.md)                                           |                                |          | 接続にポートが許可されている HESSIDs の一覧。                              |
| [**WDI\_TLV\_ホット スポット\_INDICATION\_要素**](wdi-tlv-hotspot-indication-element.md) |                                |          | アソシエーションの要求で使用されるホット スポットを示す値の要素。                    |

 

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

 

 





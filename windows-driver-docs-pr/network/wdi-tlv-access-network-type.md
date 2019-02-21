---
title: WDI_TLV_ACCESS_NETWORK_TYPE
description: WDI_TLV_ACCESS_NETWORK_TYPE では、ネットワーク アクセスの種類を含む TLV です。
ms.assetid: AE344FDB-3B87-4F4E-BFF5-4569918E8465
ms.date: 07/18/2017
keywords:
- WDI_TLV_ACCESS_NETWORK_TYPE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: f18558db36fbaa874af7a6a9ef6cf4239381da7f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550689"
---
# <a name="wditlvaccessnetworktype"></a>WDI\_TLV\_アクセス\_ネットワーク\_型


WDI\_TLV\_アクセス\_ネットワーク\_型は、ネットワーク アクセスの種類を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x100

## <a name="length"></a>長さ


UINT8 のサイズをバイト単位で。

## <a name="values"></a>値


| 種類  | 説明                                                                              |
|-------|------------------------------------------------------------------------------------------|
| UINT8 | 接続されているネットワークのプローブ要求で使用するアクセスのネットワークの種類。 |

 

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

 

 





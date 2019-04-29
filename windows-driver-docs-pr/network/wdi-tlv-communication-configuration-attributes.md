---
title: WDI_TLV_COMMUNICATION_CONFIGURATION_ATTRIBUTES
description: WDI_TLV_COMMUNICATION_CONFIGURATION_ATTRIBUTES では、ホスト アダプターの通信プロトコルの構成属性を含む TLV です。
ms.assetid: A779FA2D-D3E0-4FC9-9A8A-09B6E3CFF758
ms.date: 07/18/2017
keywords:
- WDI_TLV_COMMUNICATION_CONFIGURATION_ATTRIBUTES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 5d89bd797aefc00967f7794350c31ec41620d046
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331223"
---
# <a name="wditlvcommunicationconfigurationattributes"></a>WDI\_TLV\_通信\_構成\_属性


WDI\_TLV\_通信\_構成\_属性は、ホスト アダプターの通信プロトコルの構成の属性を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x20

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                                                | 許可されている複数の TLV インスタンス | 省略可能 | 説明                     |
|-------------------------------------------------------------------------------------|--------------------------------|----------|---------------------------------|
| [**WDI\_TLV\_通信\_機能**](wdi-tlv-communication-capabilities.md) |                                | x        | 通信の機能。 |

 

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

 

 





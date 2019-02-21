---
title: WDI_TLV_IPV6_CHECKSUM_OFFLOAD
description: WDI_TLV_IPV6_CHECKSUM_OFFLOAD では、IPv6 のチェックサム オフロード機能を含む TLV です。
ms.assetid: 878471F5-8118-4D0A-87BC-E44DE7A713DF
ms.date: 07/18/2017
keywords:
- WDI_TLV_IPV6_CHECKSUM_OFFLOAD ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 7297b677ce816088fdc78e4679b366e4ff5465b9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532630"
---
# <a name="wditlvipv6checksumoffload"></a>WDI\_TLV\_IPV6\_チェックサム\_オフロード


WDI\_TLV\_IPV6\_チェックサム\_オフロードが IPv6 のチェックサム オフロード機能を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0xD0

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                                                                 | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                  |
|------------------------------------------------------------------------------------------------------|--------------------------------|----------|----------------------------------------------|
| [**WDI\_TLV\_チェックサム\_オフロード\_V6\_TX\_パラメーター**](wdi-tlv-checksum-offload-v6-tx-parameters.md) |                                |          | Tx チェックサムのパラメーターは、IPv6 のオフロードします。 |
| [**WDI\_TLV\_チェックサム\_オフロード\_V6\_RX\_パラメーター**](wdi-tlv-checksum-offload-v6-rx-parameters.md) |                                |          | Rx のチェックサムのパラメーターは、IPv6 のオフロードします。 |

 

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

 

 





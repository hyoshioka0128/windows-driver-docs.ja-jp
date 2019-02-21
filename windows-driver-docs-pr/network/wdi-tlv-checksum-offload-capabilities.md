---
title: WDI_TLV_CHECKSUM_OFFLOAD_CAPABILITIES
description: WDI_TLV_CHECKSUM_OFFLOAD_CAPABILITIES では、IPv4 と IPv6 のチェックサム オフロード機能を含む TLV です。
ms.assetid: 400D532F-CAAA-40F9-8001-EE460D4C89F9
ms.date: 07/18/2017
keywords:
- WDI_TLV_CHECKSUM_OFFLOAD_CAPABILITIES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 7bcfede0805a8f792eb7aabc6210e928be3e619d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535411"
---
# <a name="wditlvchecksumoffloadcapabilities"></a>WDI\_TLV\_チェックサム\_オフロード\_機能


WDI\_TLV\_チェックサム\_オフロード\_機能は、IPv4 と IPv6 のチェックサム オフロード機能を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0xCB

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                                       | 許可されている複数の TLV インスタンス | 省略可能 | 説明                           |
|----------------------------------------------------------------------------|--------------------------------|----------|---------------------------------------|
| [**WDI\_TLV\_IPV4\_チェックサム\_オフロード**](wdi-tlv-ipv4-checksum-offload.md) |                                |          | パラメーターの IPv4 チェックサム オフロードします。 |
| [**WDI\_TLV\_IPV6\_チェックサム\_オフロード**](wdi-tlv-ipv6-checksum-offload.md) |                                |          | IPv6 のチェックサムのパラメーターの負荷を軽減します。 |

 

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

 

 





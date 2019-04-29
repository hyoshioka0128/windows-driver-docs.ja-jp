---
title: WDI_TLV_IPV4_CHECKSUM_OFFLOAD
description: WDI_TLV_IPV4_CHECKSUM_OFFLOAD では、IPv4 のチェックサム オフロード機能を含む TLV です。
ms.assetid: FCC5880E-4323-4A24-98C6-CE7C84D03C16
ms.date: 07/18/2017
keywords:
- WDI_TLV_IPV4_CHECKSUM_OFFLOAD ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 856197e294922427b34d1e28f4795aa575c82453
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327598"
---
# <a name="wditlvipv4checksumoffload"></a>WDI\_TLV\_IPV4\_チェックサム\_オフロード


WDI\_TLV\_IPV4\_チェックサム\_オフロードが IPv4 のチェックサム オフロード機能を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0xCF

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                                                                 | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                  |
|------------------------------------------------------------------------------------------------------|--------------------------------|----------|----------------------------------------------|
| [**WDI\_TLV\_チェックサム\_オフロード\_V4\_TX\_パラメーター**](wdi-tlv-checksum-offload-v4-tx-parameters.md) |                                |          | Tx チェックサムのパラメーターは、IPv4 のオフロードします。 |
| [**WDI\_TLV\_チェックサム\_オフロード\_V4\_RX\_パラメーター**](wdi-tlv-checksum-offload-v4-rx-parameters.md) |                                |          | Rx のチェックサムのパラメーターは、IPv4 のオフロードします。 |

 

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

 

 





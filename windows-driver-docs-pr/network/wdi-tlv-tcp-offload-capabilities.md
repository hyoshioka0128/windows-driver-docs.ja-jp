---
title: WDI_TLV_TCP_OFFLOAD_CAPABILITIES
description: WDI_TLV_TCP_OFFLOAD_CAPABILITIES では、TCP/IP のオフロード機能を含む TLV です。
ms.assetid: 9B3428CC-C9B4-4769-BD97-F25920C4AAF2
ms.date: 07/18/2017
keywords:
- WDI_TLV_TCP_OFFLOAD_CAPABILITIES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 8844720123bae2835abf537242605c5bb7734064
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557301"
---
# <a name="wditlvtcpoffloadcapabilities"></a>WDI\_TLV\_TCP\_オフロード\_機能


WDI\_TLV\_TCP\_オフロード\_機能は、TCP/IP のオフロード機能を含む TLV します。

記載されている機能の値が報告[ **NDIS\_TCP\_IP\_チェックサム\_オフロード**](https://msdn.microsoft.com/library/windows/hardware/ff567878)します。 NDIS を使用して、\_オフロード\_いない\_サポートと NDIS\_オフロード\_を介して機能を指定する際にサポートされている[OID\_WDI\_GET\_アダプター\_機能](https://msdn.microsoft.com/library/windows/hardware/dn925838)します。 FIPS モードとの接続、オフロード、UE によってオフになっています。

## <a name="tlv-type"></a>TLV 型


0xCA

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                                                                        | 許可されている複数の TLV インスタンス | 省略可能 | 説明                         |
|-------------------------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------|
| [**WDI\_TLV\_チェックサム\_オフロード\_機能**](wdi-tlv-checksum-offload-capabilities.md)                  |                                |          | チェックサム オフロード機能します。      |
| [**WDI\_TLV\_LSO\_V1\_機能**](wdi-tlv-lso-v1-capabilities.md)                                      |                                |          | 大規模なオフロード V1 の送信機能。 |
| [**WDI\_TLV\_LSO\_V2\_機能**](wdi-tlv-lso-v2-capabilities.md)                                      |                                |          | 大規模なオフロード V2 の送信機能。 |
| [**WDI\_TLV\_受信\_COALESCE\_オフロード\_機能**](wdi-tlv-receive-coalesce-offload-capabilities.md) |                                |          | オフロード機能が表示されます。       |
| [**WDI_TLV_OFFLOAD_SCOPE**](wdi-tlv-offload-scope.md) |   |   | のみまたはすべてのポートで STA ポートにオフロードを適用するかどうかを示します。 802.11ad に現在適用可能なアダプターのみです。 |

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

 

 





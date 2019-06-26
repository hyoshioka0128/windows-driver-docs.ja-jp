---
title: WDI_TLV_P2P_DISCOVERED_SERVICE_ENTRY
description: WDI_TLV_P2P_DISCOVERED_SERVICE_ENTRY では、検出されたサービスのエントリを含む TLV です。
ms.assetid: B8D453FF-49CA-4106-97DA-008893760E92
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_DISCOVERED_SERVICE_ENTRY ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 3eb08cb79d4e6964a2157733c7a210a9f1071330
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360720"
---
# <a name="wditlvp2pdiscoveredserviceentry"></a>WDI\_TLV\_P2P\_検出\_サービス\_エントリ


WDI\_TLV\_P2P\_検出\_サービス\_エントリが検出されたサービスのエントリを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x112

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                                           | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                                                                                                                               |
|--------------------------------------------------------------------------------|--------------------------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_サービス\_名**](wdi-tlv-p2p-service-name.md)               |                                |          | Utf-8、最大 255 バイトでは、サービスの名前。                                                                                                                       |
| [**WDI\_TLV\_P2P\_サービス\_情報**](wdi-tlv-p2p-service-information.md) |                                | x        | サービスのサービス情報。                                                                                                                                  |
| [**WDI\_TLV\_P2P\_サービス\_状態**](wdi-tlv-p2p-service-status.md)           |                                |          | サービスのサービスの状態。                                                                                                                                        |
| [**WDI\_TLV\_P2P\_広告\_ID**](wdi-tlv-p2p-advertisement-id.md)       |                                |          | サービス インスタンスを一意に識別する ID です。                                                                                                                      |
| [**WDI\_TLV\_P2P\_CONFIG\_メソッド**](wdi-tlv-p2p-config-methods.md)           |                                |          | 構成の方法で定義されている[ **WDI\_WPS\_構成\_メソッド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_wps_configuration_method)します。 PinDisplay PinKeypad や WFDS は適用できます。 |

 

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

 

 





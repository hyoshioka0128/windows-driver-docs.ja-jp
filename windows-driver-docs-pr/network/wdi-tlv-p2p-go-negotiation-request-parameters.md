---
title: WDI_TLV_P2P_GO_NEGOTIATION_REQUEST_PARAMETERS
description: WDI_TLV_P2P_GO_NEGOTIATION_REQUEST_PARAMETERS では、グループの所有者を Wi-Fi Direct ネゴシエーション要求パラメーターを含む TLV です。
ms.assetid: C0B1832A-D315-47F8-87B8-73373CF55D44
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_GO_NEGOTIATION_REQUEST_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 5b20a790f7dc733425a41cf035f10b10856a4aa3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374682"
---
# <a name="wditlvp2pgonegotiationrequestparameters"></a>WDI\_TLV\_P2P\_移動\_ネゴシエーション\_要求\_パラメーター


WDI\_TLV\_P2P\_移動\_ネゴシエーション\_要求\_パラメーターは、グループの所有者を Wi-Fi Direct ネゴシエーション要求パラメーターを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x6E

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型                                              | 説明                                                                                                                                                                     |
|---------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8                                             | ローカル Wi-Fi Direct 移動して目的を指定します。 有効な値は、0 ~ 15 です。                                                                                                  |
| UINT8                                             | 目的の移動の判断基準にフィールドを指定します。                                                                                                                                   |
| UINT16                                            | 移動の構成のタイムアウトをミリ秒単位で指定します。                                                                                                                         |
| UINT16                                            | クライアント構成のタイムアウトをミリ秒単位で指定します。                                                                                                                     |
| [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address) | インターフェイスのアドレスを対象としています。 後で Wi-Fi Direct 接続のローカルの MAC アドレスを指定します。                                                                                |
| UINT8                                             | Wi-Fi Direct グループ機能に対応するビットマスクを指定します。 ビットマスクは、Wi-fi P2P technical specification 表 13 グループ機能のビットマップ定義で定義されているものと一致します。 |
| UINT8                                             | グループ機能ビットマップ上でオペレーティング システムによって設定するビットを指定します。                                                                                            |

 

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

 

 





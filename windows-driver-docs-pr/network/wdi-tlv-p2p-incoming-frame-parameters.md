---
title: WDI_TLV_P2P_INCOMING_FRAME_PARAMETERS
description: WDI_TLV_P2P_INCOMING_FRAME_PARAMETERS では、受信の Wi-Fi Direct アクション フレーム パラメーターを含む TLV です。
ms.assetid: 8E530962-E4DC-4845-8A5F-87AC4E000DA8
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_INCOMING_FRAME_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 91654e9bff7e8af54f6da445ad2a2e272c4b1f2d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374680"
---
# <a name="wditlvp2pincomingframeparameters"></a>WDI\_TLV\_P2P\_受信\_フレーム\_パラメーター


WDI\_TLV\_P2P\_受信\_フレーム\_パラメーターは受信 Wi-Fi Direct アクション フレームのパラメーターを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x7A

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型                                                                    | 説明                                        |
|-------------------------------------------------------------------------|----------------------------------------------------|
| [**WDI\_P2P\_アクション\_フレーム\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_p2p_action_frame_type) | 受信操作のフレームの型。             |
| [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address)                       | リモート ピアの MAC アドレス。                |
| UINT8                                                                   | Wi-Fi Direct ダイアログ トークンのトランザクション。 |

 

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

 

 





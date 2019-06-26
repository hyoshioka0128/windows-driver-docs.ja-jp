---
title: WDI_TLV_P2P_SEND_ACTION_FRAME_RESULT_PARAMETERS
description: WDI_TLV_P2P_SEND_ACTION_FRAME_RESULT_PARAMETERS は、Wi-Fi Direct を含む TLV がフレームのアクション結果のパラメーターを送信します。
ms.assetid: A0B234F2-081B-4027-9B42-76401F600707
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_SEND_ACTION_FRAME_RESULT_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 214aed1e2bf69476a68d96911eb38fac840fb97d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353291"
---
# <a name="wditlvp2psendactionframeresultparameters"></a>WDI\_TLV\_P2P\_送信\_アクション\_フレーム\_結果\_パラメーター


WDI\_TLV\_P2P\_送信\_アクション\_フレーム\_結果\_パラメーターは、Wi-Fi Direct を含む TLV がフレームのアクション結果のパラメーターを送信します。

## <a name="tlv-type"></a>TLV 型


0xAE

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型                                              | 説明                                           |
|---------------------------------------------------|-------------------------------------------------------|
| [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address) | ターゲット Wi-Fi Direct デバイスのデバイスのアドレス。 |
| UINT8                                             | Wi-Fi Direct ダイアログ トークンこのトランザクションにします。   |

 

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

 

 





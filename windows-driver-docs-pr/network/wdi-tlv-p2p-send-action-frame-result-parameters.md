---
title: WDI_TLV_P2P_SEND_ACTION_FRAME_RESULT_PARAMETERS
description: WDI_TLV_P2P_SEND_ACTION_FRAME_RESULT_PARAMETERS は、Wi-fi ダイレクト送信アクションフレームの結果パラメーターを含む TLV です。
ms.assetid: A0B234F2-081B-4027-9B42-76401F600707
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_SEND_ACTION_FRAME_RESULT_PARAMETERS ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 76290f15188154225c5704cc6a2dacf6f81ee785
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845123"
---
# <a name="wdi_tlv_p2p_send_action_frame_result_parameters"></a>WDI\_TLV\_P2P\_\_アクションの送信\_フレーム\_結果\_パラメーター


WDI\_TLV\_P2P\_SEND\_ACTION\_FRAME\_RESULT\_PARAMETERS は、Wi-fi Direct SEND Action Frame result パラメーターを含む TLV です。

## <a name="tlv-type"></a>TLV 型


0xAE

## <a name="length"></a>長さ


含まれているすべての要素のサイズの合計 (バイト単位)。

## <a name="values"></a>値


| タスクバーの検索ボックスに                                              | 説明                                           |
|---------------------------------------------------|-------------------------------------------------------|
| [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | ターゲット Wi-fi ダイレクトデバイスのデバイスアドレス。 |
| UINT8                                             | このトランザクションの Wi-fi ダイレクトダイアログトークン。   |

 

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
<td>Wditypes</td>
</tr>
</tbody>
</table>

 

 





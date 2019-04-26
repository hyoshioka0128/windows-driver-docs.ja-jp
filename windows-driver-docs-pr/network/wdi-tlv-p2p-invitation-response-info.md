---
title: WDI_TLV_P2P_INVITATION_RESPONSE_INFO
description: WDI_TLV_P2P_INVITATION_RESPONSE_INFO では、Wi-Fi Direct 招待応答情報を含む TLV です。
ms.assetid: DFF1649A-1CBE-4E0B-8EB2-6E10F539C72F
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_INVITATION_RESPONSE_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: c22055bf6c9deedb95d2dd076b8c6a45dad76104
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347229"
---
# <a name="wditlvp2pinvitationresponseinfo"></a>WDI\_TLV\_P2P\_招待\_応答\_情報


WDI\_TLV\_P2P\_招待\_応答\_情報は、Wi-Fi Direct 招待応答情報を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x7E

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                                                                  | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                      |
|-------------------------------------------------------------------------------------------------------|--------------------------------|----------|--------------------------------------------------|
| [**WDI\_TLV\_P2P\_INVITATION\_RESPONSE\_PARAMETERS**](wdi-tlv-p2p-invitation-response-parameters.md) |                                |          | Wi-Fi Direct 招待応答のパラメーター。 |
| [**WDI\_TLV\_P2P\_グループ\_BSSID**](wdi-tlv-p2p-group-bssid.md)                                        |                                | x        | ローカル Wi-Fi Direct GO 用グループ BSSID します。       |
| [**WDI\_TLV\_P2P\_チャネル\_数**](wdi-tlv-p2p-channel-number.md)                                  |                                | x        | Wi-Fi Direct GO 用の運用チャネル。       |

 

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

 

 





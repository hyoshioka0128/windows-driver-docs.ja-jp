---
title: WDI_TLV_P2P_INVITATION_REQUEST_INFO
description: WDI_TLV_P2P_INVITATION_REQUEST_INFO では、Wi-Fi Direct 招待要求情報を含む TLV です。
ms.assetid: 055B0F6D-2B68-495D-8253-2D213D699383
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_INVITATION_REQUEST_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: dbd853552a9a8d46c798b735829ed50357058944
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536554"
---
# <a name="wditlvp2pinvitationrequestinfo"></a>WDI\_TLV\_P2P\_招待\_要求\_情報


WDI\_TLV\_P2P\_招待\_要求\_情報は、Wi-Fi Direct 招待要求情報を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x7B

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                                                                | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                     |
|-----------------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------|
| [**WDI\_TLV\_P2P\_招待\_要求\_パラメーター**](wdi-tlv-p2p-invitation-request-parameters.md) |                                |          | Wi-Fi Direct 招待要求のパラメーター。 |
| [**WDI\_TLV\_P2P\_グループ\_BSSID**](wdi-tlv-p2p-group-bssid.md)                                      |                                | X        | BSSID グループです。                                |
| [**WDI\_TLV\_P2P\_チャネル\_数**](wdi-tlv-p2p-channel-number.md)                                |                                | X        | Wi-Fi Direct GO 用の運用チャネル。      |
| [**WDI\_TLV\_P2P\_グループ\_ID**](wdi-tlv-p2p-group-id.md)                                            |                                |          | Wi-Fi Direct 移動対象のグループ ID。        |

 

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

 

 





---
title: WDI_TLV_P2P_GO_NEGOTIATION_CONFIRMATION_INFO
description: WDI_TLV_P2P_GO_NEGOTIATION_CONFIRMATION_INFO では、Wi-Fi Direct 移動ネゴシエーション確認情報を含む TLV です。
ms.assetid: 1CC470FF-9301-4DF9-BE52-5FB1DCBF5415
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_GO_NEGOTIATION_CONFIRMATION_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 14acd2c2a81ab3abb1b01f9f0cd287b3b4e269cf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550529"
---
# <a name="wditlvp2pgonegotiationconfirmationinfo"></a>WDI\_TLV\_P2P\_移動\_ネゴシエーション\_確認\_情報


WDI\_TLV\_P2P\_移動\_ネゴシエーション\_確認\_情報は、Wi-Fi Direct 移動ネゴシエーション確認情報を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x88

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                                                                                   | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                                                                                             |
|------------------------------------------------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_移動\_ネゴシエーション\_確認\_パラメーター**](wdi-tlv-p2p-go-negotiation-confirmation-parameters.md) |                                |          | Wi-Fi Direct 移動ネゴシエーション確認パラメーター。                                                                                |
| [**WDI\_TLV\_P2P\_グループ\_ID**](wdi-tlv-p2p-group-id.md)                                                               |                                | X        | Wi-Fi Direct グループ id。                                                                                                              |
| [**WDI\_TLV\_P2P\_チャネル\_数**](wdi-tlv-p2p-channel-number.md)                                                   |                                | X        | リモート デバイスのリッスン チャネル。 GO のネゴシエーション確認フレームは、これが指定されてたびに、このチャネルで送信する必要があります。 |

 

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

 

 





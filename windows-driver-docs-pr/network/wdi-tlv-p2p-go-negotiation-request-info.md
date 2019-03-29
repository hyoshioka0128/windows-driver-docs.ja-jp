---
title: WDI_TLV_P2P_GO_NEGOTIATION_REQUEST_INFO
description: WDI_TLV_P2P_GO_NEGOTIATION_REQUEST_INFO では、グループの所有者を Wi-Fi Direct ネゴシエーション要求情報を含む TLV です。
ms.assetid: 4F505DF1-8D02-4421-956F-B7E1AF99D367
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_GO_NEGOTIATION_REQUEST_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: dc90926dfe3f8664e9de868746233d7010e6df3e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580963"
---
# <a name="wditlvp2pgonegotiationrequestinfo"></a>WDI\_TLV\_P2P\_移動\_ネゴシエーション\_要求\_情報


WDI\_TLV\_P2P\_移動\_ネゴシエーション\_要求\_情報は、グループの所有者を Wi-Fi Direct ネゴシエーション要求情報を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x6D

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 型                                                                                                         | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                                                                                         |
|--------------------------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_移動\_ネゴシエーション\_要求\_パラメーター**](wdi-tlv-p2p-go-negotiation-request-parameters.md) |                                |          | グループ所有者を Wi-Fi Direct ネゴシエーション要求パラメーターです。                                                                        |
| [**WDI\_TLV\_P2P\_チャネル\_数**](wdi-tlv-p2p-channel-number.md)                                         |                                | x        | リモート デバイスのリッスン チャネル。 これを指定すると、するたびに、GO のネゴシエーション要求フレームはこのチャネルで送信する必要があります。 |

 

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

 

 





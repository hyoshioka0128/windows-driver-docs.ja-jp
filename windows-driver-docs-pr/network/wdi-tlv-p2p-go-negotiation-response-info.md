---
title: WDI_TLV_P2P_GO_NEGOTIATION_RESPONSE_INFO
description: WDI_TLV_P2P_GO_NEGOTIATION_RESPONSE_INFO では、グループの所有者を Wi-Fi Direct ネゴシエーション応答の情報を含む TLV です。
ms.assetid: A0BB2CF6-4168-4973-92D0-EFF9F596F1BE
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_GO_NEGOTIATION_RESPONSE_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: ff66fdf272a0c2a480dcd5594f458feeaa6978fd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374547"
---
# <a name="wditlvp2pgonegotiationresponseinfo"></a>WDI\_TLV\_P2P\_移動\_ネゴシエーション\_応答\_情報


WDI\_TLV\_P2P\_移動\_ネゴシエーション\_応答\_情報は、グループの所有者を Wi-Fi Direct ネゴシエーション応答の情報を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x6f になります

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                                                                           | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                             |
|----------------------------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_移動\_ネゴシエーション\_応答\_パラメーター**](wdi-tlv-p2p-go-negotiation-response-parameters.md) |                                |          | グループ所有者を Wi-Fi Direct ネゴシエーション応答のパラメーターを指定します。 |
| [**WDI\_TLV\_P2P\_グループ\_ID**](wdi-tlv-p2p-group-id.md)                                                       |                                | x        | ローカル Wi-Fi Direct GO 用のグループ ID を指定します。                       |

 

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

 

 





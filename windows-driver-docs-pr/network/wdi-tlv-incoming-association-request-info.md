---
title: WDI_TLV_INCOMING_ASSOCIATION_REQUEST_INFO
description: WDI_TLV_INCOMING_ASSOCIATION_REQUEST_INFO では、受信の関連付け要求に関する情報を含む TLV です。
ms.assetid: E36ADD95-1751-4FCE-9032-900968878DEE
ms.date: 07/18/2017
keywords:
- WDI_TLV_INCOMING_ASSOCIATION_REQUEST_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 95889b682cf985c926f7d0237be439e52fc960a8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532227"
---
# <a name="wditlvincomingassociationrequestinfo"></a>WDI\_TLV\_受信\_アソシエーション\_要求\_情報


WDI\_TLV\_受信\_アソシエーション\_要求\_情報が入力方向の関連付け要求に関する情報を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x8F

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                                                                            | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                      |
|-----------------------------------------------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------------------|
| [**WDI\_TLV\_受信\_アソシエーション\_要求\_パラメーター**](wdi-tlv-incoming-association-request-parameters.md) |                                |          | アソシエーションの着信要求のパラメーター。             |
| [**WDI\_TLV\_アソシエーション\_要求\_フレーム**](wdi-tlv-association-request-frame.md)                              |                                |          | 関連要求フレーム。                                   |
| [**WDI\_TLV\_アソシエーション\_要求\_デバイス\_コンテキスト**](wdi-tlv-association-request-device-context.md)           |                                | X        | ポートに下位へ渡されるベンダー固有の情報。 |

 

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

 

 





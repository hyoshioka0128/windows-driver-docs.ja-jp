---
title: WDI_TLV_P2P_GO_NEGOTIATION_RESPONSE_PARAMETERS
description: WDI_TLV_P2P_GO_NEGOTIATION_RESPONSE_PARAMETERS では、着信移動ネゴシエーション応答のパラメーターを含む TLV です。
ms.assetid: 78C9B274-FAF0-4B2E-98A9-865A65105DA1
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_GO_NEGOTIATION_RESPONSE_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 340d90b32dc548bd96aef63ec032399e24fbaee4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582674"
---
# <a name="wditlvp2pgonegotiationresponseparameters"></a>WDI\_TLV\_P2P\_移動\_ネゴシエーション\_応答\_パラメーター


WDI\_TLV\_P2P\_移動\_ネゴシエーション\_応答\_パラメーターは受信移動ネゴシエーション応答のパラメーターを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x71

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型                                              | 説明                                                                                                                                                                     |
|---------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8                                             | Wi-Fi Direct の仕様で定義された、Wi-Fi Direct の状態コードを指定します。                                                                                           |
| UINT8                                             | ローカル Wi-Fi Direct 移動して目的を指定します。 これは、0 ~ 15 の値です。                                                                                                   |
| UINT8                                             | 移動して目的の判断基準にフィールドを指定します。                                                                                                                               |
| UINT16                                            | 移動の構成のタイムアウトをミリ秒単位で指定します。                                                                                                                         |
| UINT16                                            | クライアント構成のタイムアウトをミリ秒単位で指定します。                                                                                                                     |
| [**WDI\_MAC\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/dn926071) | インターフェイスのアドレスを対象としています。 以降の Wi-Fi Direct 接続のローカルの MAC アドレスを指定します。                                                                                 |
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

 

 





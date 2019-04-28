---
title: WDI_TLV_P2P_GO_NEGOTIATION_REQUEST_PARAMETERS
description: WDI_TLV_P2P_GO_NEGOTIATION_REQUEST_PARAMETERS では、グループの所有者を Wi-Fi Direct ネゴシエーション要求パラメーターを含む TLV です。
ms.assetid: C0B1832A-D315-47F8-87B8-73373CF55D44
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_GO_NEGOTIATION_REQUEST_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 43f215cd6191ee1825615c6f111ae229c73d4621
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363642"
---
# <a name="wditlvp2pgonegotiationrequestparameters"></a>WDI\_TLV\_P2P\_移動\_ネゴシエーション\_要求\_パラメーター


WDI\_TLV\_P2P\_移動\_ネゴシエーション\_要求\_パラメーターは、グループの所有者を Wi-Fi Direct ネゴシエーション要求パラメーターを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x6E

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型                                              | 説明                                                                                                                                                                     |
|---------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8                                             | ローカル Wi-Fi Direct 移動して目的を指定します。 有効な値は、0 ~ 15 です。                                                                                                  |
| UINT8                                             | 目的の移動の判断基準にフィールドを指定します。                                                                                                                                   |
| UINT16                                            | 移動の構成のタイムアウトをミリ秒単位で指定します。                                                                                                                         |
| UINT16                                            | クライアント構成のタイムアウトをミリ秒単位で指定します。                                                                                                                     |
| [**WDI\_MAC\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/dn926071) | インターフェイスのアドレスを対象としています。 後で Wi-Fi Direct 接続のローカルの MAC アドレスを指定します。                                                                                |
| UINT8                                             | Wi-Fi Direct グループ機能に対応するビットマスクを指定します。 ビットマスクは、Wi-fi P2P technical specification 表 13 グループ機能のビットマップ定義で定義されているものと一致します。 |
| UINT8                                             | グループ機能ビットマップ上でオペレーティング システムによって設定するビットを指定します。                                                                                            |

 

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

 

 





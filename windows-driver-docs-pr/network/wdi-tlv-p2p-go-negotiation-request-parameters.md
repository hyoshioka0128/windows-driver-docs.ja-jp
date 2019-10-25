---
title: WDI_TLV_P2P_GO_NEGOTIATION_REQUEST_PARAMETERS
description: WDI_TLV_P2P_GO_NEGOTIATION_REQUEST_PARAMETERS は、Wi-fi Direct グループ所有者ネゴシエーション要求パラメーターを含む TLV です。
ms.assetid: C0B1832A-D315-47F8-87B8-73373CF55D44
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_GO_NEGOTIATION_REQUEST_PARAMETERS ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 0af7172f4818fbadf945f527c11f8ca9bc6552eb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840443"
---
# <a name="wdi_tlv_p2p_go_negotiation_request_parameters"></a>WDI\_TLV\_P2P\_ゴー\_ネゴシエーション\_要求\_パラメーター


WDI\_TLV\_P2P\_移動\_ネゴシエーション\_要求\_パラメーターは、Wi-fi Direct グループ所有者ネゴシエーション要求パラメーターを含む TLV です。

## <a name="tlv-type"></a>TLV 型


0x6E

## <a name="length"></a>Length


含まれているすべての要素のサイズの合計 (バイト単位)。

## <a name="values"></a>値


| 種類                                              | 説明                                                                                                                                                                     |
|---------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8                                             | ローカル Wi-fi Direct の目的を指定します。 有効な値は 0 ~ 15 です。                                                                                                  |
| UINT8                                             | 実行インテントの同一ブレーカーフィールドを指定します。                                                                                                                                   |
| UINT16                                            | 構成の開始タイムアウトをミリ秒単位で指定します。                                                                                                                         |
| UINT16                                            | クライアント構成のタイムアウトをミリ秒単位で指定します。                                                                                                                     |
| [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 目的のインターフェイスアドレス。 今後の Wi-fi 直接接続に使用するローカル MAC アドレスを指定します。                                                                                |
| UINT8                                             | Wi-fi ダイレクトグループ機能のビットマスクを指定します。 ビットマスクは、Wi-fi P2P technical specification の表13グループ機能ビットマップ定義で定義されているものと一致します。 |
| UINT8                                             | 上のグループ機能ビットマップのオペレーティングシステムによって設定されたビットを指定します。                                                                                            |

 

<a name="requirements"></a>前提条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最低限のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小サーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>ヘッダー</p></td>
<td>Wditypes</td>
</tr>
</tbody>
</table>

 

 





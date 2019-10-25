---
title: WDI_TLV_P2P_GO_NEGOTIATION_RESPONSE_PARAMETERS
description: WDI_TLV_P2P_GO_NEGOTIATION_RESPONSE_PARAMETERS は、受信ネゴシエーション応答パラメーターを含む TLV です。
ms.assetid: 78C9B274-FAF0-4B2E-98A9-865A65105DA1
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_GO_NEGOTIATION_RESPONSE_PARAMETERS ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: db1a619edbb364754e2b291a30c0a95ad6a809c8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842357"
---
# <a name="wdi_tlv_p2p_go_negotiation_response_parameters"></a>WDI\_TLV\_P2P\_アクセス\_ネゴシエーション\_応答\_パラメーター


WDI\_TLV\_P2P\_TO\_ネゴシエーション\_応答\_パラメーターは、受信ネゴシエーション応答パラメーターを含む TLV です。

## <a name="tlv-type"></a>TLV 型


0x71

## <a name="length"></a>長さ


含まれているすべての要素のサイズの合計 (バイト単位)。

## <a name="values"></a>値


| タスクバーの検索ボックスに                                              | 説明                                                                                                                                                                     |
|---------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8                                             | Wi-fi direct 仕様で定義されている Wi-fi ダイレクトステータスコードを指定します。                                                                                           |
| UINT8                                             | ローカル Wi-fi Direct の目的を指定します。 0から15までの値です。                                                                                                   |
| UINT8                                             | 目的の結合ブレーカーフィールドを指定します。                                                                                                                               |
| UINT16                                            | 構成の開始タイムアウトをミリ秒単位で指定します。                                                                                                                         |
| UINT16                                            | クライアント構成のタイムアウトをミリ秒単位で指定します。                                                                                                                     |
| [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 目的のインターフェイスアドレス。 今後の Wi-fi 直接接続に使用するローカル MAC アドレスを指定します。                                                                                 |
| UINT8                                             | Wi-fi ダイレクトグループ機能のビットマスクを指定します。 ビットマスクは、Wi-fi P2P technical specification の表13グループ機能ビットマップ定義で定義されているものと一致します。 |
| UINT8                                             | 上のグループ機能ビットマップのオペレーティングシステムによって設定されたビットを指定します。                                                                                            |

 

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

 

 





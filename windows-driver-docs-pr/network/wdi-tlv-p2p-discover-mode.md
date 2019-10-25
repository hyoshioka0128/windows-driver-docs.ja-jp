---
title: WDI_TLV_P2P_DISCOVER_MODE
description: WDI_TLV_P2P_DISCOVER_MODE は、OID_WDI_TASK_P2P_DISCOVER の Wi-fi ダイレクト検出モード情報を含む TLV です。
ms.assetid: 430DDDBE-C861-4E85-BFAB-31670F77696D
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_DISCOVER_MODE ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: e367ef0826734593ca23562b7a4d25d5e9943b7a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840449"
---
# <a name="wdi_tlv_p2p_discover_mode"></a>WDI\_TLV\_P2P\_\_モードの検出


WDI\_TLV\_P2P\_DISCOVER\_モードは、 [OID\_WDI\_タスク\_P2P\_DISCOVER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-p2p-discover)の wi-fi Direct discovery モード情報を含む TLV です。

## <a name="tlv-type"></a>TLV 型


0xA9

## <a name="length"></a>Length


含まれているすべての要素のサイズの合計 (バイト単位)。

## <a name="values"></a>値


| 種類                                                                                       | 説明                                                                                                                                                                                                                     |
|--------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_P2P\_DISCOVER\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_p2p_discover_type)(UINT32)                    | ポートによって実行される探索の種類。                                                                                                                                                                              |
| UINT8                                                                                      | 完全なデバイスを検出する必要があるかどうかを示すフラグ。 有効な値は、0 (必須ではありません) と 1 (必須) です。 このフラグが0に設定されている場合は、部分的な検出が実行されることがあります。                                           |
| [**WDI\_P2P\_SCAN\_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_p2p_scan_type) (UINT32)                            | スキャンフェーズでポートによって実行されるスキャンの種類。                                                                                                                                                                     |
| [**WDI\_P2P\_SERVICE\_DISCOVERY\_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_p2p_service_discovery_type) (UINT32) | 実行するサービス検出の種類。                                                                                                                                                                                  |
| UINT8                                                                                      | スキャンの繰り返し回数。 フルスキャンプロシージャを繰り返す必要があるかどうかを指定します。 0に設定すると、タスクがホストによって中止されるまでスキャンを繰り返す必要があります。                                                                 |
| UINT32                                                                                     | スキャンの間隔。 [スキャンの繰り返し回数] が1に設定されていない場合、この時間は、要求されたチャネルのフルスキャンが完了した後にスキャン手順を繰り返すまでの、デバイスの待機時間 (ミリ秒) を指定します。 |

 

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

 

 





---
title: WDI_TLV_GET_AUTO_POWER_SAVE
description: WDI_TLV_GET_AUTO_POWER_SAVE は、OID_WDI_GET_AUTO_POWER_SAVE の自動省電力情報を含む TLV です。
ms.assetid: E57AD1CE-A252-4BB5-B983-11D3E46B7EC1
ms.date: 07/18/2017
keywords:
- WDI_TLV_GET_AUTO_POWER_SAVE ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: b5c32da28f27c2f15bba41b0a8f5b9ab5ce96164
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843627"
---
# <a name="wdi_tlv_get_auto_power_save"></a>WDI\_TLV\_\_自動\_POWER\_保存


WDI\_TLV\_GET\_AUTO\_POWER\_SAVE は、OID\_WDI\_の自動省電力情報を含む TLV です。[自動\_power\_保存](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-get-auto-power-save)します。

## <a name="tlv-type"></a>TLV 型


0xB3

## <a name="length"></a>長さ


含まれているすべての要素のサイズの合計 (バイト単位)。

## <a name="values"></a>値


| タスクバーの検索ボックスに                                                                               | 説明                                                                                                        |
|------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|
| UINT8                                                                              | ファームウェアの現在の AutoPSM の状態。                                                                                |
| UINT8                                                                              | 予約済み。                                                                                                          |
| UINT16                                                                             | 予約済み。                                                                                                          |
| UINT16                                                                             | ビーコンの間隔 (ミリ秒単位)。                                                                               |
| UINT8                                                                              | 標識間隔の単位 (たとえば、1) のリッスン間隔。                                          |
| UINT8                                                                              | 最後の低電力状態のリッスン間隔 (たとえば、5)。 最後の低電力状態がない場合は、を255に設定します。 |
| [**WDI\_POWER\_\_レベル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_power_save_level)(UINT32) の保存              | 電源モード。                                                                                                    |
| [**WDI\_POWER\_\_レベル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_power_save_level)(UINT32) の保存              | Dx の電源モード。                                                                                              |
| [**WDI\_POWER\_MODE\_REASON\_コード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_power_mode_reason_code)(UINT32) | 省電力状態とリッスン間隔を入力する理由。                                                  |
| UINT64                                                                             | 開始以降のミリ秒数。                                                                                          |
| UINT64                                                                             | 省電力モードのミリ秒。                                                                                   |
| UINT64                                                                             | 受信したマルチキャストパケットの数 (ブロードキャストを含む)。                                                         |
| UINT64                                                                             | ブロードキャストを含む、送信されたマルチキャストパケットの数。                                                             |
| UINT64                                                                             | 受信したユニキャストパケットの数。                                                                                |
| UINT64                                                                             | 送信されたユニキャストパケットの数。                                                                                    |

 

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

 

 





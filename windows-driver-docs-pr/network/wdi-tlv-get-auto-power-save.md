---
title: WDI_TLV_GET_AUTO_POWER_SAVE
description: WDI_TLV_GET_AUTO_POWER_SAVE は、自動電源を含む TLV が OID_WDI_GET_AUTO_POWER_SAVE の情報を保存します。
ms.assetid: E57AD1CE-A252-4BB5-B983-11D3E46B7EC1
ms.date: 07/18/2017
keywords:
- WDI_TLV_GET_AUTO_POWER_SAVE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: f325b181de800ae4ed1087d7d53042db0fddf74a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358541"
---
# <a name="wditlvgetautopowersave"></a>WDI\_TLV\_取得\_自動\_POWER\_保存


WDI\_TLV\_取得\_自動\_POWER\_保存が自動省電力の情報を含む TLV [OID\_WDI\_取得\_自動\_POWER\_保存](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-get-auto-power-save)します。

## <a name="tlv-type"></a>TLV 型


0xB3

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型                                                                               | 説明                                                                                                        |
|------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|
| UINT8                                                                              | 現在 AutoPSM のファームウェア状態。                                                                                |
| UINT8                                                                              | 予約済み。                                                                                                          |
| UINT16                                                                             | 予約済み。                                                                                                          |
| UINT16                                                                             | ビーコンの間隔 (ミリ秒)。                                                                               |
| UINT8                                                                              | リッスンの間隔 (たとえば、1) ビーコン間隔の単位。                                          |
| UINT8                                                                              | 最後の省電力状態 (たとえば、5) でリッスン間隔。 最後の省電力状態がない場合は、255 に設定します。 |
| [**WDI\_POWER\_保存\_レベル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_power_save_level) (UINT32)              | 電源モード。                                                                                                    |
| [**WDI\_POWER\_保存\_レベル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_power_save_level) (UINT32)              | Dx 電源モード。                                                                                              |
| [**WDI\_POWER\_モード\_理由\_コード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_power_mode_reason_code) (UINT32) | 省電力状態とリッスン間隔を入力することの理由です。                                                  |
| UINT64                                                                             | 開始以降のミリ秒数。                                                                                          |
| UINT64                                                                             | Power (ミリ秒) では、モードを保存します。                                                                                   |
| UINT64                                                                             | ブロードキャストを含む、受信マルチキャスト パケットの数。                                                         |
| UINT64                                                                             | などのブロードキャスト送信のマルチキャスト パケットの数。                                                             |
| UINT64                                                                             | 受信したユニキャスト パケットの数。                                                                                |
| UINT64                                                                             | 送信したユニキャスト パケットの数。                                                                                    |

 

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

 

 





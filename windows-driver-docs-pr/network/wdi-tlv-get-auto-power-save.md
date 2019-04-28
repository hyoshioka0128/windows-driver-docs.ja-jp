---
title: WDI_TLV_GET_AUTO_POWER_SAVE
description: WDI_TLV_GET_AUTO_POWER_SAVE は、自動電源を含む TLV が OID_WDI_GET_AUTO_POWER_SAVE の情報を保存します。
ms.assetid: E57AD1CE-A252-4BB5-B983-11D3E46B7EC1
ms.date: 07/18/2017
keywords:
- WDI_TLV_GET_AUTO_POWER_SAVE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 1f2f04352be7f538303c935cff4226ee9f6d958b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380552"
---
# <a name="wditlvgetautopowersave"></a>WDI\_TLV\_取得\_自動\_POWER\_保存


WDI\_TLV\_取得\_自動\_POWER\_保存が自動省電力の情報を含む TLV [OID\_WDI\_取得\_自動\_POWER\_保存](https://msdn.microsoft.com/library/windows/hardware/dn925840)します。

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
| [**WDI\_POWER\_保存\_レベル**](https://msdn.microsoft.com/library/windows/hardware/dn926107) (UINT32)              | 電源モード。                                                                                                    |
| [**WDI\_POWER\_保存\_レベル**](https://msdn.microsoft.com/library/windows/hardware/dn926107) (UINT32)              | Dx 電源モード。                                                                                              |
| [**WDI\_POWER\_モード\_理由\_コード**](https://msdn.microsoft.com/library/windows/hardware/dn926106) (UINT32) | 省電力状態とリッスン間隔を入力することの理由です。                                                  |
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

 

 





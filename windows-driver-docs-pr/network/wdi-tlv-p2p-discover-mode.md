---
title: WDI_TLV_P2P_DISCOVER_MODE
description: WDI_TLV_P2P_DISCOVER_MODE は、OID_WDI_TASK_P2P_DISCOVER Wi-Fi Direct 検出モードの情報を含む TLV です。
ms.assetid: 430DDDBE-C861-4E85-BFAB-31670F77696D
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_DISCOVER_MODE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 28f98a50800e27ccf65d7df12c9e7c70de50bf99
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532793"
---
# <a name="wditlvp2pdiscovermode"></a>WDI\_TLV\_P2P\_DISCOVER\_モード


WDI\_TLV\_P2P\_DISCOVER\_モードは、Wi-Fi Direct 検出モード情報を含む TLV [OID\_WDI\_タスク\_P2P\_DISCOVER](https://msdn.microsoft.com/library/windows/hardware/dn925955)します。

## <a name="tlv-type"></a>TLV 型


0xA9

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 種類                                                                                       | 説明                                                                                                                                                                                                                     |
|--------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_P2P\_DISCOVER\_型**](https://msdn.microsoft.com/library/windows/hardware/dn926093) (UINT32)                    | ポートで実行する探索の種類。                                                                                                                                                                              |
| UINT8                                                                                      | 完全なデバイスの検出が必要なかどうかを示すフラグです。 有効な値は 0 (不要) および 1 (必須です)。 このフラグが 0 に設定されている場合は、部分的な探索を実行できます。                                           |
| [**WDI\_P2P\_スキャン\_型**](https://msdn.microsoft.com/library/windows/hardware/dn926099) (UINT32)                            | スキャン フェーズでは、ポートで実行されるスキャンの種類。                                                                                                                                                                     |
| [**WDI\_P2P\_サービス\_検出\_型**](https://msdn.microsoft.com/library/windows/hardware/dn926101) (UINT32) | 実行するサービスの検出の種類。                                                                                                                                                                                  |
| UINT8                                                                                      | スキャンの繰り返し回数。 かどうか、フル スキャンの手順を繰り返す必要がありますを指定します。 かどうかを 0 に設定すると、スキャンする必要がありますまで繰り返されるホストにより、タスクが中止されます。                                                                 |
| UINT32                                                                                     | スキャンの間隔。 この時間をどのくらいの期間 (ミリ秒) を指定を 1 にスキャンの繰り返し回数が設定されていない場合デバイスを待機して、要求されたチャネルのフル スキャンを完了した後のスキャン手順を繰り返す必要があります。 |

 

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

 

 





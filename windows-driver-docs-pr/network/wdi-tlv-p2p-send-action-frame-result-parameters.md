---
title: WDI_TLV_P2P_SEND_ACTION_FRAME_RESULT_PARAMETERS
description: WDI_TLV_P2P_SEND_ACTION_FRAME_RESULT_PARAMETERS は、Wi-Fi Direct を含む TLV がフレームのアクション結果のパラメーターを送信します。
ms.assetid: A0B234F2-081B-4027-9B42-76401F600707
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_SEND_ACTION_FRAME_RESULT_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: c08ae3fd10a8f0c29b72bb842896b0a05495d67a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549493"
---
# <a name="wditlvp2psendactionframeresultparameters"></a>WDI\_TLV\_P2P\_送信\_アクション\_フレーム\_結果\_パラメーター


WDI\_TLV\_P2P\_送信\_アクション\_フレーム\_結果\_パラメーターは、Wi-Fi Direct を含む TLV がフレームのアクション結果のパラメーターを送信します。

## <a name="tlv-type"></a>TLV 型


0xAE

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 種類                                              | 説明                                           |
|---------------------------------------------------|-------------------------------------------------------|
| [**WDI\_MAC\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/dn926071) | ターゲット Wi-Fi Direct デバイスのデバイスのアドレス。 |
| UINT8                                             | Wi-Fi Direct ダイアログ トークンこのトランザクションにします。   |

 

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

 

 





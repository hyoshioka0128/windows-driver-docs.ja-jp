---
title: WDI_TLV_P2P_INCOMING_FRAME_PARAMETERS
description: WDI_TLV_P2P_INCOMING_FRAME_PARAMETERS では、受信の Wi-Fi Direct アクション フレーム パラメーターを含む TLV です。
ms.assetid: 8E530962-E4DC-4845-8A5F-87AC4E000DA8
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_INCOMING_FRAME_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 40bbfbf0b9f60090e1ba6cf1aa7256ec81388990
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347276"
---
# <a name="wditlvp2pincomingframeparameters"></a>WDI\_TLV\_P2P\_受信\_フレーム\_パラメーター


WDI\_TLV\_P2P\_受信\_フレーム\_パラメーターは受信 Wi-Fi Direct アクション フレームのパラメーターを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x7A

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型                                                                    | 説明                                        |
|-------------------------------------------------------------------------|----------------------------------------------------|
| [**WDI\_P2P\_アクション\_フレーム\_型**](https://msdn.microsoft.com/library/windows/hardware/dn926086) | 受信操作のフレームの型。             |
| [**WDI\_MAC\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/dn926071)                       | リモート ピアの MAC アドレス。                |
| UINT8                                                                   | Wi-Fi Direct ダイアログ トークンのトランザクション。 |

 

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

 

 





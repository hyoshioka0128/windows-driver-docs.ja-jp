---
title: WDI_TLV_BSS_ENTRY_SIGNAL_INFO
description: WDI_TLV_BSS_ENTRY_SIGNAL_INFO は、BSS エントリのシグナルの情報を含む TLV です。
ms.assetid: 4410F447-5226-4DF4-923D-11D10D0159CC
ms.date: 07/18/2017
keywords:
- WDI_TLV_BSS_ENTRY_SIGNAL_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 589ce10edc66861e06ec1721367e5876dce2dc32
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379182"
---
# <a name="wditlvbssentrysignalinfo"></a>WDI\_TLV\_BSS\_エントリ\_信号\_情報


WDI\_TLV\_BSS\_エントリ\_信号\_情報が BSS エントリのシグナルの情報を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0 xb

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型   | 説明                                                                                                                                                                        |
|--------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| INT32  | ピアからビーコンまたはプローブの応答の受信信号強度指標 (RSSI) 値。 この値は 1.0 ミリ ワット (dBm) を参照するデシベル単位で指定します。 |
| UINT32 | 0 ~ 100 の値で指定されたリンクの品質。 100 の値には、リンクの最高の品質を指定します。                                                                            |

 

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

 

 





---
title: WDI_TLV_SCAN_DWELL_TIME
description: WDI_TLV_SCAN_DWELL_TIME では、スキャン ドウェル時刻の設定を含む TLV です。
ms.assetid: A0C597E7-879C-43CC-BB86-4908AC31828F
ms.date: 07/18/2017
keywords:
- WDI_TLV_SCAN_DWELL_TIME ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 2bf470aba7780223e2d2d609b255198663a392ad
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538675"
---
# <a name="wditlvscandwelltime"></a>WDI\_TLV\_スキャン\_熟考\_時間


WDI\_TLV\_スキャン\_熟考\_時間はスキャン ドウェル時刻の設定を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x7

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 種類   | 説明                                                                                                                                                                           |
|--------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT32 | アクティブなチャネルについて熟考するミリ秒単位の時間を指定します。 これは、ヒントであり、最大のスキャンの時間の要件を満たす必要があります、アダプター独自ドウェル時刻を使用する場合。  |
| UINT32 | パッシブなチャネルについて熟考するミリ秒単位の時間を指定します。 これは、ヒントであり、最大のスキャンの時間の要件を満たす必要があります、アダプター独自ドウェル時刻を使用する場合。 |
| UINT32 | スキャンの合計 (ミリ秒) で、時間を指定します。 アダプターは、上記で指定した値以下にそのドウェル時間を制限、最大スキャン時間パラメーターが無視できます。          |

 

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

 

 





---
title: WDI_TLV_TCP_RSC_STATISTICS_PARAMETERS
description: WDI_TLV_TCP_RSC_STATISTICS_PARAMETERS は、OID_WDI_TCP_RSC_STATISTICS 用 TCP RSC の統計情報を含む TLV です。
ms.assetid: C1459DF6-6492-4C1F-A22D-2BDC6492B29C
ms.date: 07/18/2017
keywords:
- WDI_TLV_TCP_RSC_STATISTICS_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 26b1b9fa0f06a91546f308e077937cdd8fa4eca0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527272"
---
# <a name="wditlvtcprscstatisticsparameters"></a>WDI\_TLV\_TCP\_RSC\_統計\_パラメーター


WDI\_TLV\_TCP\_RSC\_統計\_パラメーターがの TCP RSC の統計情報を含む TLV [OID\_WDI\_TCP\_RSC\_統計](https://msdn.microsoft.com/library/windows/hardware/dn925966)します。

## <a name="tlv-type"></a>TLV 型


0xF3

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 種類   | 説明                                                                                                                                                                                                                               |
|--------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT64 | 結合されたパケットの合計数。                                                                                                                                                                                          |
| UINT64 | 結合されたバイトの合計数。                                                                                                                                                                                            |
| UINT64 | 合体パケットから形成されたパケットの合計数である結合のイベントの合計数。                                                                                                                     |
| UINT64 | RSC の合計数は、IP データグラムの長さを超えて以外の例外の数は、イベントを中止します。 この数は、パケットがハードウェア リソースの不足により統合しないケースを含める必要があります。 |

 

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

 

 





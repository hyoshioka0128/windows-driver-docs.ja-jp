---
title: WDI_TLV_PHY_CAPABILITIES
description: WDI_TLV_PHY_CAPABILITIES は、PHY 機能を含む TLV です。
ms.assetid: 8F482ED6-6594-4DB5-B53B-4424DAD32D36
ms.date: 07/18/2017
keywords:
- WDI_TLV_PHY_CAPABILITIES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 45426b6e8174a382807e04c71d10097f37bb0e3c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349330"
---
# <a name="wditlvphycapabilities"></a>WDI\_TLV\_PHY\_機能


WDI\_TLV\_PHY\_機能は PHY 機能を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x1B

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型                                        | 説明                                        |
|---------------------------------------------|----------------------------------------------------|
| [**WDI\_PHY\_型**](https://msdn.microsoft.com/library/windows/hardware/dn926105) | PHY 型を指定します。                           |
| UINT8                                       | PHY が CF ポーリングをサポートしているかどうかを指定します。 |
| UINT32                                      | MPDU の最大長を指定します。                 |
| UINT32                                      | 動作の温度クラスを指定します。         |
| UINT32                                      | アンテナの多様性のサポートを指定します。           |

 

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

 

 





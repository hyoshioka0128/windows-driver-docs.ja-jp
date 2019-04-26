---
title: WDI_TLV_ROAMING_NEEDED_PARAMETERS
description: WDI_TLV_ROAMING_NEEDED_PARAMETERS では、ローミングのトリガーの理由を含む TLV です。 これは、NDIS_STATUS_WDI_INDICATION_ROAMING_NEEDED ペイロードで使用されます。
ms.assetid: 152F923C-ECAE-4D50-A7B4-4B2309D5A3B5
ms.date: 07/18/2017
keywords:
- WDI_TLV_ROAMING_NEEDED_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: f1d14aa9cf18d423bbdf99dd86ba7a6cc87bd907
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359367"
---
# <a name="wditlvroamingneededparameters"></a>WDI\_TLV\_ローミング\_必要\_パラメーター


WDI\_TLV\_ローミング\_必要\_パラメーターは、ローミングのトリガーの理由を含む TLV します。 使用されます、 [NDIS\_状態\_WDI\_INDICATION\_ローミング\_必要](https://msdn.microsoft.com/library/windows/hardware/dn925648)ペイロード。

## <a name="tlv-type"></a>TLV 型


0x55

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型                                                | 説明                                                                                                                                      |
|-----------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_ASSOC\_状態**](https://msdn.microsoft.com/library/windows/hardware/dn897725) | ローミングのトリガーの理由を指定します。 ときに、 [OID\_WDI\_タスク\_ローミング](https://msdn.microsoft.com/library/windows/hardware/dn925958)がトリガーされると、この理由はそれに転送されます。 |

 

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

 

 





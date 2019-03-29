---
title: WDI_TLV_DISASSOCIATION_INDICATION_PARAMETERS
description: WDI_TLV_DISASSOCIATION_INDICATION_PARAMETERS は、NDIS_STATUS_WDI_INDICATION_DISASSOCIATION の関連付けの解除を示す値のパラメーターを含む TLV です。
ms.assetid: AD799DAA-B89D-4015-8DC5-53057C4DA43E
ms.date: 07/18/2017
keywords:
- WDI_TLV_DISASSOCIATION_INDICATION_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 47c58d1e3c69326d49447c3eace367cc69ad4b92
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570635"
---
# <a name="wditlvdisassociationindicationparameters"></a>WDI\_TLV\_戻せません\_INDICATION\_パラメーター


WDI\_TLV\_関連付け解除\_INDICATION\_パラメーターがの関連付けの解除を示す値のパラメーターを含む TLV [NDIS\_状態\_WDI\_INDICATION\_戻せません](https://msdn.microsoft.com/library/windows/hardware/dn925631)します。

## <a name="tlv-type"></a>TLV 型


0xBC

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型                                                         | 説明                                                                |
|--------------------------------------------------------------|----------------------------------------------------------------------------|
| [**WDI\_MAC\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/dn926071)            | 関連付けの解除の指示に関連付けられているピアの MAC アドレス。 |
| [**WDI\_ASSOC\_状態**](https://msdn.microsoft.com/library/windows/hardware/dn897725) (UINT32) | 関連付けの解除を示す値をトリガーします。                             |

 

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

 

 





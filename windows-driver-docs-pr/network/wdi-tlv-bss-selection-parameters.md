---
title: WDI_TLV_BSS_SELECTION_PARAMETERS
description: WDI_TLV_BSS_SELECTION_PARAMETERS は、BSS 選択範囲のホストによって使用される WDI_BSS_SELECTION_FLAGS を含む TLV です。
ms.assetid: 5EDA0FAC-DF2E-437B-BB4F-F69468CE856E
ms.date: 07/18/2017
keywords:
- WDI_TLV_BSS_SELECTION_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: b8d548a7aae8947970042925aeaf748f0a707425
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536391"
---
# <a name="wditlvbssselectionparameters"></a>WDI\_TLV\_BSS\_選択\_パラメーター


WDI\_TLV\_BSS\_選択\_パラメーターが含む TLV [ **WDI\_BSS\_選択\_フラグ**](https://msdn.microsoft.com/library/windows/hardware/mt297629) BSS 選択のホストによって使用されます。

## <a name="tlv-type"></a>TLV 型


0x10F

## <a name="length"></a>長さ


Uint32 型のサイズをバイト単位で。

## <a name="values"></a>値


| 種類   | 説明                                                                                                     |
|--------|-----------------------------------------------------------------------------------------------------------------|
| UINT32 | [**WDI\_BSS\_選択\_フラグ**](https://msdn.microsoft.com/library/windows/hardware/mt297629) BSS 選択範囲のホストによって使用されます。 |

 

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

 

 





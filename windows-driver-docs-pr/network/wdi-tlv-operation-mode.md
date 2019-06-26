---
title: WDI_TLV_OPERATION_MODE
description: WDI_TLV_OPERATION_MODE では、目的の操作モードを含む TLV です。
ms.assetid: CF5D9148-E50B-4F39-B37C-2495DE9A1488
ms.date: 07/18/2017
keywords:
- WDI_TLV_OPERATION_MODE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 8bb1057b2568575683c7f8f63d84c712d023ed8d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385715"
---
# <a name="wditlvoperationmode"></a>WDI\_TLV\_操作\_モード


WDI\_TLV\_操作\_モードは、目的の操作モードを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x95

## <a name="length"></a>長さ


Uint32 型のサイズをバイト単位で。

## <a name="values"></a>値


| 型   | 説明                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| UINT32 | 定義されている、目的の操作モード[ **WDI\_操作\_モード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ne-dot11wdi-_wdi_operation_mode)します。 |

 

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

 

 





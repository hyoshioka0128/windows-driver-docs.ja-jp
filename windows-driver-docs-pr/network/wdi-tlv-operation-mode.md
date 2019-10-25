---
title: WDI_TLV_OPERATION_MODE
description: WDI_TLV_OPERATION_MODE は、目的の操作モードを含む TLV です。
ms.assetid: CF5D9148-E50B-4F39-B37C-2495DE9A1488
ms.date: 07/18/2017
keywords:
- WDI_TLV_OPERATION_MODE ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 5dc954fce2e1628948829a164a4f6d2af7789ae5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824371"
---
# <a name="wdi_tlv_operation_mode"></a>WDI\_TLV\_操作\_モード


WDI\_TLV\_操作\_モードは、目的の操作モードを含む TLV です。

## <a name="tlv-type"></a>TLV 型


0x95

## <a name="length"></a>長さ


UINT32 のサイズ (バイト単位)。

## <a name="values"></a>値


| タスクバーの検索ボックスに   | 説明                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| UINT32 | [**WDI\_operation\_モード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ne-dot11wdi-_wdi_operation_mode)で定義されている、必要な操作モード。 |

 

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
<td>Wditypes</td>
</tr>
</tbody>
</table>

 

 





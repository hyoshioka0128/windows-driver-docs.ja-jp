---
title: WDI_TLV_ADAPTER_NLO_SCAN_MODE
description: WDI_TLV_ADAPTER_NLO_SCAN_MODE は、スキャンをアクティブモードとパッシブモードのどちらで実行するかを示す TLV です。
ms.assetid: 4294AF4D-587E-4978-9C54-E11D7368FBB8
ms.date: 07/18/2017
keywords:
- WDI_TLV_ADAPTER_NLO_SCAN_MODE ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 8c25e87380433ca39f2dcb2eb851c0c7e66aee92
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842888"
---
# <a name="wdi_tlv_adapter_nlo_scan_mode"></a>WDI\_TLV\_アダプター\_NLO\_スキャン\_モード


WDI\_TLV\_ADAPTER\_NLO\_SCAN\_MODE は、スキャンをアクティブモードとパッシブモードのどちらで実行するかを示す TLV です。

## <a name="tlv-type"></a>TLV 型


0x125

## <a name="length"></a>長さ


UINT32 のサイズ (バイト単位)。

## <a name="values"></a>値


| タスクバーの検索ボックスに   | 説明                                                                                                                     |
|--------|---------------------------------------------------------------------------------------------------------------------------------|
| UINT32 | [**WDI\_SCAN\_スキャン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_scan_type)をアクティブモードとパッシブモードのどちらで実行するかを示す値を指定します。 |

 

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

 

 





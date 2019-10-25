---
title: WDI_TLV_BSS_SELECTION_PARAMETERS
description: WDI_TLV_BSS_SELECTION_PARAMETERS は、ホストが BSS 選択に使用する WDI_BSS_SELECTION_FLAGS を含む TLV です。
ms.assetid: 5EDA0FAC-DF2E-437B-BB4F-F69468CE856E
ms.date: 07/18/2017
keywords:
- WDI_TLV_BSS_SELECTION_PARAMETERS ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 48d03a8c68a97df6c7c5a2a441f0ae197807d465
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844489"
---
# <a name="wdi_tlv_bss_selection_parameters"></a>WDI\_TLV\_BSS\_SELECTION\_PARAMETERS


WDI\_TLV\_BSS\_SELECTION\_PARAMETERS は、ホストが BSS 選択に使用する[**WDI\_BSS\_選択\_フラグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_bss_selection_flags)を含む TLV です。

## <a name="tlv-type"></a>TLV 型


0x10F

## <a name="length"></a>長さ


UINT32 のサイズ (バイト単位)。

## <a name="values"></a>値


| タスクバーの検索ボックスに   | 説明                                                                                                     |
|--------|-----------------------------------------------------------------------------------------------------------------|
| UINT32 | [**WDI\_bss**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_bss_selection_flags)は、bss 選択のためにホストによって使用される\_フラグを\_選択します。 |

 

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

 

 





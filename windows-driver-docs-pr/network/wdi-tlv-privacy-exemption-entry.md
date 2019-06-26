---
title: WDI_TLV_PRIVACY_EXEMPTION_ENTRY
description: WDI_TLV_PRIVACY_EXEMPTION_ENTRY では、プライバシーの除外対象エントリを含む TLV です。
ms.assetid: 086BD366-F54C-4BF4-8544-CC2AB2472EB2
ms.date: 07/18/2017
keywords:
- WDI_TLV_PRIVACY_EXEMPTION_ENTRY ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: a43f519cc1a9babd49bf80a3af2e4a150335cb38
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366513"
---
# <a name="wditlvprivacyexemptionentry"></a>WDI\_TLV\_プライバシー\_除外\_エントリ


WDI\_TLV\_プライバシー\_除外\_エントリはプライバシーの除外対象エントリを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x48

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型                                                                   | 説明                                                 |
|------------------------------------------------------------------------|-------------------------------------------------------------|
| UINT16                                                                 | IEEE EtherType ビッグ エンディアン バイト順を指定します。      |
| [**WDI\_除外\_アクション\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ne-dot11wdi-_wdi_exemption_action_type) | 除外対象のアクションの種類を指定します。                 |
| [**WDI\_除外\_パケット\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_exemption_packet_type) | 除外対象が適用されるパケットの種類を指定します。 |

 

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

 

 





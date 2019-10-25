---
title: WDI_TLV_P2P_CHANNEL_INDICATE_REASON
description: WDI_TLV_P2P_CHANNEL_INDICATE_REASON は、通知を送信する理由を含む TLV です。
ms.assetid: DD746492-82C5-4458-94A2-778F7F0F30B4
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_CHANNEL_INDICATE_REASON ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 45b90ba6ebd7e4353ee3ddb9a35694aefe720e02
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840457"
---
# <a name="wdi_tlv_p2p_channel_indicate_reason"></a>WDI\_TLV\_P2P\_チャネル\_理由を\_示す


WDI\_TLV\_P2P\_チャネル\_は、理由が示された理由を含む TLV であることを\_示します。

## <a name="tlv-type"></a>TLV 型


0x102

## <a name="length"></a>Length


UINT32 のサイズ (バイト単位)。

## <a name="values"></a>値


| 種類   | 説明                                                                                                                                         |
|--------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT32 | 通知を送信する理由。 考えられる理由について\_理由を示すには、 [**WDI\_P2P\_CHANNEL\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_p2p_channel_indicate_reason)を参照してください。 |

 

<a name="requirements"></a>前提条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最低限のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小サーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>ヘッダー</p></td>
<td>Wditypes</td>
</tr>
</tbody>
</table>

 

 





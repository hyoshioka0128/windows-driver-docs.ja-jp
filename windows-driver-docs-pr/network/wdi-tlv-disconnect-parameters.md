---
title: WDI_TLV_DISCONNECT_PARAMETERS
description: WDI_TLV_DISCONNECT_PARAMETERS は、OID_WDI_TASK_DISCONNECT のパラメーターを含む TLV です。
ms.assetid: D0FF83A0-CD3B-47A6-BB08-842927F1D3BC
ms.date: 07/18/2017
keywords:
- WDI_TLV_DISCONNECT_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 975574b9e5630ce733e6db9e668b5785a9472640
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358569"
---
# <a name="wditlvdisconnectparameters"></a>WDI\_TLV\_切断\_パラメーター


WDI\_TLV\_切断\_パラメーターはパラメーターを含む TLV [OID\_WDI\_タスク\_切断](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-disconnect)します。

## <a name="tlv-type"></a>TLV 型


0x36

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型                                              | 説明                                                                                                                                                                         |
|---------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 関連付けを解除するピアの MAC アドレス。                                                                                                                                        |
| UINT16                                            | ホストによってトリガーされる関連付け解除の理由です。 この値は、リトル エンディアン バイト順で提供される、送信の枠の理由コードに適切にコピーする必要があります。 |

 

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

 

 





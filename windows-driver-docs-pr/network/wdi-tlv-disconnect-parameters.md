---
title: WDI_TLV_DISCONNECT_PARAMETERS
description: WDI_TLV_DISCONNECT_PARAMETERS は、OID_WDI_TASK_DISCONNECT のパラメーターを含む TLV です。
ms.assetid: D0FF83A0-CD3B-47A6-BB08-842927F1D3BC
ms.date: 07/18/2017
keywords:
- WDI_TLV_DISCONNECT_PARAMETERS ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: bfd0a2435a3e26708cf95c62efeea279f04a8e3a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834127"
---
# <a name="wdi_tlv_disconnect_parameters"></a>WDI\_TLV\_\_パラメーターの切断


WDI\_TLV\_DISCONNECT\_PARAMETERS は、 [OID\_WDI\_タスク\_切断](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-disconnect)のパラメーターを含む TLV です。

## <a name="tlv-type"></a>TLV 型


0x36

## <a name="length"></a>長さ


含まれているすべての要素のサイズの合計 (バイト単位)。

## <a name="values"></a>値


| タスクバーの検索ボックスに                                              | 説明                                                                                                                                                                         |
|---------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 関連付けを解除するピアの MAC アドレス。                                                                                                                                        |
| UINT16                                            | ホストによってトリガーされる関連付けの理由。 この値は、リトルエンディアンバイト順に記述されており、送信フレームの理由コードに適切にコピーされる必要があります。 |

 

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

 

 





---
title: WDI_TLV_INCOMING_ASSOCIATION_REQUEST_PARAMETERS
description: WDI_TLV_INCOMING_ASSOCIATION_REQUEST_PARAMETERS は、アソシエーション要求パラメーターを含む TLV です。
ms.assetid: DC3439A2-2221-4489-AB38-3752624EA4B2
ms.date: 07/18/2017
keywords:
- WDI_TLV_INCOMING_ASSOCIATION_REQUEST_PARAMETERS ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: a8e49007aa94a430a97ef8fa4d7ffa08dc64cbf2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841749"
---
# <a name="wdi_tlv_incoming_association_request_parameters"></a>WDI\_TLV\_受信\_アソシエーション\_要求\_パラメーター


WDI\_TLV\_受信\_アソシエーション\_要求\_パラメーターは、アソシエーション要求パラメーターを含む TLV です。

## <a name="tlv-type"></a>TLV 型


0x7D

## <a name="length"></a>長さ


含まれているすべての要素のサイズの合計 (バイト単位)。

## <a name="values"></a>値


| タスクバーの検索ボックスに                                              | 説明                                                                                                                   |
|---------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 送信者の MAC アドレス。                                                                                                |
| UINT8                                             | 再関連付け要求であるかどうかを示すビット。 値1は、再関連付け要求であることを示します。 |

 

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

 

 





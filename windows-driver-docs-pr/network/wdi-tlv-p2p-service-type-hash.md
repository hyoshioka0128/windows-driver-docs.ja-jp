---
title: WDI_TLV_P2P_SERVICE_TYPE_HASH
description: WDI_TLV_P2P_SERVICE_TYPE_HASH は、サービスの種類のハッシュを含む TLV です。
ms.assetid: A475C2E3-F558-47EC-9708-87887AE2D8AF
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_SERVICE_TYPE_HASH ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: cd2c6d3ef612cbe57dcced5bd5d06422ea87ea23
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838023"
---
# <a name="wdi_tlv_p2p_service_type_hash"></a>WDI\_TLV\_P2P\_サービス\_型\_HASH


WDI\_TLV\_P2P\_SERVICE\_TYPE\_HASH は、サービスの種類のハッシュを含む TLV です。

この TLV は、Windows 10 バージョン1607、WDI version 1.0.21 で追加された  に**注意**してください。

 

## <a name="tlv-type"></a>TLV 型


0x12A

## <a name="length"></a>長さ


[**WDI\_P2P\_サービス\_名\_ハッシュ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_p2p_service_name_hash)構造のサイズ (バイト単位)。

## <a name="values"></a>値


| タスクバーの検索ボックスに                                                                    | 説明               |
|-------------------------------------------------------------------------|---------------------------|
| [**WDI\_P2P\_サービス\_名前\_ハッシュ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_p2p_service_name_hash) | サービスの種類のハッシュ。 |

 

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

 

 





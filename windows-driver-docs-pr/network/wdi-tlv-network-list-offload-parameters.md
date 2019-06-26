---
title: WDI_TLV_NETWORK_LIST_OFFLOAD_PARAMETERS
description: WDI_TLV_NETWORK_LIST_OFFLOAD_PARAMETERS は、OID_WDI_SET_NETWORK_LIST_OFFLOAD のネットワークの一覧のオフロード (NLO) パラメーターを含む TLV です。
ms.assetid: B8DD3BB6-DB90-4500-9BD5-252230F4BAAD
ms.date: 07/18/2017
keywords:
- WDI_TLV_NETWORK_LIST_OFFLOAD_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 27ee11981d30545dd6b761e78e9e43b7ddc2ac98
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385714"
---
# <a name="wditlvnetworklistoffloadparameters"></a>WDI\_TLV\_ネットワーク\_一覧\_オフロード\_パラメーター


WDI\_TLV\_ネットワーク\_一覧\_オフロード\_パラメーターは、のネットワークの一覧のオフロード (NLO) パラメーターを含む TLV [OID\_WDI\_セット\_ネットワーク\_一覧\_オフロード](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-set-network-list-offload)します。

## <a name="tlv-type"></a>TLV 型


0x59

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                                                    | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                                                  |
|-----------------------------------------------------------------------------------------|--------------------------------|----------|----------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_ネットワーク\_一覧\_オフロード\_構成**](wdi-tlv-network-list-offload-config.md) |                                |          | NLO 構成を指定します。                                                                 |
| [**WDI\_TLV\_SSID\_オフロード**](wdi-tlv-ssid-offload.md)                                 | x                              | x        | 指定の Ssid をオフロードします。 この要素は、存在しない場合は、ファームウェアが NLO スキャンを停止する必要があります。 |

 

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

 

 





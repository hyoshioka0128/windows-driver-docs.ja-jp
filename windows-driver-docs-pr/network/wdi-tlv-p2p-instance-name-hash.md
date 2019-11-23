---
title: WDI_TLV_P2P_INSTANCE_NAME_HASH
description: WDI_TLV_P2P_INSTANCE_NAME_HASH は、"インスタンス名, サービスの種類" のハッシュを含む TLV です。
ms.assetid: A29D0339-93A8-43EB-8C22-DD7A7DC2147C
ms.date: 07/18/2017
keywords:
- Windows Vista 以降のネットワークドライバーの WDI_TLV_P2P_INSTANCE_NAME_HASH
ms.localizationpriority: medium
ms.openlocfilehash: 5d09bd603504b959b4d640a26dc4c29a40488493
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842358"
---
# <a name="wdi_tlv_p2p_instance_name_hash"></a>WDI\_TLV\_P2P\_インスタンス\_名前\_ハッシュ


WDI\_TLV\_P2P\_インスタンス\_名前\_ハッシュは、"インスタンス名, サービスの種類" のハッシュを含む TLV です。

この TLV は、Windows 10 バージョン1607、WDI version 1.0.21 で追加された  に**注意**してください。

 

## <a name="tlv-type"></a>TLV 型


0x12C

## <a name="length"></a>長さ


[**WDI\_P2P\_サービス\_名\_ハッシュ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_p2p_service_name_hash)構造のサイズ (バイト単位)。

## <a name="values"></a>値


| 種類                                                                    | 説明                                |
|-------------------------------------------------------------------------|--------------------------------------------|
| [**WDI\_P2P\_サービス\_名前\_ハッシュ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_p2p_service_name_hash) | "インスタンス名, サービスの種類" のハッシュ。 |

 

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

 

 





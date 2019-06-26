---
title: WDI_TLV_P2P_INSTANCE_NAME_HASH
description: WDI_TLV_P2P_INSTANCE_NAME_HASH はハッシュを含む TLV「インスタンス名、サービスの種類」のです。
ms.assetid: A29D0339-93A8-43EB-8C22-DD7A7DC2147C
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_INSTANCE_NAME_HASH ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: bbda0e3cfc06df2a723306747e2a0990ba7ad345
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374678"
---
# <a name="wditlvp2pinstancenamehash"></a>WDI\_TLV\_P2P\_インスタンス\_名前\_ハッシュ


WDI\_TLV\_P2P\_インスタンス\_名前\_ハッシュのハッシュを含む TLV は、「インスタンス名、サービスの種類」のです。

**注**  この TLV は、Windows 10 バージョン 1607、WDI バージョン 1.0.21 で追加されました。

 

## <a name="tlv-type"></a>TLV 型


0x12C

## <a name="length"></a>長さ


サイズ (バイト単位) で、 [ **WDI\_P2P\_サービス\_名前\_ハッシュ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_p2p_service_name_hash)構造体。

## <a name="values"></a>値


| 型                                                                    | 説明                                |
|-------------------------------------------------------------------------|--------------------------------------------|
| [**WDI\_P2P\_サービス\_名前\_ハッシュ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_p2p_service_name_hash) | 「インスタンス名、サービスの種類」のハッシュです。 |

 

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

 

 





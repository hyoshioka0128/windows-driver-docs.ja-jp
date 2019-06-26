---
title: WDI_TLV_SUPPORTED_GUIDS
description: WDI_TLV_SUPPORTED_GUIDS では、サポートされている NDIS GUID を含む TLV です。
ms.assetid: 957645EE-A6E3-402E-B18B-B2E7C73D6F6B
ms.date: 07/18/2017
keywords:
- WDI_TLV_SUPPORTED_GUIDS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 5935be389a74715f9ecf00275dcf968d247bffa3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386207"
---
# <a name="wditlvsupportedguids"></a>WDI\_TLV\_サポートされている\_GUID


WDI\_TLV\_サポートされている\_GUID は、TLV サポートされている NDIS GUID を格納します。

**注**  この TLV は、Windows 10 バージョン 1607、WDI バージョン 1.0.21 で追加されました。

 

## <a name="tlv-type"></a>TLV 型


0x130

## <a name="length"></a>長さ


サイズ (バイト単位) で、 [NDIS\_GUID](https://docs.microsoft.com/windows-hardware/drivers/network/filling-in-an-ndis-guid-structure)構造体。

## <a name="values"></a>値


| 型       | 説明            |
|------------|------------------------|
| NDIS\_GUID | サポートされている NDIS GUID です。 |

 

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
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_WDI\_取得\_アダプター\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-get-adapter-capabilities)

 

 





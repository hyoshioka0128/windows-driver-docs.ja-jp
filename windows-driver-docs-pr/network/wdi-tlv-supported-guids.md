---
title: WDI_TLV_SUPPORTED_GUIDS
description: WDI_TLV_SUPPORTED_GUIDS では、サポートされている NDIS GUID を含む TLV です。
ms.assetid: 957645EE-A6E3-402E-B18B-B2E7C73D6F6B
ms.date: 07/18/2017
keywords:
- WDI_TLV_SUPPORTED_GUIDS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: cd7980524d3fd6716a3968eeecdabeac6d44293e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552011"
---
# <a name="wditlvsupportedguids"></a>WDI\_TLV\_サポートされている\_GUID


WDI\_TLV\_サポートされている\_GUID は、TLV サポートされている NDIS GUID を格納します。

**注**  この TLV は、Windows 10 バージョン 1607、WDI バージョン 1.0.21 で追加されました。

 

## <a name="tlv-type"></a>TLV 型


0x130

## <a name="length"></a>長さ


サイズ (バイト単位) で、 [NDIS\_GUID](https://msdn.microsoft.com/library/windows/hardware/ff549898)構造体。

## <a name="values"></a>値


| 種類       | 説明            |
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


[OID\_WDI\_取得\_アダプター\_機能](https://msdn.microsoft.com/library/windows/hardware/dn925838)

 

 





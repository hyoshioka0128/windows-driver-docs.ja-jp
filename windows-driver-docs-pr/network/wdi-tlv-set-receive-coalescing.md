---
title: WDI_TLV_SET_RECEIVE_COALESCING
description: WDI_TLV_SET_RECEIVE_COALESCING では、パラメーターを含む受信パケット結合 OID_WDI_SET_RECEIVE_COALESCING の TLV です。
ms.assetid: 7937517E-79E5-4BF6-9C22-79E1D73CA97C
ms.date: 07/18/2017
keywords:
- WDI_TLV_SET_RECEIVE_COALESCING ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: edb89f248316ee36d9b4c4031ad99ff28566d58d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362788"
---
# <a name="wditlvsetreceivecoalescing"></a>WDI\_TLV\_設定\_受信\_COALESCING


WDI\_TLV\_設定\_受信\_COALESCING は受信パケットの結合パラメーターを含む TLV [OID\_WDI\_設定\_受信\_結合](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-set-receive-coalescing)します。

## <a name="tlv-type"></a>TLV 型


0x64

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                                               | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                |
|------------------------------------------------------------------------------------|--------------------------------|----------|--------------------------------------------|
| [**WDI\_TLV\_受信\_COALESCING\_構成**](wdi-tlv-receive-coalescing-config.md) |                                |          | 結合フィルターの構成を指定します。 |
| [**WDI\_TLV\_受信\_フィルター\_フィールド**](wdi-tlv-receive-filter-field.md)           | x                              | x        | 受信フィルター フィールドを指定します。          |

 

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

 

 





---
title: WDI_TLV_CREATE_PORT_MAC_ADDRESS
description: WDI_TLV_CREATE_PORT_MAC_ADDRESS は、OID_WDI_TASK_CREATE_PORT の MAC アドレスを含む TLV です。
ms.assetid: CE2174E2-CFD7-40E7-B8A2-B96DDB6D6AA4
ms.date: 07/18/2017
keywords:
- WDI_TLV_CREATE_PORT_MAC_ADDRESS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 06e99e197ea7d8733bea3db77feb7f65a6948d6c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558944"
---
# <a name="wditlvcreateportmacaddress"></a>WDI\_TLV\_作成\_ポート\_MAC\_アドレス


WDI\_TLV\_作成\_ポート\_MAC\_アドレスは、MAC アドレスを含む TLV [OID\_WDI\_タスク\_作成\_ポート](https://msdn.microsoft.com/library/windows/hardware/dn925949)します。

## <a name="tlv-type"></a>TLV 型


0xD9

## <a name="length"></a>長さ


サイズ (バイト単位) で、 [ **WDI\_MAC\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/dn926071)構造体。

## <a name="values"></a>値


| 種類                                              | 説明                                   |
|---------------------------------------------------|-----------------------------------------------|
| [**WDI\_MAC\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/dn926071) | ポートの作成に使用する MAC アドレスです。 |

 

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

 

 





---
title: WDI_TLV_PM_PROTOCOL_OFFLOAD_GET
description: WDI_TLV_PM_PROTOCOL_OFFLOAD_GET では、プロトコルを含む TLV が OID_WDI_GET_PM_PROTOCOL_OFFLOAD の ID をオフロードします。
ms.assetid: 71BBAA8F-0EE3-4315-AEB1-E9FD394218AD
ms.date: 07/18/2017
keywords:
- WDI_TLV_PM_PROTOCOL_OFFLOAD_GET ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: c2781cc3242716b45bdcd4efe133b8347740527a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362786"
---
# <a name="wditlvpmprotocoloffloadget"></a>WDI\_TLV\_PM\_プロトコル\_オフロード\_取得


WDI\_TLV\_PM\_プロトコル\_オフロード\_GET のプロトコルのオフロード ID を含む TLV [OID\_WDI\_取得\_PM\_プロトコル\_オフロード](https://msdn.microsoft.com/library/windows/hardware/dn925846)します。

## <a name="tlv-type"></a>TLV 型


0xA8

## <a name="length"></a>長さ


Uint32 型のサイズをバイト単位で。

## <a name="values"></a>値


| 型   | 説明                                                                                                                                                                                                                                                                                                 |
|--------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT32 | プロトコルのオフロード ID を指定します これは、オフロードされたプロトコルを識別する OS で提供される値です。 OS では、追加要求を送信します。 または、上にあるドライバーへの要求が完了すると、前に、プロトコル間で一意の値に OS セット ProtocolOffloadId をネットワーク アダプターにオフロードします。 |

 

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

 

 





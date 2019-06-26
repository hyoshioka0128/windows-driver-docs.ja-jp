---
title: WDI_TLV_CREATE_PORT_PARAMETERS
description: WDI_TLV_CREATE_PORT_PARAMETERS は、OID_WDI_TASK_CREATE_PORT のパラメーターを含む TLV です。
ms.assetid: CE0ACE11-5E7A-43E1-BE0B-8BA8F7FF8432
ms.date: 07/18/2017
keywords:
- WDI_TLV_CREATE_PORT_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: b0e86e421ccda2be78889421f41f5aedaff1a0e5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374704"
---
# <a name="wditlvcreateportparameters"></a>WDI\_TLV\_作成\_ポート\_パラメーター


WDI\_TLV\_作成\_ポート\_パラメーターはパラメーターを含む TLV [OID\_WDI\_タスク\_作成\_ポート](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-create-port).

## <a name="tlv-type"></a>TLV 型


0x28

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型   | 説明                                                                                                                                                                             |
|--------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT16 | 操作モードのビットごとの OR 値、ホストが作成されているポートで構成できます。 操作モードがで定義されている[ **WDI\_操作\_モード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ne-dot11wdi-_wdi_operation_mode)します。 |
| UINT32 | NDIS\_ポート\_番号を作成したポートに関連付けられます。 アダプターは、WDI 以外の Oid を処理する必要がある場合を除き、このフィールドに何もする必要はありません。                 |

 

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

 

 





---
title: WDI_TLV_CREATE_PORT_PARAMETERS
description: WDI_TLV_CREATE_PORT_PARAMETERS は、OID_WDI_TASK_CREATE_PORT のパラメーターを含む TLV です。
ms.assetid: CE0ACE11-5E7A-43E1-BE0B-8BA8F7FF8432
ms.date: 07/18/2017
keywords:
- WDI_TLV_CREATE_PORT_PARAMETERS ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 8ffab1a249624d2dfe89b6d2c07601bdf61a6ffa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843383"
---
# <a name="wdi_tlv_create_port_parameters"></a>WDI\_TLV\_ポート\_パラメーターを作成\_


WDI\_TLV\_CREATE\_PORT\_PARAMETERS は、 [OID\_WDI\_タスク\_\_ポートを作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-create-port)するためのパラメーターを含む TLV です。

## <a name="tlv-type"></a>TLV 型


0x28

## <a name="length"></a>長さ


含まれているすべての要素のサイズの合計 (バイト単位)。

## <a name="values"></a>値


| タスクバーの検索ボックスに   | 説明                                                                                                                                                                             |
|--------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT16 | 作成されるポートでホストが構成できる操作モードのビットごとの OR 値。 操作モードは、 [**WDI\_operation\_モード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ne-dot11wdi-_wdi_operation_mode)で定義されています。 |
| UINT32 | 作成されたポートに関連付けられる NDIS\_ポート\_番号。 アダプターが非 WDI Oid を処理する必要がある場合を除き、このフィールドで何もする必要はありません。                 |

 

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

 

 





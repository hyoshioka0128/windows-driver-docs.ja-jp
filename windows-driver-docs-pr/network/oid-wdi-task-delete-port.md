---
title: OID_WDI_TASK_DELETE_PORT
description: OID_WDI_TASK_DELETE_PORT は、IHV コンポーネントが、指定したポートに割り当てられているすべてのリソース (MAC と PHY を含む) を解放することを要求します。
ms.assetid: c84b6cd6-a8e7-4ba7-a9d9-04b2881904c8
ms.date: 07/18/2017
keywords:
- OID_WDI_TASK_DELETE_PORT ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: d6c7e43f7fa897c4b9148e63c692e1d5fe318b17
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387245"
---
# <a name="oidwditaskdeleteport"></a>OID\_WDI\_タスク\_削除\_ポート


OID\_WDI\_タスク\_削除\_ポートは IHV コンポーネントが、指定したポートに割り当てられているすべてのリソース (MAC と PHY を含む) を解放することを要求します。

| オブジェクト  | 中止できます。 | 既定の優先順位 (ホスト ドライバー ポリシー) | 通常の実行時間 (秒) |
|---------|---------------|---------------------------------------|---------------------------------|
| [アダプター] | X            | 6                                     | 1                               |

 

## <a name="task-parameters"></a>タスク パラメーター


| TLV                                                                               | 許可されている複数の TLV インスタンス | 省略可能 | 説明                 |
|-----------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------|
| [**WDI\_TLV\_削除\_ポート\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-delete-port-parameters) |                                |          | ポートのパラメーターが削除されます。 |

 

## <a name="task-completion-indication"></a>タスクの完了を示す値


[NDIS\_状態\_WDI\_INDICATION\_削除\_ポート\_完了](ndis-status-wdi-indication-delete-port-complete.md)

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
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 





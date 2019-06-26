---
title: OID_WDI_TASK_CHANGE_OPERATION_MODE
description: OID_WDI_TASK_CHANGE_OPERATION_MODE は、ポートの操作モードを構成します。
ms.assetid: 84be0658-104d-4336-bc2f-6f2624f33857
ms.date: 07/18/2017
keywords:
- OID_WDI_TASK_CHANGE_OPERATION_MODE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: f31cc86fe32c2a65f85c8b0abe8a3f45feb357e8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386527"
---
# <a name="oidwditaskchangeoperationmode"></a>OID\_WDI\_タスク\_変更\_操作\_モード


OID\_WDI\_タスク\_変更\_操作\_モードは、ポートの操作モードを構成します。

| オブジェクト | 中止できます。 | 既定の優先順位 (ホスト ドライバー ポリシー) | 通常の実行時間 (秒) |
|--------|---------------|---------------------------------------|---------------------------------|
| ポート   | X            | 4                                     | 1                               |

 

## <a name="task-parameters"></a>タスク パラメーター


| TLV                                                              | 許可されている複数の TLV インスタンス | 省略可能 | 説明                 |
|------------------------------------------------------------------|--------------------------------|----------|-----------------------------|
| [**WDI\_TLV\_操作\_モード**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-operation-mode) |                                |          | 目的の操作モード。 |

 

## <a name="task-completion-indication"></a>タスクの完了を示す値


[NDIS\_状態\_WDI\_INDICATION\_変更\_操作\_モード\_完了](ndis-status-wdi-indication-change-operation-mode-complete.md)

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

 

 





---
title: OID_WDI_TASK_CHANGE_OPERATION_MODE
description: OID_WDI_TASK_CHANGE_OPERATION_MODE は、ポートの操作モードを構成します。
ms.assetid: 84be0658-104d-4336-bc2f-6f2624f33857
ms.date: 07/18/2017
keywords:
- OID_WDI_TASK_CHANGE_OPERATION_MODE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 2987e7c326fe7f2b16822292083dbce4964b063a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550812"
---
# <a name="oidwditaskchangeoperationmode"></a>OID\_WDI\_タスク\_変更\_操作\_モード


OID\_WDI\_タスク\_変更\_操作\_モードは、ポートの操作モードを構成します。

| オブジェクト | 中止できます。 | 既定の優先順位 (ホスト ドライバー ポリシー) | 通常の実行時間 (秒) |
|--------|---------------|---------------------------------------|---------------------------------|
| ポート   | X            | 4                                     | 1                               |

 

## <a name="task-parameters"></a>タスク パラメーター


| TLV                                                              | 許可されている複数の TLV インスタンス | 省略可能 | 説明                 |
|------------------------------------------------------------------|--------------------------------|----------|-----------------------------|
| [**WDI\_TLV\_操作\_モード**](https://msdn.microsoft.com/library/windows/hardware/dn897856) |                                |          | 目的の操作モード。 |

 

## <a name="task-completion-indication"></a>タスクの完了を示す値


[NDIS\_状態\_WDI\_INDICATION\_変更\_操作\_モード\_完了](ndis-status-wdi-indication-change-operation-mode-complete.md)要件
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

 

 





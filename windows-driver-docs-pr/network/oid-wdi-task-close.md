---
title: OID_WDI_TASK_CLOSE
description: OID_WDI_TASK_CLOSE は、IHV コンポーネントが、アダプターを閉じることを要求します。 これには、割り込みを無効にして、ハードウェアをシャット ダウンが含まれます。 停止中には、このタスクは IHV によって登録された CloseAdapterHandler ハンドラーを通じて、IHV に渡されます。
ms.assetid: 407d1dfa-18f7-4e22-8f7e-51fd610210af
ms.date: 07/18/2017
keywords:
- OID_WDI_TASK_CLOSE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: a8ce742a66a3bc6fee4d8d1d7e3f95f1e3944ba4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559674"
---
# <a name="oidwditaskclose"></a>OID\_WDI\_タスク\_閉じる


OID\_WDI\_タスク\_閉じる要求 IHV コンポーネントが、アダプターを閉じます。 これには、割り込みを無効にして、ハードウェアをシャット ダウンが含まれます。 停止中には、このタスクは IHV によって登録された CloseAdapterHandler ハンドラーを通じて、IHV に渡されます。

| オブジェクト  | 中止できます。 | 既定の優先順位 (ホスト ドライバー ポリシー) | 通常の実行時間 (秒) |
|---------|---------------|---------------------------------------|---------------------------------|
| アダプタ | X            | 1                                     | 5                               |

 

## <a name="task-parameters"></a>タスク パラメーター


なし
## <a name="task-completion-indication"></a>タスクの完了を示す値


[NDIS\_状態\_WDI\_INDICATION\_閉じる\_完了](ndis-status-wdi-indication-close-complete.md)要件
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

 

 





---
title: OID_WDI_TASK_CLOSE
description: OID_WDI_TASK_CLOSE は、IHV コンポーネントが、アダプターを閉じることを要求します。 これには、割り込みを無効にして、ハードウェアをシャット ダウンが含まれます。 停止中には、このタスクは IHV によって登録された CloseAdapterHandler ハンドラーを通じて、IHV に渡されます。
ms.assetid: 407d1dfa-18f7-4e22-8f7e-51fd610210af
ms.date: 07/18/2017
keywords:
- OID_WDI_TASK_CLOSE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 5e48dd2af651173ba66ad26e030f2d03a18f0066
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348490"
---
# <a name="oidwditaskclose"></a>OID\_WDI\_タスク\_閉じる


OID\_WDI\_タスク\_閉じる要求 IHV コンポーネントが、アダプターを閉じます。 これには、割り込みを無効にして、ハードウェアをシャット ダウンが含まれます。 停止中には、このタスクは IHV によって登録された CloseAdapterHandler ハンドラーを通じて、IHV に渡されます。

| オブジェクト  | 中止できます。 | 既定の優先順位 (ホスト ドライバー ポリシー) | 通常の実行時間 (秒) |
|---------|---------------|---------------------------------------|---------------------------------|
| [アダプター] | X            | 1                                     | 5                               |

 

## <a name="task-parameters"></a>タスク パラメーター


なし
## <a name="task-completion-indication"></a>タスクの完了を示す値


[NDIS\_状態\_WDI\_INDICATION\_閉じる\_完了](ndis-status-wdi-indication-close-complete.md)

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
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 





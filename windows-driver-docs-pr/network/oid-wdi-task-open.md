---
title: OID_WDI_TASK_OPEN
description: OID_WDI_TASK_OPEN 要求、IHV コンポーネントが、アダプターを初期化します。
ms.assetid: f4a77e08-1a1e-4d75-a559-a5cb01d825ee
ms.date: 07/18/2017
keywords:
- OID_WDI_TASK_OPEN ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 23ec5cdaeb22bb08623cd47c9f313ba3830ad434
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59902540"
---
# <a name="oidwditaskopen"></a>OID\_WDI\_タスク\_開く


OID\_WDI\_タスク\_オープン要求 IHV コンポーネントが、アダプターを初期化します。

| オブジェクト  | 中止できます。 | 既定の優先順位 (ホスト ドライバー ポリシー) | 通常の実行時間 (秒) |
|---------|---------------|---------------------------------------|---------------------------------|
| [アダプター] | X            | 1                                     | 2                               |

 

アダプターの初期化には、アダプター、ファームウェアをダウンロードおよび割り込みとその他のハードウェア リソースの設定が含まれます。 初期化中に、このタスクは IHV によって登録された OpenAdapterHandler ハンドラーを使用して、IHV に渡されます。 省電力状態から再開、これに渡される、IHV OID を使用して\_WDI\_タスク\_開きます。

## <a name="task-parameters"></a>タスク パラメーター


なし
## <a name="task-completion-indication"></a>タスクの完了を示す値


[NDIS\_状態\_WDI\_INDICATION\_オープン\_完了](ndis-status-wdi-indication-open-complete.md)

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

 

 





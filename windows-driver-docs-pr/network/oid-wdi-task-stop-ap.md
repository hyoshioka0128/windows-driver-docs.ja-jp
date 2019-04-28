---
title: OID_WDI_TASK_STOP_AP
description: OID_WDI_TASK_STOP_AP は、IHV コンポーネントが指定したポートで接続されているすべてのクライアントを切断し、ビーコンおよびプローブ要求に応答を停止することを要求します。 アジア太平洋の構成と MIB 属性は保持されます。
ms.assetid: b7df1d2f-fed4-4079-8a2d-3f691a52ad52
ms.date: 07/18/2017
keywords:
- OID_WDI_TASK_STOP_AP ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: efae7d2c8c681ab42c1aeaeb02466677a9f67368
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365706"
---
# <a name="oidwditaskstopap"></a>OID\_WDI\_タスク\_停止\_アジア太平洋


OID\_WDI\_タスク\_停止\_AP 要求 IHV コンポーネントは、指定したポートに接続されているすべてのクライアントが切断され、ビーコンおよびプローブ要求に応答を停止します。 アジア太平洋の構成と MIB 属性は保持されます。

| オブジェクト | 中止できます。 | 既定の優先順位 (ホスト ドライバー ポリシー) | 通常の実行時間 (秒) |
|--------|---------------|---------------------------------------|---------------------------------|
| ポート   | X            | 2                                     | 1                               |

 

## <a name="task-parameters"></a>タスク パラメーター


なし
## <a name="task-completion-indication"></a>タスクの完了を示す値


[NDIS\_STATUS\_WDI\_INDICATION\_STOP\_AP\_COMPLETE](ndis-status-wdi-indication-stop-ap-complete.md)

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

 

 





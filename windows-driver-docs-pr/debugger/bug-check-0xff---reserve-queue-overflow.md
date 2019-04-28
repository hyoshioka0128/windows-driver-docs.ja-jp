---
title: バグ チェック 0 xff RESERVE_QUEUE_OVERFLOW
description: RESERVE_QUEUE_OVERFLOW のバグ チェックでは、0x000000FF の値を持ちます。 これは、キューのオーバーフローの原因と、予約のキューに新しい項目を挿入しようとすることを示します。
ms.assetid: d327ea41-c568-49f6-8b37-183533fd6261
keywords:
- バグ チェック 0 xff RESERVE_QUEUE_OVERFLOW
- RESERVE_QUEUE_OVERFLOW
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- RESERVE_QUEUE_OVERFLOW
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 369da6be516d4686dc1d3694b4d7653c2d0e566c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367266"
---
# <a name="bug-check-0xff-reservequeueoverflow"></a>バグ チェック 0xFF:予約\_キュー\_オーバーフロー


予約\_キュー\_オーバーフローのバグ チェックが 0x000000FF の値を持ちます。 これは、キューのオーバーフローの原因と、予約のキューに新しい項目を挿入しようとすることを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="reservequeueoverflow-parameters"></a>予約\_キュー\_オーバーフロー パラメーター


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>予約のキューのアドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>予約のキューのサイズ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>

## <a name="resolution"></a>解決方法 
[ **! 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)バグ チェックに関する情報を表示拡張機能をデバッグおよび根本原因を突き止めるには非常に役に立ちます。
 

 





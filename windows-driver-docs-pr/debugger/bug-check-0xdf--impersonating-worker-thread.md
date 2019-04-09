---
title: Bug Check 0xDF IMPERSONATING_WORKER_THREAD
description: IMPERSONATING_WORKER_THREAD のバグ チェックでは、0x000000DF の値を持ちます。 これは、作業項目が無効にしないこと偽装完了前にことを示します。
ms.assetid: d8a68b5b-3aa8-4d02-8063-420834a47f1b
keywords:
- Bug Check 0xDF IMPERSONATING_WORKER_THREAD
- IMPERSONATING_WORKER_THREAD
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- IMPERSONATING_WORKER_THREAD
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 451058389cdf553c7cd55e3722c36b18f1209ce6
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2019
ms.locfileid: "59238407"
---
# <a name="bug-check-0xdf-impersonatingworkerthread"></a>バグ チェック 0xDF:権限を借用\_ワーカー\_スレッド


偽装\_ワーカー\_スレッドのバグ チェックが 0x000000DF の値を持ちます。 これは、作業項目が無効にしないこと偽装完了前にことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="impersonatingworkerthread-parameters"></a>権限を借用\_ワーカー\_スレッド パラメーター


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
<td align="left"><p>このエラーの原因となったワーカー ルーチン</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>このワーカー ルーチンに渡されるパラメーター</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>作業項目へのポインター</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

ワーカー スレッドが別のプロセスの権限を借用し、返されるようにする前に偽装を無効にできませんでした。

 

 





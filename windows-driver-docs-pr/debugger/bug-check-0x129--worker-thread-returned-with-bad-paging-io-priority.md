---
title: Bug Check 0x129 WORKER_THREAD_RETURNED_WITH_BAD_PAGING_IO_PRIORITY
description: WORKER_THREAD_RETURNED_WITH_BAD_PAGING_IO_PRIORITY のバグ チェックでは、ワーカー スレッドがページング IOPriority が誤って変更されたことを示す 0x00000129 の値を持ちます。
ms.assetid: E662D301-6B4D-4E92-BED3-4BB0731DBFD0
keywords:
- Bug Check 0x129 WORKER_THREAD_RETURNED_WITH_BAD_PAGING_IO_PRIORITY
- WORKER_THREAD_RETURNED_WITH_BAD_PAGING_IO_PRIORITY
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- WORKER_THREAD_RETURNED_WITH_BAD_PAGING_IO_PRIORITY
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b1db5ab3bc6a2f0d25c549d4da433680de593d41
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550625"
---
# <a name="bug-check-0x129-workerthreadreturnedwithbadpagingiopriority"></a>バグ チェック 0x129 の。ワーカー\_スレッド\_から返された\_WITH\_不良\_ページング\_IO\_優先順位


ワーカー\_スレッド\_から返された\_WITH\_不良\_ページング\_IO\_優先度のバグ チェックが 0x00000129 の値を持ちます。 これは、ワーカー スレッド IOPriority のページングが呼び出されるワーカー ルーチンによって誤って変更されたことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="workerthreadreturnedwithbadpagingiopriority-parameters"></a>ワーカー\_スレッド\_から返された\_WITH\_不良\_ページング\_IO\_優先度パラメーター


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
<td align="left">1</td>
<td align="left"><p>ワーカーのルーチンのアドレス</p>
<p>使用して、 <strong><a href="ln--list-nearest-symbols-.md" data-raw-source="[ln (List Nearest Symbols)](ln--list-nearest-symbols-.md)">ln (最も近いシンボルの一覧)</a></strong>問題のあるドライバーを検索するには、このアドレスでコマンド。</p></td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">現在のページング IoPrioirity 値</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">作業項目のパラメーター</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">作業項目のアドレス</td>
</tr>
</tbody>
</table>

 

 

 





---
title: バグチェック 0x4E PFN_LIST_CORRUPT
description: PFN_LIST_CORRUPT バグチェックの値は0x0000004E です。 これは、ページフレーム番号 (PFN) リストが破損していることを示します。
ms.assetid: cf78aecb-80d3-4637-a2b5-a2511999c5e3
keywords:
- バグチェック 0x4E PFN_LIST_CORRUPT
- PFN_LIST_CORRUPT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- PFN_LIST_CORRUPT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ab66501f1bbc3ffb22b280091174cd02b48e1cac
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534625"
---
# <a name="bug-check-0x4e-pfn_list_corrupt"></a>バグチェック 0x4E: PFN \_ LIST が破損して \_ います


PFN LIST の破損した \_ \_ バグチェックには、0x0000004E の値が含まれています。 これは、ページフレーム番号 (PFN) リストが破損していることを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="pfn_list_corrupt-parameters"></a>PFN の破損した \_ パラメーターの一覧表示 \_


*パラメーター 1*は違反の種類を示します。 他のパラメーターの意味は、*パラメーター 1*の値によって異なります。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター 1</th>
<th align="left">パラメータ 2</th>
<th align="left">パラメーター3</th>
<th align="left">パラメーター4</th>
<th align="left">エラーの原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x01</p></td>
<td align="left"><p>破損した<strong>ListHead</strong>の値</p></td>
<td align="left"><p>使用可能なページ数</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>リストの先頭が破損しています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x02</p></td>
<td align="left"><p>削除されるリスト内のエントリ</p></td>
<td align="left"><p>物理的なページ番号の最大値</p></td>
<td align="left"><p>削除されるエントリの参照カウント</p></td>
<td align="left"><p>リストエントリが破損しています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x07</p></td>
<td align="left"><p>ページフレーム番号</p></td>
<td align="left"><p>現在の共有数</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>ドライバーは、ロックされているよりも多くの特定のページをロック解除しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x8D</p></td>
<td align="left"><p>状態が一致しないページフレーム番号</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>ページフリーリストが破損しています。 このエラーコードは、ハードウェアの問題を示している可能性が最も高くなります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x8F</p></td>
<td align="left"><p>新しいページ番号</p></td>
<td align="left"><p>古いページ番号</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>空きページまたはゼロページ listhead が破損しています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x99 (</p></td>
<td align="left"><p>ページフレーム番号</p></td>
<td align="left"><p>現在のページの状態</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>ページテーブルエントリ (PTE) または PFN が破損しています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x9A</p></td>
<td align="left"><p>ページフレーム番号</p></td>
<td align="left"><p>現在のページの状態</p></td>
<td align="left"><p>削除されるエントリの参照カウント</p></td>
<td align="left"><p>ドライバーは、まだ IO 用にロックされているページを解放しようとしました。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

このエラーは、通常、ドライバーによって不適切なメモリ記述子リストが渡されたことが原因で発生します。 たとえば、ドライバーは同じリストで**MmUnlockPages**を2回呼び出した場合があります。

カーネルデバッガーが使用可能な場合は、スタックトレースを確認してください。 [**! analyze**](-analyze.md)デバッグ拡張機能はバグチェックに関する情報を表示し、根本原因を特定するのに役立つ場合があります。その後、 [**k (スタックバックトレースの表示)**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)コマンドのいずれかを入力して、呼び出し履歴を表示します。

 

 





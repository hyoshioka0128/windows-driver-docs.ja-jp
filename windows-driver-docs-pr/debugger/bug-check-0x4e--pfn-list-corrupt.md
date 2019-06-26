---
title: バグ チェック 0x4E PFN_LIST_CORRUPT
description: PFN_LIST_CORRUPT のバグ チェックでは、0x0000004E の値を持ちます。 これは、ページのフレーム数 (PFN) の一覧が破損していることを示します。
ms.assetid: cf78aecb-80d3-4637-a2b5-a2511999c5e3
keywords:
- バグ チェック 0x4E PFN_LIST_CORRUPT
- PFN_LIST_CORRUPT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- PFN_LIST_CORRUPT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7740546338320770e748e887da0e36d9df91fff2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367424"
---
# <a name="bug-check-0x4e-pfnlistcorrupt"></a>バグ チェック 0x4E:PFN\_一覧\_が壊れています


PFN\_一覧\_破損バグ チェックが 0x0000004E の値を持ちます。 これは、ページのフレーム数 (PFN) の一覧が破損していることを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


## <a name="pfnlistcorrupt-parameters"></a>PFN\_一覧\_破損しているパラメーター


*パラメーター 1*違反の種類を示します。 その他のパラメーターの意味は、の値によって異なります。*パラメーター 1*します。

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
<th align="left">3 番目のパラメーター</th>
<th align="left">パラメーター 4</th>
<th align="left">エラーの原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x01</p></td>
<td align="left"><p><strong>ListHead</strong>が破損していた値</p></td>
<td align="left"><p>使用可能なページの数</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>リストの先頭が破損しています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x02</p></td>
<td align="left"><p>削除されるリストのエントリ</p></td>
<td align="left"><p>最大の物理的なページ番号</p></td>
<td align="left"><p>削除されるエントリの参照カウント</p></td>
<td align="left"><p>一覧のエントリが破損しています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x07</p></td>
<td align="left"><p>ページのフレーム数</p></td>
<td align="left"><p>現在の共有の数</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>ドライバーがロックされていない、特定のページ回よりも、ロックされていること。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x8D</p></td>
<td align="left"><p>状態が一貫性のあるページ フレームの数</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>ページ空きリストが壊れています。 このエラー コードのほとんどでは、ハードウェアの問題を示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x8F</p></td>
<td align="left"><p>新しいページ番号</p></td>
<td align="left"><p>古いページの数</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>無料またはゼロ ページ listhead が壊れています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x99</p></td>
<td align="left"><p>ページ フレームの数</p></td>
<td align="left"><p>現在のページの状態</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>ページ テーブル エントリ (PTE) か、PFN が壊れています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x9A</p></td>
<td align="left"><p>ページ フレームの数</p></td>
<td align="left"><p>現在のページの状態</p></td>
<td align="left"><p>削除されるエントリの参照カウント</p></td>
<td align="left"><p>ドライバーは、IO をまだロックされているページを解放しようとしました。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

このエラーは通常、不良メモリ記述子のリストを渡してドライバーで発生します。 たとえば、ドライバーを呼び出したことがある**MmUnlockPages**同じリストに 2 回です。

カーネル デバッガーを使用できる場合は、スタック トレースを調べる: [ **! 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)デバッグ拡張機能を根本原因を突き止めるに役立ち、入力のいずれかのことができますとバグ チェックに関する情報が表示されます、[ **k (Display Stack Backtrace)** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-)呼び出し履歴を表示するコマンド。

 

 





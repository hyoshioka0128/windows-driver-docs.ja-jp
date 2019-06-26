---
title: バグ チェック xc 7 TIMER_OR_DPC_INVALID
description: TIMER_OR_DPC_INVALID のバグ チェックでは、0x000000C7 の値を持ちます。 場合、カーネルのタイマーが発行または遅延プロシージャ呼び出し (DPC) が許可されていないメモリのどこかが見つかりません。
ms.assetid: 25a85b38-c299-4bf8-a7ed-f516adb5fcb1
keywords:
- バグ チェック xc 7 TIMER_OR_DPC_INVALID
- TIMER_OR_DPC_INVALID
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- TIMER_OR_DPC_INVALID
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 38bb1e52ca075e84b628ee7a361f3faf0cd80bb0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367180"
---
# <a name="bug-check-0xc7-timerordpcinvalid"></a>バグ チェック 0xC7:タイマー\_または\_DPC\_が無効です


タイマー\_または\_DPC\_の無効なバグ チェックが 0x000000C7 の値を持ちます。 場合、カーネルのタイマーが発行または遅延プロシージャ呼び出し (DPC) が許可されていないメモリのどこかが見つかりません。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


## <a name="timerordpcinvalid-parameters"></a>タイマー\_または\_DPC\_パラメーターが無効です


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
<td align="left"><p>0x0</p></td>
<td align="left"><p>タイマー オブジェクトのアドレス</p></td>
<td align="left"><p>チェックされているメモリの範囲の開始</p></td>
<td align="left"><p>チェックされているメモリの範囲の終了</p></td>
<td align="left"><p>タイマー オブジェクトには、タイマー オブジェクトは許可されていないメモリ ブロックが記載されています。 .</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1</p></td>
<td align="left"><p>DPC オブジェクトのアドレス</p></td>
<td align="left"><p>チェックされているメモリの範囲の開始</p></td>
<td align="left"><p>チェックされているメモリの範囲の終了</p></td>
<td align="left"><p>DPC オブジェクト DPC オブジェクトは許可されていないメモリ ブロックが見つかりました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2</p></td>
<td align="left"><p>DPC ルーチンのアドレス</p></td>
<td align="left"><p>チェックされているメモリの範囲の開始</p></td>
<td align="left"><p>チェックされているメモリの範囲の終了</p></td>
<td align="left"><p>DPC オブジェクトは許可されていないメモリ ブロックには、DPC ルーチンが見つかりました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3</p></td>
<td align="left"><p>DPC オブジェクトのアドレス</p></td>
<td align="left"><p>プロセッサの数</p></td>
<td align="left"><p>システムのプロセッサの数</p></td>
<td align="left"><p>DPC オブジェクトのプロセッサ数が正しくありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4</p></td>
<td align="left"><p>DPC ルーチンのアドレス</p></td>
<td align="left"><p>スレッドの APC は、カーネルは、DPC ルーチンを呼び出す前に、カウントを無効にします。</p></td>
<td align="left"><p>スレッドの APC DPC ルーチンが呼び出された後のカウントを無効にします。</p></td>
<td align="left"><p>スレッドの APC の無効化の数は、DPC ルーチンの実行中に変更されました。</p>
<p>APC の無効化カウントがデクリメントされますドライバーを呼び出すたびに<strong>KeEnterCriticalRegion</strong>、 <strong>FsRtlEnterFileSystem</strong>、または、ミュー テックスを取得します。</p>
<p>APC の無効化の数には、ドライバーを呼び出すたびがインクリメントされます<strong>KeLeaveCriticalRegion</strong>、 <strong>KeReleaseMutex</strong>、または<strong>FsRtlExitFileSystem</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x5</p></td>
<td align="left"><p>DPC ルーチンのアドレス</p></td>
<td align="left"><p>スレッドの APC は、カーネルは、DPC ルーチンを呼び出す前に、カウントを無効にします。</p></td>
<td align="left"><p>スレッドの APC DPC ルーチンが呼び出された後のカウントを無効にします。</p></td>
<td align="left"><p>スレッドの APC の無効化の数は、タイマー DPC ルーチンの実行中に変更されました。</p>
<p>APC の無効化カウントがデクリメントされますドライバーを呼び出すたびに<strong>KeEnterCriticalRegion</strong>、 <strong>FsRtlEnterFileSystem</strong>、または、ミュー テックスを取得します。</p>
<p>APC の無効化の数には、ドライバーを呼び出すたびがインクリメントされます<strong>KeLeaveCriticalRegion</strong>、 <strong>KeReleaseMutex</strong>、または<strong>FsRtlExitFileSystem</strong>します。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

この条件は通常、ドライバーが存在する場所のメモリを解放する前に、タイマーまたは DPC をキャンセルする失敗によって発生します。

<a name="resolution"></a>解決方法
----------

ドライバー開発者の場合は、このバグ チェックで得られた情報を使用して、コードで、バグを修正します。

システム管理者は、問題が解決しない場合、ドライバーをアンロードする必要があります。

 

 





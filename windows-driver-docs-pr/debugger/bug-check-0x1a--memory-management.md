---
title: バグ チェック 0x1A MEMORY_MANAGEMENT
description: MEMORY_MANAGEMENT のバグ チェックでは、0x0000001A の値を持ちます。 これは、重大なメモリ管理エラーが発生したことを示します。
ms.assetid: 7d3ff54e-e61a-43fa-a378-fb8d32565586
keywords:
- バグ チェック 0x1A MEMORY_MANAGEMENT
- MEMORY_MANAGEMENT
ms.date: 09/12/2018
topic_type:
- apiref
api_name:
- MEMORY_MANAGEMENT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 42817f2cfc7c0973970dc8d2bf42bab2a5862993
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464190"
---
# <a name="bug-check-0x1a-memorymanagement"></a>バグ チェック 0x1A:メモリ\_管理


メモリ\_管理のバグ チェックが 0x0000001A の値を持ちます。 これは、重大なメモリ管理エラーが発生したことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="memorymanagement-parameters"></a>メモリ\_管理パラメーター


パラメーター 1 が; 関心のある唯一のパラメーターこれは、正確な違反を識別します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター 1</th>
<th align="left">エラーの原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>フォークのクローン ブロックの参照カウントが壊れています。 (これでのみ行われます Windows のチェック ビルドします。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x31</p></td>
<td align="left"><p>イメージの再配置の修正をテーブルまたはコード ストリームが破損しています。 おそらくこれが、ハードウェア エラーです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3f</p></td>
<td align="left"><p>CRC エラー インページ操作に失敗しました。 2 番目のパラメーターには、ページファイルのオフセットが含まれています。 3 番目のパラメーターには、ページ CRC 値にはが含まれています。 パラメーター 4 には、予想される CRC 値が含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x403</p></td>
<td align="left"><p>ページのテーブルと PFNs 同期されていません。 これはおそらく、ハードウェア エラー場合に特にパラメーター 3 &amp; 4 ビットは 1 つのみが異なります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x411</p></td>
<td align="left"><p>ページ テーブル エントリ (PTE) が破損しています。 2 番目のパラメーターは、PTE のアドレスです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x777</p></td>
<td align="left"><p>呼び出し元が現在ロックされていないシステム キャッシュのアドレスをロック解除します。 (このアドレスは決してマップされていたか、または 2 回ロック解除中です)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x778</p></td>
<td align="left"><p>システムでは、保存してではなく最後のシステム キャッシュの表示アドレスで使用します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x780</p>
<p>0x781</p></td>
<td align="left"><p>引数のシステム キャッシュのビューをマッピング Pte が破損しています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1000</p></td>
<td align="left"><p>呼び出し元<strong>MmGetSystemAddressForMdl *</strong>非キャッシュとして完全にキャッシュされている物理ページをマップしようとしています。 この操作で競合しているハードウェア変換バッファー エントリを実行して、これは、オペレーティング システムによって拒否されました。 呼び出し元には、要求元の MDL で「エラー発生時のバグ チェック」が指定されているため、システムがなかったが処理するには、このインスタンスでのバグ チェックを発行します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1010</p></td>
<td align="left"><p>呼び出し元が現在ロックされていないページング可能なセクションをロック解除します。 (このセクションではないロックされていたか、または 2 回ロック解除中です)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1233</p></td>
<td align="left"><p>ドライバーは、ロックされていない物理メモリのページをマップしようとしました。 内容またはページの属性は、いつでもでも変更できるため、法的はありません。 これは、呼び出すマッピングを行ったコードのバグです。 2 番目のパラメーターは、ドライバーをマップしようとしました。 物理ページのページのフレーム数です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1234</p></td>
<td align="left"><p>呼び出し元は存在しないページング可能なセクションをロックしようとしました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1235</p></td>
<td align="left"><p>呼び出し元が無効なマッピングで、MDL を保護しようとしています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1236</p></td>
<td align="left"><p>呼び出し元は、ロックされていない (または無効な) 物理ページを含む、MDL を指定します。 2 番目のパラメーターには、MDL へのポインターが含まれています。 3 番目のパラメーターには、無効な PFN へのポインターが含まれています。 パラメーター 4 には、無効な PFN 値が含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3451</p></td>
<td align="left"><p>スワップ アウトされている、カーネル スレッド スタックの Pte が破損しています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4477</p></td>
<td align="left"><p>ドライバーは、システム プロセスのユーザー領域で、未割り当てのアドレスに書き込もうとしました。 2 番目のパラメーターには、書き込みの試行のアドレスが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x5003</p></td>
<td align="left"><p>作業セットのフリー リストが壊れています。 おそらくこれが、ハードウェア エラーです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x5100</p></td>
<td align="left"><p>アロケーション ビットマップが壊れています。 Memory manager では、既に使用されている仮想アドレスを上書きしようとしています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x5200</p></td>
<td align="left"><p>空きプール SLIST 上のページが破損しています。 ドライバー、または前のページからオーバーラン無料書き込み後にバグによって引き起こされることができます。 2 番目のパラメーターには、空きプールのブロックのアドレスが含まれています。 パラメーター 4 には、そのアドレスで予測された値が含まれています。 3 番目のパラメーターには、検出された実際の値が含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x8884</p></td>
<td align="left"><p>(Windows の 7 のみ)。 同一のページ優先順位の値を持つことを予定していたスタンバイ リスト上の 2 つのページには、同一のページ優先順位の値を実際は必要はありませんも。 異なる値は、パラメーター 4 にキャプチャされます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x8888</p>
<p>0x8889</p></td>
<td align="left"><p>内部メモリの管理構造が破損しています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x888A</p></td>
<td align="left"><p>(PTE 可能性がありますまたは PFN) の内部メモリの管理構造が破損しています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x41283</p></td>
<td align="left"><p>PTE でエンコードされたワーキング セットのインデックスが壊れています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x41284</p></td>
<td align="left"><p>PTE または作業用セットの一覧が壊れています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x41286</p></td>
<td align="left"><p>呼び出し元が、無効なプールのアドレスを解放しようとしています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x41785</p></td>
<td align="left"><p>作業用セットの一覧が壊れています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x41287</p></td>
<td align="left"><p>作業セットの同期を保持しているときに、無効なページ フォールトが発生しました。 2 番目のパラメーターには、参照先の仮想アドレスが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x41790</p></td>
<td align="left"><p>ページ テーブル ページが破損しています。 Windows の 64 ビット バージョンでは、2 番目のパラメーターには、破損しているページ テーブル ページの PFN のアドレスが含まれています。 Windows の 32 ビット バージョンでは、2 番目のパラメーターの使用の Pte 数へのポインターを格納して、3 番目のパラメーターに使用される Pte の数が含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x41792</p></td>
<td align="left"><p>破損した PTE が検出されました。 2 番目のパラメーターには、PTE のアドレスが含まれています。 パラメーター 3/4 では、PTE の低/高部分が含まれます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x41793</p></td>
<td align="left"><p> ページ テーブル ページが破損しています。 2 番目のパラメーターには、最後に処理された PTE へのポインターが含まれています。 3 番目のパラメーターには、0 以外の Pte 検出の数が含まれています。 パラメーター 4 には、予想されるページ テーブル内の 0 以外の Pte 数が含まれています。</p><p>このメモリ パラメーターは非推奨し、Windows 10 バージョン 1803 後は使用できなくします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x61940</p></td>
<td align="left"><p>PDE が予期せず無効にします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x61941</p></td>
<td align="left"><p>ページングの階層が壊れています。 2 番目のパラメーターは、エラーの原因となった仮想アドレスへのポインターです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x61946</p></td>
<td align="left"><p>作成される MDL は不備があります。 これはほぼ常に、ドライバーの呼び出し元を意味<strong>MmProbeAndLockPages</strong>障害があります。 通常、ドライバーは、求めるページング読み取りを処理するときに、書き込み MDL を作成しています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x61949</p></td>
<td align="left"><p>IoPageFrameNode が null です。 2 番目のパラメーターは、PageFrameIndex です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x03030303</p></td>
<td align="left"><p>ブート ローダーが壊れています。 (この値は、Intel Itanium のコンピューターにのみ適用されます)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x03030308</p></td>
<td align="left"><p>削除 (または truncate) の範囲で使用されて、ローダーに安全に削除することはできませんので、システムが停止コードを発行する必要があります。  2 番目のパラメーターは、HighestPhysicalPage です。</p></td>
</tr>
</tbody>
</table>


<a name="resolution"></a>解決方法
----------

[ **! 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)バグ チェックに関する情報を表示拡張機能をデバッグおよび根本原因を突き止めるには非常に役に立ちます。 実行している、 [ **Windows Memory Diagnostic** ](https://social.technet.microsoft.com/wiki/contents/articles/29343.windows-10-technical-preview-running-windows-memory-diagnostics-tool.aspx)ツールは、任意の種類の物理メモリ モジュールに影響を与える問題を除外するにも役立つ可能性があります。
 

 

 





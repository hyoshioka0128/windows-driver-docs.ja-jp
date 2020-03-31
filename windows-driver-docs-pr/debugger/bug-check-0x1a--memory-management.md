---
title: 'バグ チェック 0x1A: MEMORY_MANAGEMENT'
description: MEMORY_MANAGEMENT バグ チェックの値は、0x0000001A です。 これは、重大なメモリ管理エラーが発生したことを示します。
ms.assetid: 7d3ff54e-e61a-43fa-a378-fb8d32565586
keywords:
- 'バグ チェック 0x1A: MEMORY_MANAGEMENT'
- MEMORY_MANAGEMENT
ms.date: 02/04/2020
topic_type:
- apiref
api_name:
- MEMORY_MANAGEMENT
api_type:
- NA
ms.localizationpriority: high
ms.openlocfilehash: aa8f9ccbbf1c8f8e979072dea177ef3202cb8ef3
ms.sourcegitcommit: 063827f0253d6d14cd928b4e4ebf5e3b9c30dc6f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/27/2020
ms.locfileid: "80327571"
---
# <a name="bug-check-0x1a-memory_management"></a>バグ チェック 0x1A:MEMORY\_MANAGEMENT

MEMORY\_MANAGEMENT バグ チェックの値は、0x0000001A です。 これは、重大なメモリ管理エラーが発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルー スクリーン エラー コードが表示される場合は、「[ブルー スクリーン エラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。

## <a name="memory_management-parameters"></a>MEMORY\_MANAGEMENT のパラメーター

パラメーター 1 は、正確な違反を識別します。

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
<td align="left"><p>フォーク クローン ブロックの参照カウントが破損しています。 これは、Windows のチェック ビルドでのみ発生します。 チェック ビルドは、Windows 10 バージョン 1803 以前の古いバージョンの Windows で使用することができました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x31</p></td>
<td align="left"><p>イメージの再配置修正テーブルまたはコード ストリームが破損しました。 これは、ハードウェア エラーの可能性があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3f</p></td>
<td align="left"><p>インページ操作が CRC エラーで失敗しました。 パラメーター 2 には、ページ ファイルのオフセットが含まれます。 パラメーター 3 には、ページの CRC 値が含まれます。 パラメーター 4 には、予想される CRC 値が含まれます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x403</p></td>
<td align="left"><p>ページ テーブルと PFN が同期されていません。 これは、特にパラメーター 3 および 4 の違いが 1 ビットだけの場合、ハードウェア エラーの可能性があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x404</p></td>
<td align="left"><p>システム ページを削除するプロセスで、ページ フレーム番号 (PFN) と現在のページ テーブル エントリ (PTE) ポインターの間で矛盾が発生しました。 パラメーター 2 は予想される PTE です。 パラメーター 3 は PTE の内容で、パラメーター 4 は PFN の PTE です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x411</p></td>
<td align="left"><p>ページ テーブル エントリ (PTE) が破損しました。 パラメーター 2 は、PTE のアドレスです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x777</p></td>
<td align="left"><p>呼び出し元が、現在ロックされていないシステム キャッシュ アドレスのロックを解除中です (このアドレスは、マップされていないか、2 回ロック解除されようとしています)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x778</p></td>
<td align="left"><p>システムは、最新のシステム キャッシュ ビュー アドレスを保持するのではなく使用しています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x780</p>
<p>0x781</p></td>
<td align="left"><p>引数システム キャッシュ ビューをマッピングする PTE が破損しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1000</p></td>
<td align="left"><p><strong>MmGetSystemAddressForMdl*</strong> 呼び出し元が、完全にキャッシュされた物理ページを非キャッシュとしてマップしようとしました。 このアクションにより、ハードウェア変換バッファー エントリの競合が発生するため、アクションはオペレーティング システムによって拒否されました。 呼び出し元が、要求している MDL で "失敗時のバグ チェック" を指定したため、システムはこのインスタンスでバグ チェックを発行する以外に選択肢がありませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1010</p></td>
<td align="left"><p>呼び出し元が、現在ロックされていないページング可能なセクションのロックを解除中です (このセクションは、ロックされていないか、2 回ロック解除されようとしています)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1233</p></td>
<td align="left"><p>ドライバーが、ロックされていない物理メモリ ページをマップしようとしました。 ページのコンテンツまたは属性はいつでも変更できるため、これは無効です。 これは、マッピング呼び出しを行ったコードのバグです。 パラメーター 2 は、ドライバーがマップしようとした物理ページのページ フレーム番号です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1234</p></td>
<td align="left"><p>呼び出し元が、存在しないページング可能セクションをロックしようとしています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1235</p></td>
<td align="left"><p>呼び出し元が、無効なマッピングで MDL を保護しようとしています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1236</p></td>
<td align="left"><p>呼び出し元が、ロックされていない (または無効な) 物理ページを含む MDL を指定しました。 パラメーター 2 には、MDL へのポインターが含まれます。 パラメーター 3 には、無効な PFN へのポインターが含まれます。 パラメーター 4 には、無効な PFN 値が含まれます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1240</p></td>
<td align="left"><p>呼び出し元が、常駐しない仮想アドレス範囲に対して MDL をビルドするのは無効です。 パラメーター 2 はメモリ記述子リスト (MDL) で、パラメーター 3 は PTE ポインターです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1241</p></td>
<td align="left"><p>MDL の仮想アドレスが、MDL をビルドする呼び出しの途中で予期せず非同期でマップ解除されました。 パラメーター 2 は MDL で、パラメーター 3 は PTE ポインターです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3300</p></td>
<td align="left"><p>書き込みを実行するプロセスで、参照された仮想アドレスが誤って書き込み時コピーとしてマークされています。 パラメーター 2 は FaultingAddress です。  パラメーター 3 は PTE の内容です。 パラメーター 4 は、仮想アドレス空間の種類を示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3451</p></td>
<td align="left"><p>スワップ アウトされたカーネル スレッド スタックの PTE が破損しています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3453</p></td>
<td align="left"><p>終了したプロセスのすべてのページ テーブル ページが、未処理の参照のために削除できませんでした。  通常、これは、プロセスのページ テーブル構造が破損していることを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3470</p></td>
<td align="left"><p>空きリスト上のキャッシュされたカーネル スタックが破損しました。このメモリ破損は、呼び出し元スタックが対象または原因である可能性がある重大な問題を示します。 パラメーター 2 は仮想アドレス (VA) で、パラメーター 3 は VA Cookie です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4477</p></td>
<td align="left"><p>ドライバーが、システム プロセスのユーザー空間にある未割り当てのアドレスに書き込もうとしました。 パラメーター 2 には、試行された書き込みのアドレスが含まれます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x5003</p></td>
<td align="left"><p>ワーキング セットの空きリストが破損しています。 これは、ハードウェア エラーの可能性があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x5100</p></td>
<td align="left"><p>割り当てビットマップが破損しています。 メモリ マネージャーが、既に使用されている仮想アドレスに上書きしようとしています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x5200</p></td>
<td align="left"><p>空きプール SLIST のページが破損しました。 これは、ドライバーの解放後書き込みバグ、または前のページからのオーバーランの結果である可能性があります。 パラメーター 2 には、空きプール ブロックのアドレスが含まれます。 パラメーター 4 には、そのアドレスにあることが予期されていた値が含まれます。 パラメーター 3 には、検出された実際の値が含まれます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x5305</p></td>
<td align="left"><p>呼び出し元が、無効なプール アドレス (パラメーター 2) を指定して解放しようとしています。 パラメーター 2 は評価される仮想アドレス (VA) で、パラメーター 3 は領域のサイズです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x6001</p></td>
<td align="left"><p>メモリ ストア コンポーネントのプライベート メモリの範囲が破損しているため、アクセスできなくなりました。 パラメーター 2 は、返された状態です。  パラメーター 3 は、ストアのプライベート メモリの範囲内にある仮想アドレスです。 パラメーター 4 は MemoryDescriptorList です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x8884</p><p>0x8885</p><p>0x8886</p><p>0x8887</p></td>
<td align="left"><p>(Windows 7 以降)。 ページ優先順位の値が同じであると想定されていたスタンバイ リスト上の 2 つのページが、実際には、同じページ優先順位値ではありません。 異なる値は、パラメーター 4 にキャプチャされます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x8888</p><p>0x8889</p></td>
<td align="left"><p>内部のメモリ管理構造が破損しています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x888A</p></td>
<td align="left"><p>内部のメモリ管理構造 (おそらく PTE または PFN) が破損しています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x9696</p></td>
<td align="left"><p>PFN (パラメーター 2) が、最上位レベルのプロセスに接続されなくなった、破損したリンケージで検出されました。  これは、PFN 構造の破損を示しています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x15000</p></td>
<td align="left"><p>呼び出し元が、不正なアドレスを指定しているか、不正なプロセス コンテキストでこのルーチンを呼び出しています。  このエラーのために検出できない範囲は安全ではないため、どちらも無効です。 パラメーター 2 は、評価される仮想アドレス (VA) です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x15001</p></td>
<td align="left"><p>以前に保護されていたメモリのセキュリティを解除するプロセスでエラーが発生しました。  これは、呼び出し元が不正なプロセス コンテキストで MmUnsecureVirtualMemory を誤って呼び出した場合に発生する可能性があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x41201</p></td>
<td align="left"><p>仮想アドレスを照会するプロセスで、ページ フレーム番号 (PFN) と現在のページ テーブル エントリ (PTE) ポインターの間で矛盾が発生しました。 パラメーター 2 は、対応する PTE です。 パラメーター 3 は PTE の内容で、パラメーター 4 は仮想アドレス記述子です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x41202</p></td>
<td align="left"><p>0 以外の PTE のページ保護を決定するプロセスで、PTE が破損していると判断されました。  パラメーター 2 は PTE ポインター、パラメーター 3 は PTE の内容、パラメーター 4 は仮想アドレス記述子 (VAD) です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x41283</p></td>
<td align="left"><p>PTE でエンコードされたワーキング セット インデックスが破損しています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x41284</p></td>
<td align="left"><p>PTE またはワーキング セット リストが破損しています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x41286</p></td>
<td align="left"><p>呼び出し元が無効なプール アドレスを解放しようとしています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x41785</p></td>
<td align="left"><p>ワーキング セット リストが破損しています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x41287</p></td>
<td align="left"><p>ワーキング セットの同期を保持しているときに、無効なページ フォールトが発生しました。 パラメーター 2 には、参照される仮想アドレスが含まれます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x41790</p></td>
<td align="left"><p>ページ テーブル ページが破損しています。 64 ビット バージョンの Windows では、パラメーター 2 には、破損したページ テーブル ページの PFN のアドレスが含まれます。 32 ビット バージョンの Windows では、パラメーター 2 には、使用済み PTE の数へのポインターが含まれ、パラメーター 3 には、使用済み PTE の数が含まれます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x41792</p></td>
<td align="left"><p>破損した PTE が検出されました。 パラメーター 2 には、PTE のアドレスが含まれます。 パラメーター 3 および 4 には、PTE の低および高部分が含まれます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x41793</p></td>
<td align="left"><p> ページ テーブル ページが破損しています。 パラメーター 2 には、最後に処理された PTE へのポインターが含まれます。 パラメーター 3 には、見つかった 0 以外の PTE の数が含まれます。 パラメーター 4 には、ページ テーブル内にある 0 以外の PTE の予想される数が含まれます。</p><p>このメモリ パラメーターは廃止され、Windows 10 バージョン 1803 以降では使用できなくなりました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x61940</p></td>
<td align="left"><p>PDE が予期せず無効になりました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x61941</p></td>
<td align="left"><p>ページング階層が破損しています。 パラメーター 2 は、障害の原因となった仮想アドレスへのポインターです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x61946</p></td>
<td align="left"><p>作成中の MDL に欠陥があります。 ほとんどの場合、これは、<strong>MmProbeAndLockPages</strong> を呼び出しているドライバーに問題があることを意味します。 通常、ドライバーが、ページング読み取りの処理を要求されているときに、書き込み MDL を作成しようとしています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x61948</p></td>
<td align="left"><p>I/O スペース領域の参照カウントをデクリメントするプロセスで、そのアカウンティング ノードが見つかりませんでした。  通常、これは、引数範囲がロックされていないか、既にロック解除されていることを意味します。  パラメーター 2 は、ベース I/O フレームです。 パラメーター 3 は領域内のページ数で、パラメーター 4 は、ノードが見つからなかった特定の I/O フレームです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x61949</p></td>
<td align="left"><p>IoPageFrameNode が null です。 パラメーター 2 は PageFrameIndex です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x6194A</p></td>
<td align="left"><p>マップ解除中の I/O 領域の物理ページで参照カウントをデクリメントするときに、エラーが発生しました。 現在参照されていないエントリが逆参照されています。  パラメーター 2 および 3 は、呼び出し元のマップ解除中の I/O 領域の範囲を示し、パラメーター 4 は、参照されることが予想されるが参照されていない I/O 領域の物理ページです。 </p></td>
</tr>
<tr class="even">
<td align="left"><p>0x03030303</p></td>
<td align="left"><p>ブートローダーが破損しています (この値は、Intel Itanium マシンにのみ適用されます)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x03030308</p></td>
<td align="left"><p>削除する (または切り捨てる) 範囲がローダーによって使用されているため、安全に削除できません。このため、システムは停止コードを発行する必要があります。  パラメーター 2 は HighestPhysicalPage です。</p></td>
</tr>
</tbody>
</table>

<a name="resolution"></a>解決方法
----------

[ **!analyze**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze) デバッグ拡張機能は、バグ チェックに関する情報を表示し、根本原因の特定に役立ちます。 

Windows メモリ診断ツールを実行すると、物理メモリ モジュールに影響するあらゆる種類の問題を排除するためにも役立ちます。

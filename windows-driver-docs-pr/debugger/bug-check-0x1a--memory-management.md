---
title: バグチェック 0x1A MEMORY_MANAGEMENT
description: MEMORY_MANAGEMENT バグチェックの値は0x0000001A です。 これは、重大なメモリ管理エラーが発生したことを示します。
ms.assetid: 7d3ff54e-e61a-43fa-a378-fb8d32565586
keywords:
- バグチェック 0x1A MEMORY_MANAGEMENT
- MEMORY_MANAGEMENT
ms.date: 06/29/2019
topic_type:
- apiref
api_name:
- MEMORY_MANAGEMENT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 37a621a1f25f0581ec8bd5da84381209026d77f1
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209320"
---
# <a name="bug-check-0x1a-memory_management"></a>バグチェック 0x1A: メモリ\_管理


メモリ\_管理のバグチェックには、値0x0000001A があります。 これは、重大なメモリ管理エラーが発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="memory_management-parameters"></a>メモリ\_管理パラメーター

パラメーター1は正確な違反を識別します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター1</th>
<th align="left">エラーの原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>フォーク複製ブロックの参照カウントが破損しています。 これは、Windows のチェックされたビルドでのみ発生します。 チェックを行ったビルドは、Windows 10 バージョン1803より前の古いバージョンの Windows で使用できました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x31</p></td>
<td align="left"><p>イメージ再配置の修正テーブルまたはコードストリームが破損しています。 ハードウェアエラーの場合もあります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3f</p></td>
<td align="left"><p>Inpage 操作が CRC エラーで失敗しました。 パラメーター2にはページファイルのオフセットが含まれます。 パラメーター3には、ページの CRC 値が含まれます。 パラメーター4には、予期される CRC 値が含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x403</p></td>
<td align="left"><p>ページテーブルと PFNs が同期されていません。 これは、特に、パラメーター 3 & 4 が1ビットのみで異なる場合に、ハードウェアエラーになります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x404</p></td>
<td align="left"><p>システムページを削除するプロセスで、ページフレーム番号 (PFN) と現在のページテーブルエントリ (PTE) ポインターが矛盾していました。 パラメーター2は予想される PTE です。 パラメーター3は PTE の内容であり、パラメーター4は PFN の PTE です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x411</p></td>
<td align="left"><p>ページテーブルエントリ (PTE) が破損しています。 パラメーター2は、PTE のアドレスです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x777</p></td>
<td align="left"><p>呼び出し元は、現在ロックされていないシステムキャッシュアドレスのロックを解除しています。 (このアドレスは、マップされていないか、または2回ロック解除されています。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x778</p></td>
<td align="left"><p>システムは、最新のシステムキャッシュビューアドレスを保持するのではなく、そのアドレスを使用しています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x780</p>
<p>0x781</p></td>
<td align="left"><p>引数システムキャッシュビューをマッピングする Pte が破損しています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1000</p></td>
<td align="left"><p><strong>MmGetSystemAddressForMdl *</strong>の呼び出し元が、完全にキャッシュされた物理ページを非キャッシュとしてマップしようとしました。 この操作により、競合するハードウェア変換バッファーの入力が発生し、オペレーティングシステムによって拒否されました。 要求元が要求する MDL に "バグチェックが失敗しました" が指定されているため、このインスタンスでバグチェックを発行するための選択肢はありませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1010</p></td>
<td align="left"><p>呼び出し元は、現在ロックされていないページング可能なセクションのロックを解除しています。 (このセクションは、ロックされていないか、2回ロック解除されています。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1233</p></td>
<td align="left"><p>ドライバーが、ロックされていない物理メモリページをマップしようとしました。 これは、ページのコンテンツや属性がいつでも変更される可能性があるため、無効です。 これは、マッピング呼び出しを行ったコードのバグです。 パラメーター2は、ドライバーがマップしようとした物理ページのページフレーム番号です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1234</p></td>
<td align="left"><p>呼び出し元が、存在しないページング可能なセクションをロックしようとしています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1235</p></td>
<td align="left"><p>呼び出し元が、無効なマッピングで MDL を保護しようとしています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1236</p></td>
<td align="left"><p>呼び出し元が、ロックが解除された (または無効な) 物理ページを含む MDL を指定しました。 パラメーター2には、MDL へのポインターが含まれています。 パラメーター3に無効な PFN へのポインターが含まれています。 パラメーター4に無効な PFN 値が含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3300</p></td>
<td align="left"><p>書き込みを実行しているときに、参照先の仮想アドレスが誤って copy on write としてマークされています。 パラメーター2は FaultingAddress です。  パラメーター3は、PTE の内容です。 パラメーター4は、仮想アドレス空間の種類を示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3451</p></td>
<td align="left"><p>スワップアウトされたカーネルスレッドスタックの Pte が破損しています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3453</p></td>
<td align="left"><p>未完了の参照により、終了したプロセスのすべてのページテーブルページを削除できませんでした。  これは通常、プロセスのページテーブル構造が破損していることを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x447 7</p></td>
<td align="left"><p>ドライバーがシステムプロセスのユーザー領域で未割り当てのアドレスに書き込みを試みました。 パラメーター2には、書き込みを試行したアドレスが含まれます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x5003</p></td>
<td align="left"><p>ワーキングセットのフリーリストが破損しています。 ハードウェアエラーの場合もあります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x5100</p></td>
<td align="left"><p>割り当てビットマップが破損しています。 メモリマネージャーは、既に使用されている仮想アドレスを上書きしようとしています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x5200</p></td>
<td align="left"><p>空きプールのページのページが破損しています。 これは、ドライバーの書き込み後のバグ、または前のページからのオーバーランの結果である可能性があります。 パラメーター2には、空きプールブロックのアドレスが含まれています。 パラメーター4には、そのアドレスにあると予期された値が含まれています。 パラメーター3には、検出された実際の値が含まれます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x6001</p></td>
<td align="left"><p>メモリストアコンポーネントのプライベートメモリの範囲が破損しているため、アクセスできなくなりました。 パラメーター2は返された状態です。  パラメーター3は、ストアのプライベートメモリ範囲内の仮想アドレスです。 パラメーター4は、Memory記述子の一覧です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x888 4</p></td>
<td align="left"><p>(Windows 7 のみ)。 同じページの優先順位の値を持つことが想定されていたスタンバイリストの2つのページには、同じページ優先度値が設定されていません。 パラメーター4では、異なる値がキャプチャされます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x888 8</p>
<p>0x888 9</p></td>
<td align="left"><p>内部メモリ管理構造が破損しています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0X888 a</p></td>
<td align="left"><p>内部メモリ管理構造 (多くの場合、PTE または PFN) が破損しています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x9696</p></td>
<td align="left"><p>PFN (パラメーター 2) が見つかりましたが、破損したリンケージが最上位レベルのプロセスに接続されていません。  これは、PFN 構造体が破損していることを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x15001</p></td>
<td align="left"><p>以前に保護されていたメモリのセキュリティを解除する処理で、エラーが発生しました。  これは、呼び出し元が間違ったプロセスコンテキストで MmUnsecureVirtualMemory を誤って呼び出した場合に発生する可能性があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x41201</p></td>
<td align="left"><p>仮想アドレスを照会するプロセスで、ページフレーム番号 (PFN) と現在のページテーブルエントリ (PTE) ポインターの間に矛盾がありました。 パラメーター2は対応する PTE です。 パラメーター3は、PTE の内容であり、パラメーター4は仮想アドレス記述子です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x41283</p></td>
<td align="left"><p>PTE にエンコードされたワーキングセットインデックスが破損しています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x41284</p></td>
<td align="left"><p>PTE またはワーキングセットリストが破損しています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x41286</p></td>
<td align="left"><p>呼び出し元が、無効なプールアドレスを解放しようとしています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x41785</p></td>
<td align="left"><p>ワーキングセットリストが破損しています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x41287</p></td>
<td align="left"><p>ワーキングセット同期を保持しているときに、無効なページフォールトが発生しました。 パラメーター2には、参照先の仮想アドレスが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x41790</p></td>
<td align="left"><p>ページテーブルページが破損しています。 Windows の64ビットバージョンでは、パラメーター2に、破損したページテーブルページの PFN のアドレスが含まれています。 Windows の32ビットバージョンでは、パラメーター2に、使用されている Pte の数へのポインターが含まれています。また、パラメーター3には、使用されている Pte の数が含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x41792</p></td>
<td align="left"><p>破損した PTE が検出されました。 パラメーター2には、PTE のアドレスが含まれます。 パラメーター3/4 には、PTE の低/高部分が含まれます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x41793</p></td>
<td align="left"><p> ページテーブルページが破損しています。 パラメーター2には、最後に処理された PTE へのポインターが含まれています。 パラメーター3に、見つかった0以外の Pte の数が含まれています。 パラメーター4には、ページテーブルで想定される0以外の Pte の数が含まれます。</p><p>このメモリパラメーターは非推奨とされており、Windows 10 バージョン1803以降は使用できなくなりました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x61940</p></td>
<td align="left"><p>PDE が予期せず無効になりました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x61941</p></td>
<td align="left"><p>ページング階層が破損しています。 パラメーター2は、エラーの原因となった仮想アドレスへのポインターです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x61946</p></td>
<td align="left"><p>作成されている MDL に欠陥があります。 これは、ほとんどの場合、 <strong>MmProbeAndLockPages</strong>を呼び出すドライバーが障害時であることを意味します。 通常、ドライバーは、ページングの読み取りを処理するように要求されたときに、書き込み MDL を作成しようとしています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x61948</p></td>
<td align="left"><p>I/o スペース領域の参照カウントをデクリメントするプロセスで、そのアカウンティングノードが見つかりませんでした。  通常、これは、引数の範囲がロックされていないか、既にロックが解除されていることを意味します。  パラメーター2は、ベース i/o フレームです。 パラメーター3は、領域内のページ数を示します。パラメーター4は、ノードが見つからなかった特定の i/o フレームです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x61949</p></td>
<td align="left"><p>IoPageFrameNode が null です。 パラメーター2は PageFrameIndex です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x6194A</p></td>
<td align="left"><p>マップ解除されている i/o スペース物理ページの参照カウントをデクリメント中にエラーが発生しました。 現在参照されていないエントリを逆参照しています。  パラメーター2と3は、マップ解除されている呼び出し元の i/o 領域の範囲を示します。パラメーター4は、参照する必要があるが、ではない i/o 領域の物理ページです。 </p></td>
</tr>
<tr class="even">
<td align="left"><p>0x03030303</p></td>
<td align="left"><p>ブートローダーが破損しています。 (この値は、Intel Itanium コンピューターにのみ適用されます。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x03030308</p></td>
<td align="left"><p>削除 (または切り捨て) する範囲はローダーによって使用されているため、安全に削除できないため、システムは停止コードを発行する必要があります。  パラメーター2は HighestPhysicalPage です。</p></td>
</tr>
</tbody>
</table>


<a name="resolution"></a>解像度
----------

! [デバッグ拡張機能の[**分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。 

Windows メモリ診断ツールを実行すると、物理メモリモジュールに影響するあらゆる種類の問題を除外するのにも役立ちます。

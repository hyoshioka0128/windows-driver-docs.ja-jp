---
title: バグ チェック 0x76 PROCESS_HAS_LOCKED_PAGES
description: PROCESS_HAS_LOCKED_PAGES のバグ チェックでは、0x00000076 の値を持ちます。 このバグ チェックでは、I/O 操作の後にロックされたページを解放するドライバーが失敗したことを示します。
ms.assetid: 25c63e2e-6d2a-401a-b523-ffa70e9f75df
keywords:
- バグ チェック 0x76 PROCESS_HAS_LOCKED_PAGES
- PROCESS_HAS_LOCKED_PAGES
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- PROCESS_HAS_LOCKED_PAGES
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f62046d30d581dd4d1668d01dce3fcf785051ecc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361750"
---
# <a name="bug-check-0x76-processhaslockedpages"></a>バグ チェック 0x76:プロセス\_HAS\_ロック\_ページ


プロセス\_HAS\_ロック\_ページのバグ チェックが 0x00000076 の値を持ちます。 このバグ チェックでは、I/O 操作の後にロックされたページを解放するドライバーが失敗したこと、またはが既にロックされているページのロックを解除しようとしたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


## <a name="processhaslockedpages-parameters"></a>プロセス\_HAS\_ロック\_ページ パラメーター


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
<td align="left"><p>0x00</p></td>
<td align="left"><p>プロセス オブジェクトへのポインター</p></td>
<td align="left"><p>ロックされたページ数</p></td>
<td align="left"><p>(有効) の場合、ドライバー スタックへのポインター。 それ以外の場合、このパラメーターは 0 です。</p></td>
<td align="left"><p>終了中のプロセスでは、メモリ ページをロックします。 ドライバーには、プロセスが終了する前に、プロセスでそれをロックしている可能性がありますメモリがロックを解除する必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x01</p></td>
<td align="left"><p>ドライバーで指定された MDL</p></td>
<td align="left"><p>現在のプロセスでは、ロックされたメモリ ページ数</p></td>
<td align="left"><p>(有効) の場合は、そのプロセスのドライバー スタックへのポインター。 それ以外の場合、このパラメーターは 0 です。</p></td>
<td align="left"><p>ドライバーがロックされていないプロセスのメモリ ページのロックを解除しようとしています。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

ロックされているページのロックを解除できなかったか、ドライバー (パラメーター 1 の値は 0x0)、またはドライバーがロックされていない、またはが既にロックされているページのロックを解除しようと (パラメーター 1 の値は 0x1 です)。

<a name="resolution"></a>解決方法
----------

[ **! 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)バグ チェックに関する情報を表示拡張機能をデバッグおよび根本原因を突き止めるに役に立ちます。

**パラメーター 1 の値は 0x0 場合**

まずを使用して、 [ **! 検索**](-search.md)全体ですべての物理メモリの現在のプロセス ポインターで拡張機能。 この拡張機能は、現在のプロセスが指すメモリの少なくとも 1 つ記述子一覧 (MDL) にあります。 次に、使用 **! 検索**現在のプロセスが指す I/O 要求パケット (IRP) を取得する表示されている各 MDL にします。 この IRP では、ドライバーは、ページのリークを識別できます。

それ以外の場合、ドライバー、レジストリを編集してエラーの原因を検出できます。

1.  **\\ \\HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール\\セッション マネージャー\\メモリ管理**のレジストリ キーを作成または編集、 **TrackLockedPages**値に設定して、DWORD 1 に設定します。

2.  コンピューターを再起動します。

システムは、問題の原因となったドライバーを簡単に識別できるようにし、スタック トレースを保存します。 場合は、ドライバーが原因で、もう一度同じエラー [**バグ チェック 0xCB** ](bug-check-0xcb--driver-left-locked-pages-in-process.md) (ドライバー\_左\_ロック\_ページ\_IN\_プロセス) が発行されます。、このエラーが発生したドライバーの名前がブルー スクリーンに表示され、場所のメモリに格納されていると (PUNICODE\_文字列) **KiBugCheckDriver**します。

**パラメーター 1 の値が 0x1 の場合**

ロックし、メモリのロックを解除するドライバーのソース コードを調べ、メモリがロックされている最初ないインスタンスを検索しようとしています。 ロックされています。

 

 





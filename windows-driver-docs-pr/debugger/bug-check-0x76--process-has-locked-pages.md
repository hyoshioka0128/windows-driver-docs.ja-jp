---
title: 0x76 PROCESS_HAS_LOCKED_PAGES のバグチェック
description: PROCESS_HAS_LOCKED_PAGES バグチェックの値は0x00000076 です。 このバグチェックは、i/o 操作後にロックされたページをドライバーが解放できなかったことを示します。
ms.assetid: 25c63e2e-6d2a-401a-b523-ffa70e9f75df
keywords:
- 0x76 PROCESS_HAS_LOCKED_PAGES のバグチェック
- PROCESS_HAS_LOCKED_PAGES
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- PROCESS_HAS_LOCKED_PAGES
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 50694b44d9ec169bbafdfb6367b971411bb099c0
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534615"
---
# <a name="bug-check-0x76-process_has_locked_pages"></a>バグチェック 0x76: プロセス \_ にロックされたページがあります \_ \_


プロセスでロックされた \_ \_ ページの \_ バグチェックには、値0x00000076 が指定されています。 このバグチェックは、i/o 操作後にドライバーがロックされたページを解放できなかったか、既にロックが解除されているページのロックを解除しようとしたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="process_has_locked_pages-parameters"></a>プロセス \_ にロックされた \_ \_ ページパラメーターがあります


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
<td align="left"><p>0x00</p></td>
<td align="left"><p>プロセスオブジェクトへのポインター</p></td>
<td align="left"><p>ロックされたページの数</p></td>
<td align="left"><p>ドライバースタックへのポインター (有効になっている場合)。 それ以外の場合、このパラメーターは0になります。</p></td>
<td align="left"><p>終了しようとしているプロセスには、ロックされているメモリページがあります。 プロセスが終了する前に、ドライバーがプロセスでロックされている可能性のあるすべてのメモリのロックを解除する必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x01</p></td>
<td align="left"><p>ドライバーによって指定された MDL</p></td>
<td align="left"><p>そのプロセス内の現在のロックされているメモリページ数</p></td>
<td align="left"><p>そのプロセスのドライバースタックへのポインター (有効になっている場合)。 それ以外の場合、このパラメーターは0になります。</p></td>
<td align="left"><p>ドライバーは、ロックされていないプロセスメモリページのロックを解除しようとしています。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

ドライバーは、ロックされたページのロック解除に失敗したか (パラメーター1の値が 0x0)、またはロックされていないページのロックを解除しようとしています (パラメーター1の値が 0x1)。

<a name="resolution"></a>解像度
----------

! [デバッグ拡張機能の[**分析**](-analyze.md)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。

**パラメーター1の値が0x0 の場合**

最初に、すべての物理メモリ内の現在のプロセスポインターで[**! search**](-search.md)拡張機能を使用します。 この拡張機能では、現在のプロセスを指すメモリ記述子リスト (MDL) が少なくとも1つ見つかります。 次に、検出された各 MDL に対して **! search**を使用して、現在のプロセスを参照する i/o 要求パケット (IRP) を取得します。 この IRP から、どのドライバーがページをリークしているかを特定できます。

それ以外の場合は、レジストリを編集することで、エラーの原因となったドライバーを検出できます。

1.  ** \\ \\ HKEY \_ LOCAL \_ MACHINE \\ SYSTEM \\ CurrentControlSet \\ Control \\ Session Manager \\ Memory Management**レジストリキーで、 **TrackLockedPages**の値を作成または編集し、それを DWORD 1 に設定します。

2.  コンピューターを再起動します。

システムはスタックトレースを保存するため、問題の原因となったドライバーを簡単に特定できます。 ドライバーによって同じエラーが再度発生する場合は、[**バグチェック 0xCB**](bug-check-0xcb--driver-left-locked-pages-in-process.md) ( \_ \_ \_ \_ 処理中のドライバーのロック済みページ \_ ) が発行され、このエラーの原因となったドライバーの名前がブルースクリーンに表示され、メモリ内の場所 (punicode \_ 文字列) **KiBugCheckDriver**に格納されます。

**パラメーター1の値が0x1 の場合**

メモリをロックおよびロック解除するドライバーのソースコードを調べ、最初にロックされることなくメモリのロックが解除されているインスタンスを見つけようとします。

 

 





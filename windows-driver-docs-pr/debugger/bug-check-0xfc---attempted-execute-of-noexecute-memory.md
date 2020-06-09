---
title: バグチェック 0xFC ATTEMPTED_EXECUTE_OF_NOEXECUTE_MEMORY
description: ATTEMPTED_EXECUTE_OF_NOEXECUTE_MEMORY のバグチェックの値は、0x000000FC です。 これは、実行可能でないメモリを実行しようとしたことを示します。
ms.assetid: bece76bd-03ca-40fd-a69b-f6cc05d09806
keywords:
- バグチェック 0xFC ATTEMPTED_EXECUTE_OF_NOEXECUTE_MEMORY
- ATTEMPTED_EXECUTE_OF_NOEXECUTE_MEMORY
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ATTEMPTED_EXECUTE_OF_NOEXECUTE_MEMORY
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d50724bba4a07e9c181100a55bba8f08df34bc34
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534785"
---
# <a name="bug-check-0xfc-attempted_execute_of_noexecute_memory"></a>バグチェック 0xFC: \_ \_ \_ noexecute メモリの実行を試みました \_


\_ \_ Noexecute メモリのバグチェックを実行しようとしたときに、 \_ \_ 値0x000000fc が指定されています。 これは、実行可能でないメモリを実行しようとしたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="attempted_execute_of_noexecute_memory-parameters"></a>\_ \_ \_ Noexecute MEMORY パラメーターの実行が \_ 試行されました


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
<td align="left"><p>実行しようとした仮想アドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>ページテーブルエントリ (PTE) の内容</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
</tbody>
</table>

 

<a name="resolution"></a>解像度
----------

! [デバッグ拡張機能の[**分析**](-analyze.md)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。
可能な場合は、実行不可能なメモリを実行しようとしたドライバー名の Unicode 文字列がバグチェック画面に出力され、 **KiBugCheckDriver**にも保存されます。 そうでない場合は、スタックトレースを実行し、現在の命令ポインターを確認することで、問題のドライバーが見つかることがよくあります。

 

 





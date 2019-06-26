---
title: バグ チェック 0 xfc ATTEMPTED_EXECUTE_OF_NOEXECUTE_MEMORY
description: ATTEMPTED_EXECUTE_OF_NOEXECUTE_MEMORY のバグ チェックでは、0x000000FC の値を持ちます。 これは、非実行可能メモリを実行しようとすることを示します。
ms.assetid: bece76bd-03ca-40fd-a69b-f6cc05d09806
keywords:
- バグ チェック 0 xfc ATTEMPTED_EXECUTE_OF_NOEXECUTE_MEMORY
- ATTEMPTED_EXECUTE_OF_NOEXECUTE_MEMORY
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ATTEMPTED_EXECUTE_OF_NOEXECUTE_MEMORY
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 09901e5f697dd8749600685cd57d22c8ae21fcb6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361483"
---
# <a name="bug-check-0xfc-attemptedexecuteofnoexecutememory"></a>バグ チェック 0xFC:試行\_EXECUTE\_の\_NOEXECUTE\_メモリ


試行\_EXECUTE\_の\_NOEXECUTE\_メモリのバグ チェックが 0x000000FC の値を持ちます。 これは、非実行可能メモリを実行しようとすることを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


## <a name="attemptedexecuteofnoexecutememory-parameters"></a>試行\_EXECUTE\_の\_NOEXECUTE\_メモリ パラメーター


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
<td align="left"><p>実行が試行された仮想アドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>ページ テーブル エントリ (PTE) の内容</p></td>
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

 

<a name="resolution"></a>解決方法
----------

[ **! 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)バグ チェックに関する情報を表示拡張機能をデバッグおよび根本原因を突き止めるに役に立ちます。
非実行可能メモリを実行しようとするドライバー名の Unicode 文字列がバグの確認画面で印刷されはでも保存可能であれば、 **KiBugCheckDriver**します。 それ以外の場合、ドライバーの問題は、多くの場合、スタック トレースを実行し、現在の命令ポインターをレビューして確認できます。

 

 





---
title: バグチェック 0xBE ATTEMPTED_WRITE_TO_READONLY_MEMORY
description: ATTEMPTED_WRITE_TO_READONLY_MEMORY バグチェックの値は0x000000BE です。 これは、ドライバーが読み取り専用のメモリセグメントに書き込もうとした場合に発行されます。
ms.assetid: d6247828-09ae-4071-9b4f-917af29265bc
keywords:
- バグチェック 0xBE ATTEMPTED_WRITE_TO_READONLY_MEMORY
- ATTEMPTED_WRITE_TO_READONLY_MEMORY
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ATTEMPTED_WRITE_TO_READONLY_MEMORY
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: be0219f1be94a0355509cf84e226ecad9f5fc563
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534797"
---
# <a name="bug-check-0xbe-attempted_write_to_readonly_memory"></a>バグチェック 0xBE: \_ \_ \_ 読み取り専用メモリへの書き込みを試行しました \_


\_読み取り専用メモリへの書き込み試行のバグチェックには、 \_ \_ \_ 値0x000000be が設定されています。 これは、ドライバーが読み取り専用のメモリセグメントに書き込もうとした場合に発行されます。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="attempted_write_to_readonly_memory-parameters"></a>\_ \_ \_ 読み取り専用 \_ メモリパラメーターへの書き込みが試行されました


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
<td align="left"><p>書き込み試行の仮想アドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>PTE の内容</p></td>
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

 

エラーの原因となっているドライバーを識別できる場合は、その名前が青色の画面に出力され、メモリ内の場所 (PUNICODE \_ 文字列) **KiBugCheckDriver**に格納されます。


<a name="remarks"></a>注釈
-------

! [デバッグ拡張機能の[**分析**](-analyze.md)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。
 





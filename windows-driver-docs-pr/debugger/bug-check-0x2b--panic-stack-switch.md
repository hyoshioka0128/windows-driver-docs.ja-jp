---
title: バグチェック 0x2B PANIC_STACK_SWITCH
description: PANIC_STACK_SWITCH のバグチェックには、0x0000002B の値が指定されています。 これは、カーネルモードスタックがオーバーランしたことを示します。
ms.assetid: 0ab28a16-979d-4b40-812a-a31fac3f6be8
keywords:
- バグチェック 0x2B PANIC_STACK_SWITCH
- PANIC_STACK_SWITCH
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- PANIC_STACK_SWITCH
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7f72d552417809635692772e693f50341a73aecc
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534823"
---
# <a name="bug-check-0x2b-panic_stack_switch"></a>バグチェック 0x2B: パニック \_ スタック \_ スイッチ


パニック \_ スタックスイッチのバグチェックには、 \_ 0x0000002b の値が指定されています。 これは、カーネルモードスタックがオーバーランしたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="panic_stack_switch-parameters"></a>パニック \_ スタック \_ スイッチパラメーター


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
<td align="left"><p>トラップフレーム</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>予約済み</p></td>
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

 

<a name="cause"></a>原因
-----

このエラーは通常、カーネルモードドライバーが使用しているスタック領域が多すぎる場合に表示されます。 また、カーネルで深刻なデータ破損が発生した場合にも表示されます。


## <a name="resolution"></a>解像度
! [デバッグ拡張機能の[**分析**](-analyze.md)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。
 

 





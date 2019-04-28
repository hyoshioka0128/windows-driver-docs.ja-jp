---
title: バグ チェック 0x2B PANIC_STACK_SWITCH
description: PANIC_STACK_SWITCH のバグ チェックでは、0x0000002B の値を持ちます。 これは、カーネル モード スタックがオーバーランすることを示します。
ms.assetid: 0ab28a16-979d-4b40-812a-a31fac3f6be8
keywords:
- バグ チェック 0x2B PANIC_STACK_SWITCH
- PANIC_STACK_SWITCH
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- PANIC_STACK_SWITCH
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0572fd89535adc906ed8f16cc9bcaec1017d73b7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361547"
---
# <a name="bug-check-0x2b-panicstackswitch"></a>バグ チェック 0x2B:パニック\_スタック\_スイッチ


パニック\_スタック\_スイッチのバグ チェックが 0x0000002B の値を持ちます。 これは、カーネル モード スタックがオーバーランすることを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="panicstackswitch-parameters"></a>パニック\_スタック\_スイッチ パラメーター


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
<td align="left"><p>トラップ フレーム</p></td>
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

このエラーは、通常、カーネル モード ドライバーは、スタック領域が多すぎるを使用する場合に表示されます。 これは、カーネルの重大なデータ破損が発生したときにも表示できます。


## <a name="resolution"></a>解決方法
[ **! 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)バグ チェックに関する情報を表示拡張機能をデバッグおよび根本原因を突き止めるに役に立ちます。
 

 





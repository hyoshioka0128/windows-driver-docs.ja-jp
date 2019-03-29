---
title: バグ チェック 0x41 MUST_SUCCEED_POOL_EMPTY
description: MUST_SUCCEED_POOL_EMPTY のバグ チェックでは、0x00000041 の値を持ちます。 これは、カーネル モードのスレッドが多すぎる must-succeed プールを要求したことを示します。
ms.assetid: 10aafcf4-6af0-41b5-803c-578369bdd810
keywords:
- バグ チェック 0x41 MUST_SUCCEED_POOL_EMPTY
- MUST_SUCCEED_POOL_EMPTY
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- MUST_SUCCEED_POOL_EMPTY
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: beb923e4ffa031d365f40d9a7c6f69a4a957b3bf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578017"
---
# <a name="bug-check-0x41-mustsucceedpoolempty"></a>バグ チェック 0x41:必要があります\_SUCCEED\_プール\_空


必要があります\_SUCCEED\_プール\_空のバグ チェックが 0x00000041 の値を持ちます。 これは、カーネル モードのスレッドが多すぎる must-succeed プールを要求したことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="mustsucceedpoolempty-parameters"></a>必要があります\_SUCCEED\_プール\_空のパラメーター


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
<td align="left"><p>満たされていない要求のサイズ</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>非ページ プールから使用されるページ数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>PAGE_SIZE よりも大きい非ページ プールからの要求の数</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>使用可能なページの数</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

要求するドライバーは許可されていませんプールの必要があります-成功します。

Must-succeed 要求を満たすことができない場合は、このバグ チェックが発行されます。

<a name="resolution"></a>解決方法
----------

置換または要求を行っているドライバーを書き直してください。 ドライバーはプールの必要があります-成功を要求する必要があります。 代わりに、通常のプールを要求し、プールが一時的に空のシナリオを適切に処理が必要があります。

[ **Kb (Display Stack Backtrace)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)コマンド エラーの原因となったドライバーが表示されます。

また、2 番目のコンポーネントでは、must-succeed プールを使い果たしました可能です。 まず、ケースを確認するには、を使用して、 **kb**コマンド。 使用して[ **vm 1** ](-vm.md)合計プールの使用状況を表示する[ **! poolused 2** ](-poolused.md) nonpaged タグごとに表示するプールの使用状況、および **!。poolused 4**個々 のタグを表示するページ プールの使用量。 ほとんどのプールを使用して、タグに関連付けられているコンポーネントは、問題の原因で、可能性があります。

 

 





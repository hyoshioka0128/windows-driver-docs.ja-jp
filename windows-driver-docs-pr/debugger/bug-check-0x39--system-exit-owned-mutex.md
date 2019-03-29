---
title: バグ チェック 0x39 SYSTEM_EXIT_OWNED_MUTEX
description: SYSTEM_EXIT_OWNED_MUTEX のバグ チェックでは、0x00000039 の値を持ちます。 これは、ワーカーのルーチンが所有、ミュー テックス オブジェクトを解放することがなく返されることを示します。
ms.assetid: 79257486-f65e-4d02-acf0-b7f0607a21cc
keywords:
- バグ チェック 0x39 SYSTEM_EXIT_OWNED_MUTEX
- SYSTEM_EXIT_OWNED_MUTEX
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- SYSTEM_EXIT_OWNED_MUTEX
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4890cfe1cf28c4ba9700ed0fe8e15706af6198a2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582267"
---
# <a name="bug-check-0x39-systemexitownedmutex"></a>バグ チェック 0x39:システム\_終了\_所有されている\_ミュー テックス


システム\_終了\_所有されている\_ミュー テックスのバグ チェックが 0x00000039 の値を持ちます。 これは、ワーカーのルーチンが所有、ミュー テックス オブジェクトを解放することがなく返されることを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="systemexitownedmutex-parameters"></a>システム\_終了\_所有されている\_ミュー テックス パラメーター


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
<td align="left"><p>エラーの原因となったワーカー ルーチンのアドレス。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>ワーカーのルーチンに渡されるパラメーター。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>作業項目のアドレス。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>予約済み。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

ワーカー ルーチンは、ミュー テックス オブジェクトも所有しているときに返されます。 現在のワーカー スレッドが他の関連のない作業項目を実行する処理が続行され、ミュー テックスが解放されません。

<a name="resolution"></a>解決方法
----------

この問題を分析するには、デバッガーが必要です。 エラーが発生したドライバーを検索するには、使用、 **ln**デバッガー コマンドを (最も近いシンボルの一覧)。

kd&gt; ln アドレス

アドレスのパラメーター 1 で指定されたワーカー ルーチンです。

 

 





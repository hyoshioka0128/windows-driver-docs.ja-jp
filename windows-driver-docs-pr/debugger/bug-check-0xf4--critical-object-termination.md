---
title: Bug Check 0xF4 CRITICAL_OBJECT_TERMINATION
description: CRITICAL_OBJECT_TERMINATION のバグ チェックでは、0x000000F4 の値を持ちます。 これは、ことプロセスまたはスレッド システムを操作するために重要が予期せず終了または終了したことを示します。
ms.assetid: 51a73ada-5e82-45a2-ad2a-8ef53f96318c
keywords:
- Bug Check 0xF4 CRITICAL_OBJECT_TERMINATION
- CRITICAL_OBJECT_TERMINATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CRITICAL_OBJECT_TERMINATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8b21b988ada0a56956a36ecce7e18d0dfb5258f0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548932"
---
# <a name="bug-check-0xf4-criticalobjecttermination"></a>バグ チェック 0xF4 の。重要な\_オブジェクト\_終了


CRITICAL\_オブジェクト\_終了バグ チェックが 0x000000F4 の値を持ちます。 これは、ことプロセスまたはスレッド システムを操作するために重要が予期せず終了または終了したことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="criticalobjecttermination-parameters"></a>重要な\_オブジェクト\_終了パラメーター


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
<td align="left"><p>終端のオブジェクトの種類:</p>
<p><strong>0x3:</strong>Process</p>
<p><strong>0x6:</strong>スレッド</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>終端オブジェクト</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>プロセスのイメージ ファイル名</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>説明のメッセージを含む ASCII 文字列へのポインター</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

いくつかのプロセスとスレッドは、システムの操作に必要なのです。 何らかの理由で停止されるときにシステムが機能しないことができます。

 
<a name="resolution"></a>解決方法
----------

[ **! 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)バグ チェックに関する情報を表示拡張機能をデバッグおよび根本原因を突き止めるには非常に役に立ちます。
 





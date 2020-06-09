---
title: バグチェック 0xF4 CRITICAL_OBJECT_TERMINATION
description: CRITICAL_OBJECT_TERMINATION のバグチェックの値が0x000000F4 になっています。 これは、システム操作にとって重要なプロセスまたはスレッドが予期せず終了または終了されたことを示します。
ms.assetid: 51a73ada-5e82-45a2-ad2a-8ef53f96318c
keywords:
- バグチェック 0xF4 CRITICAL_OBJECT_TERMINATION
- CRITICAL_OBJECT_TERMINATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CRITICAL_OBJECT_TERMINATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2b5b38327eeede96d0e2e7cb1d579153c33ac070
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534789"
---
# <a name="bug-check-0xf4-critical_object_termination"></a>バグチェック 0xF4: 重要な \_ オブジェクトの \_ 終了


重要な \_ オブジェクトの終了のバグチェックには、 \_ 値0x000000f4 があります。 これは、システム操作にとって重要なプロセスまたはスレッドが予期せず終了または終了されたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="critical_object_termination-parameters"></a>重要な \_ オブジェクト \_ 終了パラメーター


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
<td align="left"><p>終了するオブジェクトの種類:</p>
<p><strong>0x3:</strong>Process</p>
<p><strong>0x6:</strong>レッド</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>終了するオブジェクト</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>プロセスイメージのファイル名</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>説明メッセージを含む ASCII 文字列へのポインター</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

システムを操作するには、いくつかのプロセスとスレッドが必要です。 何らかの理由で終了した場合、システムは機能しなくなります。

 
<a name="resolution"></a>解像度
----------

! [デバッグ拡張機能の[**分析**](-analyze.md)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。
 





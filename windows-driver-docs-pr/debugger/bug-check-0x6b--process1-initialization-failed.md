---
title: バグ チェック 0x6B PROCESS1_INITIALIZATION_FAILED
description: PROCESS1_INITIALIZATION_FAILED のバグ チェックでは、0x0000006B の値を持ちます。 このバグ チェックでは、Microsoft Windows オペレーティング システムの初期化が失敗したことを示します。
ms.assetid: 8680d924-3041-4927-a228-52b281bbc267
keywords:
- バグ チェック 0x6B PROCESS1_INITIALIZATION_FAILED
- PROCESS1_INITIALIZATION_FAILED
ms.date: 06/27/2018
topic_type:
- apiref
api_name:
- PROCESS1_INITIALIZATION_FAILED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3cbd94e081b19f34fda6e198b6d80beabb0a16de
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59902956"
---
# <a name="bug-check-0x6b-process1initializationfailed"></a>バグ チェック 0x6B:PROCESS1\_初期化\_失敗


PROCESS1\_初期化\_失敗のバグ チェックが 0x0000006B の値を持ちます。 このバグ チェックでは、Microsoft Windows オペレーティング システムの初期化が失敗したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="process1initializationfailed-parameters"></a>PROCESS1\_初期化\_FAILED パラメーター


次のパラメーターは、ブルー スクリーンに表示されます。

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
<td align="left"><p>エラーの原因となった NT 状態コード</p></td>
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

ディスク サブシステムの任意の部分は、PROCESS1 可能性\_初期化\_失敗のバグ チェック、不良ディスクを含む同じチェーン、またはないので、使用可能なドライブ上の ATA 型デバイスの混在、不正または不適切なケーブルハードウェアの再生成します。

このバグ チェックも可能性があります、ブート パーティションから不足しているファイルまたはでユーザーが誤って無効になっているドライバー、**ドライバー**タブ。

 
## <a name="resolution"></a>解決方法
[ **! 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)バグ チェックに関する情報を表示拡張機能をデバッグおよび根本原因を突き止めるに役に立ちます。 





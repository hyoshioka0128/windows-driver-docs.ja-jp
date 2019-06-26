---
title: デバッグ\_プロセス\_XXX
description: 処理オプションは、少しデバッガー エンジンによるユーザー modeprocesses の処理方法を制御するに設定されます。 これらの処理オプションの一部はグローバルです。他のユーザーは、プロセスに固有です。
ms.assetid: 5b485ae2-6d97-4cfc-b2bf-ad8ddca268a8
ms.date: 12/07/2017
topic_type:
- apiref
api_name:
- DEBUG_PROCESS_DETACH_ON_EXIT
- DEBUG_PROCESS_ONLY_THIS_PROCESS
api_location:
- DbgEng.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.openlocfilehash: dd957c3e15efbc2a06f05374b5b43a05852a8f72
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366980"
---
# <a name="debugprocessxxx"></a>デバッグ\_プロセス\_XXX


処理オプションがそのコントロールを設定して少し方法、[デバッガー エンジン](https://docs.microsoft.com/windows-hardware/drivers/debugger/introduction#debugger-engine)ユーザー モードを扱う[プロセス](https://docs.microsoft.com/windows-hardware/drivers/debugger/controlling-threads-and-processes#processes)します。 これらの処理オプションの一部はグローバルです。他のユーザーは、プロセスに固有です。

処理オプションは、ライブ ユーザー モードのデバッグにのみ適用されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ビット フラグ</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><span id="DEBUG_PROCESS_DETACH_ON_EXIT"></span><span id="debug_process_detach_on_exit"></span>
<strong>DEBUG_PROCESS_DETACH_ON_EXIT</strong></td>
<td align="left"><p>デバッガーに自動的に自体はプロセスからデタッチ ターゲット、デバッガーが終了したとき。 これは、グローバル設定です。</p></td>
</tr>
<tr class="even">
<td align="left"><span id="DEBUG_PROCESS_ONLY_THIS_PROCESS"></span><span id="debug_process_only_this_process"></span>
<strong>DEBUG_PROCESS_ONLY_THIS_PROCESS</strong></td>
<td align="left"><p>デバッガーでは、このプロセスによって作成された子プロセスはデバッグできません。</p></td>
</tr>
</tbody>
</table>

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">DbgEng.h (DbgEng.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[ **.childdbg**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-childdbg--debug-child-processes-)

 

 







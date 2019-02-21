---
title: .breakin (カーネル デバッガーにブレーク)
description: .Breakin コマンドは、ユーザー モードのデバッグのカーネル モードのデバッグに切り替えます。 このコマンドは、カーネル デバッガーからユーザー モード デバッガーの制御を行うときに特に便利です。
ms.assetid: f0dab2c2-60f4-4a85-91bd-6379b247ceaf
keywords:
- .breakin (カーネル デバッガーに中断) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .breakin (Break to the Kernel Debugger)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ead826fad720ba8e9729b0044cd2db10064a1fe0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560145"
---
# <a name="breakin-break-to-the-kernel-debugger"></a>.breakin (カーネル デバッガーにブレーク)


**.Breakin**コマンドがユーザー モードのデバッグのカーネル モードのデバッグに切り替えます。 このコマンドは、カーネル デバッガーからユーザー モード デバッガーの制御を行うときに特に便利です。

```dbgcmd
    .breakin 
```

## <span id="ddk_meta_break_to_the_kernel_debugger_dbg"></span><span id="DDK_META_BREAK_TO_THE_KERNEL_DEBUGGER_DBG"></span>


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでのみ</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ デバッグのみ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

ブート プロセス中に、カーネル モードのデバッグが有効にし、ユーザー モード デバッガーを実行している場合は使用できます、 **.breakin**オペレーティング システムを停止し、カーネル デバッガーに制御を転送するコマンド。

**.Breakin**コマンドは、デバッガーのプロセスのコンテキストでカーネル モードの中断を実行します。 カーネル デバッガーがアタッチされている場合は、アクティブになります。 カーネル デバッガーの[プロセス コンテキスト](changing-contexts.md)ユーザー モード デバッガーのターゲット プロセスではなく、ユーザー モード デバッガーのプロセスに自動的に設定されます。

このコマンドは、ユーザー モードの問題をデバッグする場合は、システムのカーネルの状態に関する情報を取得する必要がある場合、主に使用します。 ユーザー モードのデバッグ セッションを続行するには、カーネル デバッガーでの実行を再開すると必要があります。

したら[カーネル デバッガーからユーザー モード デバッガーの制御](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)ユーザー モード デバッガーのプロンプトがカーネル デバッガーに表示されると、このコマンドをユーザー モード デバッガーを一時停止し、カーネル モード デバッグのプロンプトを行います表示されます。

システムでカーネル デバッガーを中断することがない場合、エラー メッセージが表示されます。

このコマンドは、カーネル デバッガーを使用してユーザー領域でブレークポイントを設定して、そのブレークポイントは、カーネル デバッガーではなくユーザー モード デバッガーでキャッチされた場合にも役立ちます。 ユーザー モード デバッガーでこのコマンドを発行すると、カーネル デバッガーに制御が転送されます。

場合、 **.breakin**コマンドを使用したデバッグを有効に起動されていないシステムで、影響を与えません。

 

 






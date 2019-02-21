---
title: .sleep (デバッガーを一時停止)
description: .Sleep コマンドは、ユーザー モード デバッガーを一時停止と対象コンピューターがアクティブになるとします。 このコマンドは、カーネル デバッガーからユーザー モード デバッガーの制御を行うときにのみ使用されます。
ms.assetid: bc3ee17f-e3b8-4bdb-8c80-6b1fef29000e
keywords:
- デバッガー (.sleep) コマンドを一時停止します。
- カーネル デバッガーを一時停止のデバッガー (.sleep) コマンドからユーザー モード デバッガーの制御
- .sleep (デバッガーを一時停止) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .sleep (Pause Debugger)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1d05c72238575ddf79a51f0f7e9f2035212e0dde
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559849"
---
# <a name="sleep-pause-debugger"></a>.sleep (デバッガーを一時停止)


**.Sleep**コマンドがアクティブになると対象コンピューターの一時停止をユーザー モードのデバッガーを実行します。 このコマンドは、カーネル デバッガーからユーザー モード デバッガーの制御を行うときにのみ使用されます。

```dbgcmd
.sleep milliseconds
```

## <a name="span-idddkmetapausedebuggerdbgspanspan-idddkmetapausedebuggerdbgspanparameters"></a><span id="ddk_meta_pause_debugger_dbg"></span><span id="DDK_META_PAUSE_DEBUGGER_DBG"></span>パラメーター


<span id="_______milliseconds______"></span><span id="_______MILLISECONDS______"></span> *(ミリ秒)*   
一時停止、ミリ秒単位の長さを指定します。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>カーネル デバッガーからユーザー モード デバッガーの制御</p></td>
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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細およびスリープ モードのデバッガーを起動する方法については、次を参照してください。[カーネル デバッガーからユーザー モード デバッガーの制御](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)します。

<a name="remarks"></a>注釈
-------

カーネル デバッガーからユーザー モード デバッガーの制御を行うと、ユーザー モード デバッガーのプロンプトがカーネル デバッガーに表示される、このコマンドはスリープ モードを有効にします。 カーネル デバッガーや、ユーザー モード デバッガーが、ターゲット アプリケーションのすべては固定が、ターゲット コンピューターの残りの部分がアクティブになります。

その他のシナリオでこのコマンドを使用する場合は、一定期間だけです、デバッガーを固定にされます。

スリープ時間 (ミリ秒単位) は、しない限り、既定の基数に従って解釈されますなどのプレフィックス**0n**使用されます。 したがって、既定の基数が 16 の場合は、次のコマンドには約 65 秒スリープが発生します。

```dbgcmd
0:000> .sleep 10000
```

 

 






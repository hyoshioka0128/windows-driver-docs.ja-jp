---
title: gh (例外処理ありで実行)
description: Gh コマンドは、特定のスレッドの例外として処理されたことを示し、スレッドで例外が発生した命令の実行を再起動することができます。
ms.assetid: 3e06a3ff-b57d-435f-9625-011f38d7b26a
keywords:
- gh (例外処理での移動) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- gh (Go with Exception Handled)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f42e7c2a2f07a925fe63a662f7de3350ade490d1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570726"
---
# <a name="gh-go-with-exception-handled"></a>gh (例外処理ありで実行)


**Gh**コマンドは、特定のスレッドの例外が処理済みとしてマークし、スレッドで例外が発生した命令の実行を再起動することができます。

ユーザー モードの構文

```dbgcmd
[~Thread] gh[a] [= StartAddress] [BreakAddress ... [; BreakCommands]] 
```

カーネル モードの構文

```dbgcmd
gh[a] [= StartAddress] [BreakAddress ... [; BreakCommands]] 
```

## <a name="span-idddkcmdgowithexceptionhandleddbgspanspan-idddkcmdgowithexceptionhandleddbgspanparameters"></a><span id="ddk_cmd_go_with_exception_handled_dbg"></span><span id="DDK_CMD_GO_WITH_EXCEPTION_HANDLED_DBG"></span>パラメーター


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *スレッド*   
(ユーザー モードのみ)スレッドの実行を指定します。 このスレッドは、例外によって停止している必要があります。 構文の詳細については、[スレッド構文](thread-syntax.md)を参照してください。

<span id="_______a______"></span><span id="_______A______"></span> **A**   
プロセッサのブレークポイントにするには、このコマンドによって作成されたすべてのブレークポイントの発生 (などによって作成された[ **ba**](ba--break-on-access-.md)) ソフトウェア ブレークポイントではなく (などによって作成された[ **bp** ](bp--bu--bm--set-breakpoint-.md)と**bm**)。 場合*BreakAddress*が指定されていない、ブレークポイントは作成されません、 **、** フラグが影響を与えません。

<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span> *StartAddress*   
実行を開始するアドレスを指定します。 これが指定されていない、デバッガーは実行をアドレス通過し、例外が発生します。 構文の詳細については、[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)を参照してください。

<span id="_______BreakAddress______"></span><span id="_______breakaddress______"></span><span id="_______BREAKADDRESS______"></span> *BreakAddress*   
ブレークポイントを設定するアドレスを指定します。 場合*BreakAddress*指定すると、命令アドレスを指定する必要があります (つまり、アドレス必要命令の最初のバイトがあります)。 最大 10 個の区切りは、任意の順序でのアドレスを一度に 1 つ指定できます。 場合*BreakAddress*解決できないとして格納されて、[未解決ブレークポイント](unresolved-breakpoints---bu-breakpoints-.md)します。 構文の詳細については、[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)を参照してください。

<span id="_______BreakCommands______"></span><span id="_______breakcommands______"></span><span id="_______BREAKCOMMANDS______"></span> *BreakCommands*   
ブレークポイントが指定されたときに自動的に実行する 1 つまたは複数のコマンドを指定します*BreakAddress*にヒットします。 *BreakCommands*パラメーターの先頭にセミコロンする必要があります。 複数*BreakAddress*値を指定すると、 *BreakCommands*それらすべてに適用されます。

**注**   、 *BreakCommands*パラメーターは、たとえば、別のブレークポイント コマンド内でまたは内 - 別のコマンドによって使用されるコマンド文字列内でこのコマンドを埋め込む場合にのみ使用します。除くまたはイベントの設定。 セミコロンを終了する、コマンド ラインで、 **gh**後すぐに実行される、セミコロンの後、コマンド、および追加のコマンドが表示されている、 **gh**コマンドを実行します。

 

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでは、カーネル モード</p></td>
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

このコマンドと、関連するコマンドの概要を発行するには、他の方法を参照してください。[ターゲットを制御する](controlling-the-target.md)します。

<a name="remarks"></a>コメント
-------

使用する場合、 *BreakAddress*ブレークポイント、この新しいブレークポイントを設定するパラメーターは、現在のスレッドによってのみトリガーされます。 その場所でコードを実行する他のスレッドは停止します。

場合*スレッド*が指定されている、 **gh**コマンドを実行すると、指定されたスレッドのフリーズとフリーズ他のすべて。 たとえば場合、 **~ 123gh**、  **~ \#gh**、または **~ \*gh**コマンドを指定すると、指定されたスレッド固定されたでない他のすべてのユーザーが固定されているとします。

 

 






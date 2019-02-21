---
title: gn、gN (Go 処理されない例外を使用)
description: Gn と gN コマンド、例外が処理済みとしてマークすることがなく特定のスレッドの実行を続行します。 これにより、アプリケーションの例外のハンドラーが例外を処理できます。
ms.assetid: b6f69882-b30a-45b7-b777-1b4857719e7f
keywords:
- gn、gN (Go 処理されない例外で) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- gn, gN (Go with Exception Not Handled)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ab11fa4e087cce9bb0448eee10dff4e95e551d46
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558040"
---
# <a name="gn-gn-go-with-exception-not-handled"></a>gn、gN (Go 処理されない例外を使用)


**Gn**と**gN**コマンドは、例外が処理済みとしてマークすることがなく特定のスレッドの実行を続行します。 これにより、アプリケーションの例外のハンドラーが例外を処理できます。

ユーザー モードの構文

```dbgcmd
[~Thread] gn[a] [= StartAddress] [BreakAddress ... [; BreakCommands]] 
[~Thread] gN[a] [= StartAddress] [BreakAddress ... [; BreakCommands]] 
```

カーネル モードの構文

```dbgcmd
gn[a] [= StartAddress] [BreakAddress ... [; BreakCommands]] 
gN[a] [= StartAddress] [BreakAddress ... [; BreakCommands]] 
```

## <a name="span-idddkcmdgowithexceptionnothandleddbgspanspan-idddkcmdgowithexceptionnothandleddbgspanparameters"></a><span id="ddk_cmd_go_with_exception_not_handled_dbg"></span><span id="DDK_CMD_GO_WITH_EXCEPTION_NOT_HANDLED_DBG"></span>パラメーター


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *スレッド*   
(ユーザー モードのみ)スレッドの実行を指定します。 このスレッドは、例外によって停止している必要があります。 構文の詳細については、次を参照してください。[スレッド構文](thread-syntax.md)します。

<span id="_______a______"></span><span id="_______A______"></span> **A**   
プロセッサのブレークポイントにするには、このコマンドによって作成されたすべてのブレークポイントの発生 (などによって作成された[ **ba**](ba--break-on-access-.md)) ソフトウェア ブレークポイントではなく (などによって作成された[ **bp** ](bp--bu--bm--set-breakpoint-.md)と**bm**)。 場合*BreakAddress*が指定されていない、ブレークポイントは作成されません、 **、** フラグが影響を与えません。

<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span> *StartAddress*   
実行を開始するアドレスを指定します。 これが指定されていない、デバッガーは実行をアドレス通過し、例外が発生します。 構文の詳細については、次を参照してください。[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)します。

<span id="_______BreakAddress______"></span><span id="_______breakaddress______"></span><span id="_______BREAKADDRESS______"></span> *BreakAddress*   
ブレークポイントを設定するアドレスを指定します。 場合*BreakAddress*指定すると、命令アドレスを指定する必要があります (つまり、アドレス必要命令の最初のバイトがあります)。 最大 10 個の区切りは、任意の順序でのアドレスを一度に 1 つ指定できます。 場合*BreakAddress*解決できないとして格納されて、[未解決ブレークポイント](unresolved-breakpoints---bu-breakpoints-.md)します。 構文の詳細については、次を参照してください。[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)します。

<span id="_______BreakCommands______"></span><span id="_______breakcommands______"></span><span id="_______BREAKCOMMANDS______"></span> *BreakCommands*   
ブレークポイントが指定されたときに自動的に実行する 1 つまたは複数のコマンドを指定します*BreakAddress*にヒットします。 *BreakCommands*パラメーターの先頭にセミコロンする必要があります。 複数*BreakAddress*値を指定すると、 *BreakCommands*それらすべてに適用されます。

**注**   、 *BreakCommands*パラメーターは、たとえば、別のブレークポイント コマンド内でまたは内 - 別のコマンドによって使用されるコマンド文字列内でこのコマンドを埋め込む場合にのみ使用します。除くまたはイベントの設定。 コマンド ラインで、セミコロンは、コマンドを終了し、直後に実行される、セミコロンの後に、追加のコマンドが表示、 **gn**または**gN**コマンドを実行します。

 

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

<a name="remarks"></a>注釈
-------

デバッガーがブレークポイントで停止していない場合**gn**と**gN**動作は同じです。 デバッガーがブレークポイントで停止している場合**gn**は機能しません。 このコマンドを実行する"N"を大文字に変換する必要があります。 これは、未処理のブレークポイントを続行することはほとんどありません賢明であるために、安全のためです。

使用する場合、 *BreakAddress*ブレークポイント、この新しいブレークポイントを設定するパラメーターは、現在のスレッドによってのみトリガーされます。 その場所でコードを実行する他のスレッドは停止します。

場合*スレッド*が指定されている、 **gn**コマンドを実行すると、指定されたスレッドのフリーズとフリーズ他のすべて。 たとえば場合、 **~ 123gn**、  **~ \#gn**、または **~ \*gn**コマンドを指定すると、指定されたスレッド固定されたでない他のすべてのユーザーが固定されているとします。

 

 






---
title: g (実行)
description: G コマンドでは、特定のプロセスまたはスレッドの実行を開始します。 BreakAddress に達したら、または別のイベントにより、デバッガーを停止するときに、プログラムの最後に実行を停止します。
ms.assetid: 9b6aac94-6c53-40c2-a8de-2ad106678c65
keywords:
- g (移動) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- g (Go)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 42b9d7cd181a6c508374323b2ad877886a06c0d7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357588"
---
# <a name="g-go"></a>g (実行)


**G**コマンドは、特定のプロセスまたはスレッドの実行を開始します。 プログラムの最後に実行を停止時に*BreakAddress*に達すると、または別のイベントがデバッガーを停止を発生する場合。

ユーザー モードの構文

```dbgcmd
[~Thread] g[a] [= StartAddress] [BreakAddress ... [; BreakCommands]]
```

カーネル モードの構文

```dbgcmd
g[a] [= StartAddress] [BreakAddress ... [; BreakCommands]] 
```

## <a name="span-idddkcmdgodbgspanspan-idddkcmdgodbgspanparameters"></a><span id="ddk_cmd_go_dbg"></span><span id="DDK_CMD_GO_DBG"></span>パラメーター


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *スレッド*   
(ユーザー モードのみ)スレッドの実行を指定します。 構文の詳細については、次を参照してください。[スレッド構文](thread-syntax.md)します。

<span id="_______a______"></span><span id="_______A______"></span> **A**   
プロセッサのブレークポイントにするには、このコマンドによって作成されたすべてのブレークポイントの発生 (などによって作成された[ **ba**](ba--break-on-access-.md)) ソフトウェア ブレークポイントではなく (などによって作成された[ **bp** ](bp--bu--bm--set-breakpoint-.md)と**bm**)。 場合*BreakAddress*が指定されていない、ブレークポイントは作成されません、 **、** フラグが影響を与えません。

<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span> *StartAddress*   
実行を開始するアドレスを指定します。 これが指定されていない場合、デバッガーは実行を命令ポインターの現在の値で指定されたアドレスに渡します。 構文の詳細については、次を参照してください。[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)します。

<span id="_______BreakAddress______"></span><span id="_______breakaddress______"></span><span id="_______BREAKADDRESS______"></span> *BreakAddress*   
ブレークポイントを設定するアドレスを指定します。 場合*BreakAddress*指定すると、命令アドレスを指定する必要があります (つまり、アドレス必要命令の最初のバイトがあります)。 最大 10 個の区切りは、任意の順序でのアドレスを一度に 1 つ指定できます。 場合*BreakAddress*解決できないとして格納されて、[未解決ブレークポイント](unresolved-breakpoints---bu-breakpoints-.md)します。 構文の詳細については、次を参照してください。[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)します。

<span id="_______BreakCommands______"></span><span id="_______breakcommands______"></span><span id="_______BREAKCOMMANDS______"></span> *BreakCommands*   
ブレークポイントが指定されたときに自動的に実行する 1 つまたは複数のコマンドを指定します*BreakAddress*にヒットします。 *BreakCommands*パラメーターの先頭にセミコロンする必要があります。 複数*BreakAddress*値を指定すると、 *BreakCommands*それらすべてに適用されます。

**注**   、 *BreakCommands*パラメーターは、たとえば、別のブレークポイント コマンド内でまたは内 - 別のコマンドによって使用されるコマンド文字列内でこのコマンドを埋め込む場合にのみ使用します。除くまたはイベントの設定。 セミコロンを終了する、コマンド ラインで、 **g**後すぐに実行される、セミコロンの後、コマンド、および追加のコマンドが表示されている、 **g**コマンドを実行します。

 

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

場合*スレッド*が指定されている、 **g**コマンドを実行すると、指定されたスレッドのフリーズとフリーズ他のすべて。 たとえば場合、 **~ 123 g**、  **~ \#g**、または **~ \*g**コマンドを指定すると、指定されたスレッドは、固定されていない他のすべてのユーザーが固定されているとします。

 

 






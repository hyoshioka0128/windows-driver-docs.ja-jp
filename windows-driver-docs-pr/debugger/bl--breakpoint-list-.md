---
title: bl (ブレークポイントの一覧)
description: '[Bl] コマンドを実行すると、既存のブレークポイントに関する情報が表示されます。'
ms.assetid: 3e7c31d4-5c76-4609-91be-c6b0fc1cb292
keywords:
- bl (ブレークポイント一覧) Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- bl (Breakpoint List)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: dd69b601b4c4b80202c8c1a900767f53c4ffe51f
ms.sourcegitcommit: 9dbb1ef59c3e797bfc3cc418dd2b9bdc44940d14
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71284922"
---
# <a name="bl-breakpoint-list"></a>bl (ブレークポイントの一覧)


**[Bl]** コマンドを実行すると、既存のブレークポイントに関する情報が表示されます。

```dbgcmd
bl [/L] [Breakpoints]
```

## <a name="span-idddk_cmd_breakpoint_list_dbgspanspan-idddk_cmd_breakpoint_list_dbgspanparameters"></a><span id="ddk_cmd_breakpoint_list_dbg"></span><span id="DDK_CMD_BREAKPOINT_LIST_DBG"></span>パラメータ


<span id="________L______"></span><span id="________l______"></span> **/L**   
ソースファイルと行番号を表示するのではなく、常に**bl**にブレークポイントアドレスを表示します。

<span id="_______Breakpoints______"></span><span id="_______breakpoints______"></span><span id="_______BREAKPOINTS______"></span>*ブレークポイント*   
一覧表示するブレークポイントの ID 番号を指定します。 *ブレークポイント*を省略した場合、デバッガーはすべてのブレークポイントを一覧表示します。 任意の数のブレークポイントを指定できます。 複数の Id は、スペースまたはコンマで区切る必要があります。 ブレークポイント Id の範囲を指定するには、ハイフン (-) を使用します。 すべてのブレークポイントを示すには、アスタリスク (\*) を使用できます。 ID に[数値式](numerical-expression-syntax.md)を使用する場合は、角かっこ (\[\]) で囲みます。 [ワイルドカード文字を含む文字列](string-wildcard-syntax.md)をブレークポイントのシンボリック名と一致させるには、引用符で囲みます (\"\")。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>Environment

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Modes</strong></p></td>
<td align="left"><p>ユーザーモード、カーネルモード</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブデバッグのみ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Platforms</strong></p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ブレークポイントの使用方法の詳細と例、ブレークポイントを制御するその他のブレークポイントコマンドと方法、カーネルデバッガーからユーザー空間にブレークポイントを設定する方法の詳細については、「[ブレークポイントの使用](using-breakpoints.md)」を参照してください。 条件付きブレークポイントの詳細については、「[条件付きブレークポイントの設定](setting-a-conditional-breakpoint.md)」を参照してください。

<a name="remarks"></a>注釈
-------

各ブレークポイントについて、次の情報が表示されます。

- ブレークポイント ID。 この ID は、後のコマンドでブレークポイントを参照するために使用できる10進数です。

- ブレークポイントの状態。 状態は、 **e** (有効) または**d** (無効) のいずれかになります。

- (未解決のブレークポイントのみ)ブレークポイントが未解決の場合、文字 "u" が表示されます。 つまり、ブレークポイントは、現在読み込まれているモジュール内のシンボリック参照と一致しません。 これらのブレークポイントの詳細については、「[未解決のブレークポイント (Bu ブレークポイント)](unresolved-breakpoints---bu-breakpoints-.md)」を参照してください。

- ブレークポイントの位置を構成する仮想アドレスまたはシンボリック式。 ソース行番号の読み込みを有効にした場合、 **bl**コマンドは、アドレスのオフセットではなく、ファイルと行番号の情報を表示します。 ブレークポイントが未解決の場合、アドレスはここでは省略され、リストの末尾に表示されます。

- (データブレークポイントのみ)データブレークポイントの種類とサイズの情報が表示されます。 型には、 **e** (実行)、 **r** (読み取り/書き込み)、 **w** (書き込み)、 **i** (入力/出力) を指定できます。 これらの型の後には、ブロックのサイズがバイト単位で含まれます。 これらのブレークポイントの詳細については、「[プロセッサのブレークポイント (Ba ブレークポイント)](processor-breakpoints---ba-breakpoints-.md)」を参照してください。

- ブレークポイントがアクティブになるまで保持されるパスの数。その後に、かっこで囲まれた最初のパス数が続きます。 この種類のブレークポイントの詳細については、「 [**bp、bu、bm (ブレークポイントの設定)** ](bp--bu--bm--set-breakpoint-.md)」の*パス*パラメーターの説明を参照してください。

- 関連付けられたプロセスとスレッド。 Thread が3つのアスタリスク (\*\*\*) として指定されている場合、このブレークポイントはスレッド固有のブレークポイントではありません。

- ブレークポイントアドレスに対応する、オフセットを持つモジュールと関数。 ブレークポイントが未解決の場合は、代わりにブレークポイントのアドレスがかっこ内に表示されます。 ブレークポイントが有効なアドレスに設定されているにもかかわらず、シンボル情報がない場合、このフィールドは空白になります。

- このブレークポイントにヒットしたときに自動的に実行されるコマンドです。 このコマンドは引用符で囲まれて表示されます。

既存のブレークポイントの設定に使用されたコマンドがわからない場合は、 [ **. bpcmds (ブレークポイントコマンドを表示)** ](-bpcmds--display-breakpoint-commands-.md)を使用して、すべてのブレークポイントとそれらの作成に使用したコマンドを一覧表示します。

次の例は、 **bl**コマンドの出力を示しています。

例

```dbgcmd
0:000> bl
 0 e 010049e0     0001 (0001)  0:**** stst!main
```

この出力には、次の情報が含まれています。

- ブレークポイント ID は**0**です。

- ブレークポイントの状態は**e** (有効) です。

- ブレークポイントが未解決ではありません (出力に**u**がありません)。

- ブレークポイントの仮想アドレスは、 **010049e0**です。

- ブレークポイントは、コードを最初に通過したときにアクティブになり、デバッガーでコードがまだ実行されていません。 この情報は、最初のパスカウンターで、"残りの時間" カウンターに 1 (**0001**)、値が 1 (**0001)** で示されます。

- このブレークポイントは、スレッド固有のブレークポイントではありません (\*\*\*)。

- ブレークポイントは、 **stst**モジュールの**main**に設定されます。

 

 






---
title: bl (ブレークポイントの一覧)
description: Bl コマンドは、既存のブレークポイント情報を一覧表示します。
ms.assetid: 3e7c31d4-5c76-4609-91be-c6b0fc1cb292
keywords:
- bl (ブレークポイントの一覧) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- bl (Breakpoint List)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6776d96d5fd9690adcb0e835ca991258e2505b2f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574045"
---
# <a name="bl-breakpoint-list"></a>bl (ブレークポイントの一覧)


**Bl**コマンドは、既存のブレークポイント情報を一覧表示します。

```dbgcmd
bl [/L] [Breakpoints]
```

## <a name="span-idddkcmdbreakpointlistdbgspanspan-idddkcmdbreakpointlistdbgspanparameters"></a><span id="ddk_cmd_breakpoint_list_dbg"></span><span id="DDK_CMD_BREAKPOINT_LIST_DBG"></span>パラメーター


<span id="________L______"></span><span id="________l______"></span> **/L**   
強制**bl**を常にソース ファイルと行の数を表示するのではなくブレークポイントのアドレスを表示します。

<span id="_______Breakpoints______"></span><span id="_______breakpoints______"></span><span id="_______BREAKPOINTS______"></span> *ブレークポイント*   
一覧表示するブレークポイントの ID 番号を指定します。 省略した場合*ブレークポイント*デバッガーは、すべてのブレークポイントを一覧表示します。 ブレークポイントの任意の数を指定することができます。 スペースまたはコンマで複数の Id を区切る必要があります。 ハイフンを使用してブレークポイント Id の範囲を指定することができます (-)。 アスタリスクを使用することができます (**\\* * *) をすべてのブレークポイントを示します。使用する場合、[数値式](numerical-expression-syntax.md)id、角かっこで囲む (*<em>\[\]</em><em>)。使用する場合、[ワイルドカード文字を含む文字列](string-wildcard-syntax.md)ブレークポイントのシンボリック名を一致するように引用符で囲みます (**""</em>*  )。

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
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細とブレークポイント、他のブレークポイント コマンドや、ブレークポイントを制御する方法を使用する方法と、カーネル デバッガーからのユーザー領域でブレークポイントを設定する方法の例については、[を使用してブレークポイント](using-breakpoints.md)を参照してください。 条件付きブレークポイントの詳細については、[、条件付きブレークポイント](setting-a-conditional-breakpoint.md)を参照してください。

<a name="remarks"></a>コメント
-------

各ブレークポイントでは、コマンドは、次の情報が表示されます。

- ブレークポイントの id。 この ID は、後のコマンドでブレークポイントを指すために使用できる 10 進数です。

- ブレークポイントの状態です。 状態は、 **e** (有効) または**d** (無効)。

- (未解決のブレークポイントのみ)ブレークポイントが解決されない場合は、文字"u"が表示されます。 つまり、ブレークポイントでは、現在読み込まれているモジュールのシンボリック参照は一致しません。 これらのブレークポイントの詳細については、[未解決ブレークポイント (bu ブレークポイント)](unresolved-breakpoints---bu-breakpoints-.md)を参照してください。

- 仮想アドレスまたはブレークポイントの場所を構成するシンボル定義の式。 ソース行の番号の読み込みを有効にした場合、 **bl**コマンドがアドレス オフセットではなく、ファイルと行番号情報を表示します。 アドレスがここでを省略して、一覧の最後に表示、ブレークポイントが解決されない場合は、代わりにします。

- (データ ブレークポイントのみ)データ ブレークポイントの種類とサイズの情報が表示されます。 指定できる型は**e** (execute)、 **r** (読み取り/書き込み) **w** (書き込み)、または**は**(入力/出力)。 これらの型は、(バイト単位)、ブロックのサイズに従います。 これらのブレークポイントの詳細については、[プロセッサ ブレークポイント (ba ブレークポイント)](processor-breakpoints---ba-breakpoints-.md)を参照してください。

- ブレークポイントがアクティブになるまでのパス数後にかっこで囲まれたパスの初期数。 この種のブレークポイントの詳細については、の説明を参照して、*パス*パラメーター [ **bp、bu、bm (ブレークポイントの設定)**](bp--bu--bm--set-breakpoint-.md)します。

- 関連付けられたプロセスとスレッド。 スレッドは 3 つのアスタリスクとして指定した場合 ("* *\*\*\\* * *")、このブレークポイントは、スレッド固有のブレークポイントではありません。

- モジュールとのオフセットでの関数は、ブレークポイントのアドレスに対応します。 ブレークポイントが解決されない場合、ブレークポイントのアドレスが表示されます代わりに、かっこで囲まれました。 ブレークポイントが有効なアドレスの設定、シンボル情報が不足している場合は、このフィールドは空白です。

- このブレークポイントにヒットしたときに自動的に実行されるコマンドです。 このコマンドは、引用符で表示されます。

既存のブレークポイントの設定を使用してどのようなコマンドを使用しましたが不明の場合[ **.bpcmds (ブレークポイント コマンドが表示)** ](-bpcmds--display-breakpoint-commands-.md)を作成するために使用されたコマンドとすべてのブレークポイントを一覧表示します。

次の例の出力を示しています、 **bl**コマンド。

例

```dbgcmd
0:000> bl
 0 e 010049e0     0001 (0001)  0:**** stst!main
```

この出力には、次の情報が含まれています。

- ID はブレークポイント**0**します。

- ブレークポイントの状態が**e** (有効)。

- ブレークポイントが未解決 (があるない**u**出力に)。

- ブレークポイントの仮想アドレス**010049e0**します。

- ブレークポイントがコードを最初のパス上でアクティブにして、コードがデバッガーで実行されていません。 この情報は、値 1 で示されます (**0001**)「残り渡します」カウンターと、値 1 (**(0001)**)、初期のカウンターを渡します。

- このブレークポイントは、スレッド固有のブレークポイントではありません (* *\*\*\*\\* * *)。

- ブレークポイントが設定**メイン**で、 **stst**モジュール。

 

 






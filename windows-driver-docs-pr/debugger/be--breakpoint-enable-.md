---
title: be (ブレークポイントの有効化)
description: コマンドの復元を以前に無効にする 1 つまたは複数のブレークポイントにあります。
ms.assetid: 110fe8b0-0bc7-49ce-9c66-326d5897c0ca
keywords:
- (ブレークポイントを有効にする) Windows のデバッグをします。
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- be (Breakpoint Enable)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 17f0ab8fcf782655dfee280abbe77a688f00026b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579802"
---
# <a name="be-breakpoint-enable"></a>be (ブレークポイントの有効化)


**する**コマンドは、以前に無効にする 1 つまたは複数のブレークポイントを復元します。

```dbgcmd
be Breakpoints 
```

## <a name="span-idddkcmdbreakpointenabledbgspanspan-idddkcmdbreakpointenabledbgspanparameters"></a><span id="ddk_cmd_breakpoint_enable_dbg"></span><span id="DDK_CMD_BREAKPOINT_ENABLE_DBG"></span>パラメーター


<span id="_______Breakpoints______"></span><span id="_______breakpoints______"></span><span id="_______BREAKPOINTS______"></span> *ブレークポイント*   
有効にするブレークポイントの ID 番号を指定します。 ブレークポイントの任意の数を指定することができます。 スペースまたはコンマで複数の Id を区切る必要があります。 ハイフンを使用してブレークポイント Id の範囲を指定することができます (-)。 アスタリスクを使用することができます (**\\* * *) をすべてのブレークポイントを示します。使用する場合、[数値式](numerical-expression-syntax.md)id、角かっこで囲む (*<em>\[\]</em><em>)。使用する場合、[ワイルドカード文字を含む文字列](string-wildcard-syntax.md)ブレークポイントのシンボリック名を一致するように引用符で囲みます (**""</em>*  )。

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

詳細とブレークポイント、他のブレークポイント コマンドや、ブレークポイントを制御する方法を使用する方法と、カーネル デバッガーからのユーザー領域でブレークポイントを設定する方法の例については、次を参照してください。[を使用してブレークポイント](using-breakpoints.md)します。 条件付きブレークポイントの詳細については、次を参照してください。 [、条件付きブレークポイント](setting-a-conditional-breakpoint.md)します。

<a name="remarks"></a>コメント
-------

使用して、 [ **bl (ブレークポイントの一覧)** ](bl--breakpoint-list-.md)既存のすべてのブレークポイント、ID 番号、およびそれらの状態を一覧表示するコマンド。

使用して、 [ **.bpcmds (ブレークポイント コマンドが表示)** ](-bpcmds--display-breakpoint-commands-.md)既存のすべてのブレークポイント、ID 番号、およびその作成に使用されたコマンドを一覧表示するコマンド。

 

 






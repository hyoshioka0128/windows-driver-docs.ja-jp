---
title: bc (ブレークポイントのクリア)
description: Bc コマンドから完全に削除したブレークポイントを設定するシステム。
ms.assetid: 7bff5261-179f-4fd6-b427-de74e830a8c7
keywords:
- bc (ブレークポイント クリア) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- bc (Breakpoint Clear)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5601e6bd150011861b40d7d80aab98650063f000
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357022"
---
# <a name="bc-breakpoint-clear"></a>bc (ブレークポイントのクリア)


**Bc**削除は、システムからブレークポイントを設定する前に完全にコマンドします。

```dbgcmd
bc Breakpoints 
```

## <a name="span-idddkcmdbreakpointcleardbgspanspan-idddkcmdbreakpointcleardbgspanparameters"></a><span id="ddk_cmd_breakpoint_clear_dbg"></span><span id="DDK_CMD_BREAKPOINT_CLEAR_DBG"></span>パラメーター


<span id="_______Breakpoints______"></span><span id="_______breakpoints______"></span><span id="_______BREAKPOINTS______"></span> *ブレークポイント*   
削除するブレークポイントの ID 番号を指定します。 ブレークポイントの任意の数を指定することができます。 スペースまたはコンマで複数の Id を区切る必要があります。 ハイフンを使用してブレークポイント Id の範囲を指定することができます (-)。 アスタリスクを使用することができます (\*) をすべてのブレークポイントを示します。 使用する場合、[数値式](numerical-expression-syntax.md)id、角かっこで囲む (\[\])。 使用する場合、[ワイルドカード文字を含む文字列](string-wildcard-syntax.md)ブレークポイントのシンボリック名を一致するように引用符で囲みます ("")。

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

ブレークポイント、他のブレークポイント コマンドや、ブレークポイントを制御する方法を使用する方法と、カーネル デバッガーからのユーザー領域でブレークポイントを設定する方法の詳細については、次を参照してください。[を使用してブレークポイント](using-breakpoints.md)します。 条件付きブレークポイントの詳細については、次を参照してください。 [、条件付きブレークポイント](setting-a-conditional-breakpoint.md)します。

<a name="remarks"></a>コメント
-------

使用して、 [ **bl (ブレークポイントの一覧)** ](bl--breakpoint-list-.md)既存のすべてのブレークポイント、ID 番号、およびそれらの状態を一覧表示するコマンド。

使用して、 [ **.bpcmds (ブレークポイント コマンドが表示)** ](-bpcmds--display-breakpoint-commands-.md)既存のすべてのブレークポイント、ID 番号、およびその作成に使用されたコマンドを一覧表示するコマンド。

 

 






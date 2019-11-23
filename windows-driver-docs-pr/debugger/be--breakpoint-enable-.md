---
title: be (ブレークポイントの有効化)
description: Be コマンドは、以前に無効になっていた1つ以上のブレークポイントを復元します。
ms.assetid: 110fe8b0-0bc7-49ce-9c66-326d5897c0ca
keywords:
- be (ブレークポイントを有効にする) Windows デバッグ
ms.date: 09/18/2019
topic_type:
- apiref
api_name:
- be (Breakpoint Enable)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8aeea0aecdd9a591ec5f48c26715ef9789823211
ms.sourcegitcommit: 3246a166d5454c68f77c15267f3f0b347359f505
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/19/2019
ms.locfileid: "71108101"
---
# <a name="be-breakpoint-enable"></a>be (ブレークポイントの有効化)

**Be**コマンドは、以前に無効になっていた1つ以上のブレークポイントを復元します。

```dbgcmd
be Breakpoints 
```

## <a name="span-idddk_cmd_breakpoint_enable_dbgspanspan-idddk_cmd_breakpoint_enable_dbgspanparameters"></a><span id="ddk_cmd_breakpoint_enable_dbg"></span><span id="DDK_CMD_BREAKPOINT_ENABLE_DBG"></span>パラメータ

<span id="_______Breakpoints______"></span><span id="_______breakpoints______"></span><span id="_______BREAKPOINTS______"></span>*ブレークポイント*   
有効にするブレークポイントの ID 番号を指定します。 任意の数のブレークポイントを指定できます。 複数の Id は、スペースまたはコンマで区切る必要があります。 ブレークポイント Id の範囲を指定するには、ハイフン (-) を使用します。 すべてのブレークポイントを示すには、アスタリスク (\*) を使用できます。 ID に[数値式](numerical-expression-syntax.md)を使用する場合は、角かっこ (\[ \]) で囲みます。 [ワイルドカード文字を含む文字列](string-wildcard-syntax.md)をブレークポイントのシンボル名と一致させるには、引用符 ("") で囲みます。

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

[ [**Bl (ブレークポイントの一覧)** ](bl--breakpoint-list-.md) ] コマンドを使用すると、既存のすべてのブレークポイント、その ID 番号、およびそれらの状態を一覧表示できます。

[**Bpcmds (ブレークポイントコマンドの表示)** ](-bpcmds--display-breakpoint-commands-.md)コマンドを使用して、既存のすべてのブレークポイント、その ID 番号、およびそれらの作成に使用されたコマンドを一覧表示します。

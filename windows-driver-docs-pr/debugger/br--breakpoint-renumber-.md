---
title: br (ブレークポイント番号)
description: Br コマンドでは、1 つ以上のブレークポイントを更新します。
ms.assetid: 1b41eb37-3375-4203-bbf5-f55869383db8
keywords:
- br (ブレークポイント番号) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- br (Breakpoint Renumber)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c53c99d28d259391fd85b44b745f3b069673a013
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554020"
---
# <a name="br-breakpoint-renumber"></a>br (ブレークポイント番号)


**Br**コマンドは、1 つ以上のブレークポイントを更新します。

```dbgcmd
br OldID NewID [OldID2 NewID2 ...] 
```

## <a name="span-idddkcmdbreakpointrenumberdbgspanspan-idddkcmdbreakpointrenumberdbgspanparameters"></a><span id="ddk_cmd_breakpoint_renumber_dbg"></span><span id="DDK_CMD_BREAKPOINT_RENUMBER_DBG"></span>パラメーター


<span id="_______OldID______"></span><span id="_______oldid______"></span><span id="_______OLDID______"></span> *OldID*   
ブレークポイントの現在の ID 番号を指定します。

<span id="_______NewID______"></span><span id="_______newid______"></span><span id="_______NEWID______"></span> *NewID*   
ブレークポイントの ID になる新しい番号を指定します。

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

<a name="remarks"></a>注釈
-------

使用することができます、 **br**を同時に、ブレークポイントの任意の数を再設定するコマンド。 各ブレークポイントでは、へのパラメーターとして、古い ID とその順序で、新しい ID を一覧**br**します。

ブレークポイントの id は既にかどうか*NewID*のコマンドは失敗し、エラー メッセージが表示されます。

 

 






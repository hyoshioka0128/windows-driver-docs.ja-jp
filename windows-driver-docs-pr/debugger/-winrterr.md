---
title: winrterr
description: Winrterr モードの Windows ランタイム エラーを報告するデバッガーを設定します。
ms.assetid: 72E3EF7A-6055-405F-9E24-C9B81C07B8A7
keywords:
- Windows デバッグ winrterr
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- winrterr
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c9ad1fceba52fcf3c86a75e865cc605ed8649d3e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580590"
---
# <a name="winrterr"></a>!winrterr


**! Winrterr**モードの Windows ランタイム エラーを報告するデバッガーを設定します。

```dbgcmd
!winrterr Mode
!winrterr
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="Mode"></span><span id="mode"></span><span id="MODE"></span>*モード*  
次の表に、可能な値*モード*します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="report"></span><span id="REPORT"></span>レポート</p></td>
<td align="left"><p>Windows ランタイム エラーが発生したときに、デバッガーが実行 contunues でエラーと関連するテキストが表示されます。 これが既定の設定です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="break"></span><span id="BREAK"></span>break</p></td>
<td align="left"><p>Windows ランタイム エラーが発生したときにエラーと関連するテキストは、デバッガーで表示され、実行が停止します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="quiet"></span><span id="QUIET"></span>通知の停止</p></td>
<td align="left"><p>Windows ランタイム エラーが発生した、デバッガーでは何も表示され、実行が続行されます。</p></td>
</tr>
</tbody>
</table>

 

場合*モード*を省略すると、 **! winrterr**現在のレポート モードを表示します。 デバッガーは、Windows ランタイム エラーの結果として分かれているが場合のエラー メッセージと関連付けられたテキストも表示されます。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[Windows ランタイムのデバッガー コマンド](windows-runtime-debugger-commands.md)

[**!hstring**](-hstring.md)

[**!hstring2**](-hstring2.md)

 

 







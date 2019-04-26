---
title: .scroll_prefs (ソース スクロール設定の制御)
description: .Scroll_prefs コマンドでは、行にスクロールする場合、ソース ウィンドウで、ソースの位置を制御します。
ms.assetid: 08978751-c4b7-491a-9e1f-de21d74a10a8
keywords:
- .scroll_prefs (ソースのコントロールにスクロールの基本設定) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .scroll_prefs (Control Source Scrolling Preferences)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 22361c782981011a8fc5a36235973049077594e8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339836"
---
# <a name="scrollprefs-control-source-scrolling-preferences"></a>.scroll\_環境設定 (コントロール ソース スクロールの設定)


**.Scroll\_prefs**コマンドが行にスクロールする場合、ソース ウィンドウで、ソースの位置を制御します。

```dbgcmd
.scroll_prefs Before After 
.scroll_prefs 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Before______"></span><span id="_______before______"></span><span id="_______BEFORE______"></span> *以前は*   
ソース ウィンドウ内をスクロールする行を表示するか前に、ソース行の数を指定します。

<span id="_______After______"></span><span id="_______after______"></span><span id="_______AFTER______"></span> *後*   
ソース ウィンドウ内をスクロールする行を表示するか後に、ソース行の数を指定します。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

このコマンドは、WinDbg でのみ使用でき、スクリプト ファイルでは使用できません。

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
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

このコマンドは、パラメーターなしの使用は、現在のソース スクロールの設定が表示されます。

 

 






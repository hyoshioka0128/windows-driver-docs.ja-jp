---
title: logexts.logm
description: Logexts.logm 拡張機能を作成またはモジュールの一覧またはモジュールの除外一覧が表示されます。
ms.assetid: 1037ba25-ffa6-4edd-99fd-bd0e249f4b37
keywords:
- デバッグ logexts.logm Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- logexts.logm
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5b0d75d3eda156570b2ddfec2a11544465382ca8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535575"
---
# <a name="logextslogm"></a>!logexts.logm


**! Logexts.logm**拡張機能を作成またはモジュールの一覧またはモジュールの除外一覧が表示されます。

```dbgcmd
!logexts.logm i Modules 
!logexts.logm x Modules 
!logexts.logm 
```

## <a name="span-idddklogextslogmdbgspanspan-idddklogextslogmdbgspanparameters"></a><span id="ddk__logexts_logm_dbg"></span><span id="DDK__LOGEXTS_LOGM_DBG"></span>パラメーター


<span id="_______i______"></span><span id="_______I______"></span> **i**   
モジュールの一覧を使用するロガーをによりします。 指定した構成することが、*モジュール*します。

<span id="_______x______"></span><span id="_______X______"></span> **x**   
モジュールの除外リストを使用するロガーをによりします。 Logexts.dll、kernel32.dll、および指定したので構成されているが*モジュール*します。

<span id="_______Modules______"></span><span id="_______modules______"></span><span id="_______MODULES______"></span> *モジュール*   
含まれるまたは除外するモジュールを指定します。 この一覧では累積されます。このコマンドの使用では、まったく新しいリストを作成します。 複数のモジュールが一覧される場合は、空白で区切ります。 アスタリスク (\*) をすべてのモジュールを示すために使用できます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>logexts.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>logexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、[Logger と LogViewer](logger-and-logviewer.md)を参照してください。

<a name="remarks"></a>注釈
-------

パラメーターなしで、 **! logexts.logm**拡張機能は、現在の信頼のリストまたは除外の一覧が表示されます。

拡張機能 **! logexts.logm x \\** * と **! logexts.logm は**は同等です: 完全に空の一覧で結果します。

拡張機能 **! logexts.logm は\\** * と **! logexts.logm x**は同等です: Logexts.dll と kernel32.dll のみを含む除外リストの結果します。 これら 2 つのモジュールはロガーはログ自体に許可されていませんので、常に除外します。

例をいくつか紹介します。

```dbgcmd
0:001> !logm
Excluded modules:
  LOGEXTS.DLL      [mandatory]
  KERNEL32.DLL     [mandatory]
  USER32.DLL
  GDI32.DLL
  ADVAPI32.DLL

0:001> !logm x winmine.exe
Excluded modules:
  Logexts.dll      [mandatory]
  kernel32.dll     [mandatory]
  winmine.exe

0:001> !logm x user32.dll gdi32.dll
Excluded modules:
  Logexts.dll      [mandatory]
  kernel32.dll     [mandatory]
  user32.dll
  gdi32.dll

0:001> !logm i winmine.exe mymodule2.dll
Included modules:
  winmine.exe
  mymodule2.dll
```

 

 






---
title: chksym
description: Chksym 拡張機能は、モジュールに対してシンボル ファイルの有効性をテストします。
ms.assetid: 52ea75cb-44a2-4c84-a3af-b3fc027348f4
keywords:
- Windows デバッグ chksym
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- chksym
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5f8f6fce41e4fb8e70116fd1c15e38c70d512317
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535705"
---
# <a name="chksym"></a>! chksym


**! Chksym**拡張機能は、モジュールに対してシンボル ファイルの有効性をテストします。

```dbgsyntax
    !chksym Module [Symbol] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Module______"></span><span id="_______module______"></span><span id="_______MODULE______"></span> *モジュール*   
モジュールの名前またはベース アドレスの名前を指定します。

<span id="_______Symbol______"></span><span id="_______symbol______"></span><span id="_______SYMBOL______"></span> *シンボル*   
シンボル ファイルの名前を指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>利用不可</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP</strong></p></td>
<td align="left"><p>利用不可</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Windows Vista 以降</strong></p></td>
<td align="left"><p>Dbghelp.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

提出済みのシンボルを指定しない場合は、読み込まれたシンボルがテストされます。 それ以外の場合、.pdb ファイルまたは .dbg のシンボル ファイルのパスを指定する場合は、読み込まれたシンボルが読み込まれたモジュールに対してテストされます。

 

 






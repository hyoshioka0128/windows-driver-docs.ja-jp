---
title: lmi
description: Lmi 拡張機能では、モジュールに関する詳細な情報が表示されます。
ms.assetid: 00438edf-618a-401e-818f-24add7861487
keywords:
- Windows デバッグ lmi
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- lmi
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 53e387a16ef145a63b919fc367629643747f96de
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531540"
---
# <a name="lmi"></a>!lmi


**! Lmi**拡張機能には、モジュールに関する情報が表示されます。

```dbgcmd
!lmi Module
```

## <a name="span-idddklmidbgspanspan-idddklmidbgspanparameters"></a><span id="ddk__lmi_dbg"></span><span id="DDK__LMI_DBG"></span>パラメーター


<span id="_______Module______"></span><span id="_______module______"></span><span id="_______MODULE______"></span> *モジュール*   
読み込まれたモジュールの場合は、名前またはベース アドレスのいずれかを指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Dbghelp.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Dbghelp.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

使用してモジュールのアドレスを特定することができます、 [ **lm (読み込まれたモジュールの一覧)** ](lm--list-loaded-modules-.md)コマンド。

**! Lmi**拡張機能は、モジュールのヘッダーを分析し、その情報の書式設定された概要が表示されます。 モジュール ヘッダーをページ アウト、エラー メッセージが表示されます。 ヘッダー情報の詳細の表示を表示するには、使用、 [ **! dh** ](-dh.md)拡張機能コマンド。

このコマンドは、それぞれ別のタイトルが、フィールドの数を示します。 これらのタイトルの一部で、特定の意味があります。

-   **イメージ名**フィールドには、拡張機能を含め、実行可能ファイルの名前が表示されます。 通常、完全なパスが含まれるカーネル モードではなくユーザー モードにします。

-   **モジュール**フィールド、*モジュール名*します。 これは、通常、拡張子を除いたファイル名だけです。 いくつかの場合、モジュール名はファイル名から大幅に異なります。

-   **記号の型**フィールドには、このモジュールのシンボルを読み込むため、デバッガーの試行に関する情報が表示されます。 さまざまな状態の値の詳細については、次を参照してください。[シンボルの状態の省略形](symbol-status-abbreviations.md)します。 シンボルが読み込まれている場合、シンボル ファイル名はこれに従います。

-   モジュールの最初のアドレスを示した**ベース アドレス**します。 モジュールのサイズを示す**サイズ**します。 したがって場合、**ベース アドレス**"faab4000"と**サイズ**「2000」0xFAAB5FFF、包括的に 0xFAAB4000 からモジュールを拡張します。

以下に例を示します。

```dbgcmd
0:000> lm 
start    end        module name
00400000 0042d000   Prymes     C (pdb symbols)              Prymes.pdb
77e80000 77f35000   KERNEL32     (export symbols)           C:\WINNT\system32\KERNEL32.dll
77f80000 77ffb000   ntdll        (export symbols)           ntdll.dll

0:000> !lmi 00400000
Loaded Module Info: [00400000] 
         Module: Prymes
   Base Address: 00400000
     Image Name: Prymes.exe
   Machine Type: 332 (I386)
     Time Stamp: 3c76c346 Fri Feb 22 14:16:38 2002
           Size: 2d000
       CheckSum: 0
Characteristics: 230e stripped 
Debug Data Dirs: Type Size     VA  Pointer
                 MISC  110,     0,   77a00 [Data not mapped]
    Symbol Type: EXPORT   - PDB not found
    Load Report: export symbols
```

表示される省略形の詳細については、**特性**行のこの例では、次を参照してください。[シンボルの状態の省略形](symbol-status-abbreviations.md)します。

 

 






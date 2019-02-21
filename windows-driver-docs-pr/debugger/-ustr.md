---
title: ustr
description: Ustr 拡張機能には、UNICODE_STRING 構造が表示されます。
ms.assetid: 17b84bf0-5a5b-47a5-893b-fdc58ca2afc3
keywords:
- 文字列
- UNICODE_STRING 構造体
- Windows デバッグ ustr
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ustr
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3edcbc657def7230ee0b7ca0488c542b227a0751
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559073"
---
# <a name="ustr"></a>! ustr


**! Ustr**拡張機能の表示、UNICODE\_文字列構造体。

```dbgcmd
!ustr Address
```

## <a name="span-idddkustrdbgspanspan-idddkustrdbgspanparameters"></a><span id="ddk__ustr_dbg"></span><span id="DDK__USTR_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
UNICODE の 16 進数のアドレスを指定します\_文字列構造体。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

UNICODE の詳細については\_構造体の文字列を Microsoft Windows SDK のマニュアルを参照してください。

<a name="remarks"></a>注釈
-------

次の構造で定義されている Unicode 文字列には 16 ビット文字の文字列がカウントされます。

```cpp
typedef struct _UNICODE_STRING {
    USHORT Length;
    USHORT MaximumLength;
    PWSTR  Buffer;
} UNICODE_STRING;
```

文字列が null で終わる場合**長さ**末尾の null は含まれません。

Win32 のほとんどの文字の文字列引数は、実際の処理が行われる前に、Unicode 文字列に変換されます。

 

 






---
title: str
description: Str 拡張機能では、ANSI_STRING または OEM_STRING 構造体が表示されます。
ms.assetid: 5ebb29d4-5d77-475b-ace5-8bc8a4299320
keywords:
- 文字列
- ANSI_STRING 構造体
- str Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- str
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1840a0ec00d167fdf87d9d02031152738417176c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528883"
---
# <a name="str"></a>! str


**! Str**拡張機能の表示、ANSI\_文字列または OEM\_文字列構造体。

```dbgcmd
!str Address
```

## <a name="span-idddkstrdbgspanspan-idddkstrdbgspanparameters"></a><span id="ddk__str_dbg"></span><span id="DDK__STR_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
ANSI の 16 進数のアドレスを指定します\_文字列または OEM\_文字列構造体。

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

ANSI の詳細については\_構造体の文字列を Microsoft Windows SDK のマニュアルを参照してください。

<a name="remarks"></a>注釈
-------

ANSI 文字列は、次の構造で定義されている 8 ビット文字の文字列をカウントします。

```cpp
typedef struct _STRING {
    USHORT Length;
    USHORT MaximumLength;
    PCHAR Buffer;
} STRING;
typedef STRING ANSI_STRING;
typedef STRING OEM_STRING;
```

文字列が null で終わる場合**長さ**末尾の null は含まれません。

 

 






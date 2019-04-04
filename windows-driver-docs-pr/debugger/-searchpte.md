---
title: searchpte
description: Searchpte 拡張機能は、指定したページのフレーム数 (PFN) の物理メモリを検索します。
ms.assetid: b9bac11e-605b-4064-b078-d3171b59da3b
keywords:
- Windows デバッグ searchpte
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- searchpte
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 954c895069cf8be024003b9ce39bf3b2adbacb75
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578011"
---
# <a name="searchpte"></a>!searchpte


**! Searchpte**拡張機能は、指定したページのフレーム数 (PFN) の物理メモリを検索します。

```dbgcmd
!searchpte PFN 
!searchpte -?
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______PFN______"></span><span id="_______pfn______"></span> *PFN*   
16 進数形式で、PFN を指定します。

<span id="_______-_______"></span> **-?**   
この拡張機能のデバッガー コマンド ウィンドウでヘルプを表示します。

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
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ページのテーブルとページのディレクトリについては、*Microsoft Windows internals 』*、Mark Russinovich と David Solomon を参照してください。 (この本できない場合がありますのいくつかの言語および国。)

<a name="remarks"></a>コメント
-------

いつでも実行を停止するには、(WinDbg) では、CTRL + BREAK または (KD) では、CTRL + C キーを押します。

 

 






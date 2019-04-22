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
ms.openlocfilehash: 522016ebe465bb97d0820a615ccbf41049c83abb
ms.sourcegitcommit: fb8b1d2e18dd727e8a479b04c9e6051e7e9fa484
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/18/2019
ms.locfileid: "59239489"
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

ページのテーブルとページのディレクトリについては、次を参照してください。 *Microsoft Windows internals 』*、Mark Russinovich と David Solomon します。 

<a name="remarks"></a>注釈
-------

いつでも実行を停止するには、(WinDbg) では、CTRL + BREAK または (KD) では、CTRL + C キーを押します。

 

 






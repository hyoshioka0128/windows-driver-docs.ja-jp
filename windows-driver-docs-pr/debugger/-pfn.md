---
title: pfn
description: Pfn 拡張機能では、特定のページ フレームまたはページ全体のフレームのデータベースに関する情報が表示されます。
ms.assetid: cbdb1f04-30bc-4e12-b073-9882e4457e1a
keywords:
- ページ フレーム
- Windows デバッグ pfn
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pfn
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 85a113b3b470fd5d3ed9602e8e7db0a98ec8a02c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537508"
---
# <a name="pfn"></a>!pfn


**! Pfn**拡張機能は、特定のページ フレームまたはページ全体のフレームのデータベースに関する情報を表示します。

```dbgcmd
!pfn PageFrame
```

## <a name="span-idddkpfndbgspanspan-idddkpfndbgspanparameters"></a><span id="ddk__pfn_dbg"></span><span id="DDK__PFN_DBG"></span>パラメーター


<span id="_______PageFrame______"></span><span id="_______pageframe______"></span><span id="_______PAGEFRAME______"></span> *PageFrame*   
表示されるページ フレームの 16 進数を指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ページのテーブル、ページのディレクトリ、およびページ フレームについては、次を参照してください。 *Microsoft Windows internals 』*、Mark Russinovich と David Solomon します。 (この本できない場合がありますのいくつかの言語および国。)

<a name="remarks"></a>注釈
-------

使用して、仮想アドレスのページ フレームの数を取得できます、 [ **! pte** ](-pte.md)拡張機能。

この拡張機能からの出力の例を次に示します。

```dbgcmd
kd> !pte 801544f4
801544F4  - PDE at C0300800        PTE at C0200550
          contains 0003B163      contains 00154121
        pfn 3b G-DA--KWV    pfn 154 G--A--KRV

kd> !pfn 3b
    PFN 0000003B at address 82350588
    flink       00000000  blink / share count 00000221  pteaddress C0300800
    reference count 0001                                 color 0
    restore pte 00000000  containing page        000039  Active   
 

kd> !pfn 154
    PFN 00000154 at address 82351FE0
    flink       00000000  blink / share count 00000001  pteaddress C0200550
    reference count 0001                                 color 0
    restore pte 00000060  containing page        00003B  Active     M     
    Modified          
```

 

 






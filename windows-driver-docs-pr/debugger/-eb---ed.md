---
title: eb、ed
description: Eb および ed 拡張機能は、指定された物理アドレスに値のシーケンスを書き込みます。 これらの拡張機能のコマンドと混同しない e\\ (値を入力) コマンド。
ms.assetid: 368937e4-0989-4dca-983a-65bc63142108
keywords:
- eb 拡張機能
- ed 拡張機能
- メモリ、拡張機能の物理書き込み (e)
- eb、ed Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- eb, ed
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ec85a19cf391ba5831c813b1749e6ffe0bbeb695
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334543"
---
# <a name="eb-ed"></a>!eb、!ed


**! Eb**と **! ed**拡張機能は、指定された物理アドレスに値のシーケンスを記述します。

これらの拡張機能のコマンドと混同しないで、 [ **e\* (値を入力)** ](e--ea--eb--ed--ed--ef--ep--eq--eu--ew--eza--ezu--enter-values-.md)コマンド。

```dbgcmd
!eb [Flag] PhysicalAddress Data [ ... ] 
!ed [Flag] PhysicalAddress Data [ ... ]
```

## <a name="span-idddkedbgspanspan-idddkedbgspanparameters"></a><span id="ddk__e__dbg"></span><span id="DDK__E__DBG"></span>パラメーター


<span id="_______Flag______"></span><span id="_______flag______"></span><span id="_______FLAG______"></span> *フラグ*   
次の値のいずれを指定できます。 *フラグ*値は、角かっこで囲む必要があります。

<span id="_c_"></span><span id="_C_"></span>**\[c\]**  
キャッシュされたメモリに書き込みます。

<span id="_uc_"></span><span id="_UC_"></span>**\[uc\]**  
キャッシュされていないメモリに書き込みます。

<span id="_wc_"></span><span id="_WC_"></span>**\[wc\]**  
書き込み結合のメモリに書き込みます。

<span id="_______PhysicalAddress______"></span><span id="_______physicaladdress______"></span><span id="_______PHYSICALADDRESS______"></span> *PhysicalAddress*   
データが書き込まれる、16 進数で、ターゲット コンピューター上の最初の物理アドレスを指定します。

<span id="_______Data______"></span><span id="_______data______"></span><span id="_______DATA______"></span> *データ*   
物理メモリに順番に書き込まれる 1 つまたは複数の値を指定します。 これらの値を 16 進形式で入力します。 **! Eb**拡張機能では、各値は 1 バイト (2 桁の 16 進数) である必要があります。 **! Ed**拡張機能では、各値は 1 つの DWORD (16 進数 8) である必要があります。 任意の数を含めることができます*データ*1 行の値。 複数の値を分離するには、コンマまたはスペースを使用します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p></p>
Kext.dll Kdextx86.dll</td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

物理メモリを読み取り、使用、 [ **! d\\**  * ](-db---dc---dd---dp---dq---du---dw.md)拡張機能。 その他のメモリに関連するコマンドの説明とメモリの操作の概要については、次を参照してください。[読み取りと書き込みメモリ](reading-and-writing-memory.md)します。

 

 






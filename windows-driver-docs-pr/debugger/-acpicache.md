---
title: acpicache
description: Acpicache 拡張機能では、すべての HAL によってキャッシュされる Advanced Configuration and Power Interface (ACPI) のテーブルが表示されます。
ms.assetid: 488bbc40-0f67-4d13-8615-944ff8a6a177
keywords:
- Windows デバッグ acpicache
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- acpicache
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a5e2600a8a4d9b218e3c2153cf3d476c5861d46a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334827"
---
# <a name="acpicache"></a>!acpicache


**! Acpicache**拡張機能では、すべての HAL によってキャッシュされる Advanced Configuration and Power Interface (ACPI) のテーブルが表示されます。

```dbgcmd
!acpicache [DisplayLevel]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______DisplayLevel______"></span><span id="_______displaylevel______"></span><span id="_______DISPLAYLEVEL______"></span> *DisplayLevel*   
表示の詳細レベルを指定します。 この値は省略形の表示の場合は 0 または 1 の詳細の表示のいずれかです。 既定値は 0 です。

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

ACPI の詳細については、Microsoft Windows Driver Kit (WDK) ドキュメント、Windows SDK のドキュメントを参照してくださいと*Microsoft Windows internals 』* Mark Russinovich と David Solomon します。 (これらの書籍やリソースできない場合がありますのいくつかの言語および国。)参照してください[ACPI デバッグ](acpi-debugging.md)については、ACPI に関連付けられている他の拡張機能。

 

 






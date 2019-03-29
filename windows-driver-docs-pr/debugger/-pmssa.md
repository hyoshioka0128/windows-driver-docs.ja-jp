---
title: pmssa
description: Pmssa 拡張機能では、指定されたプロセッサの最小限の状態の保存領域 (最小 StateSave 領域とも呼ばれます) が表示されます。
ms.assetid: 55d605bd-0621-4366-8b37-62d462ee1f34
keywords:
- プロセッサ minstate 領域の保存
- Windows デバッグ pmssa
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pmssa
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cd8c009c07d34b416a2f1542b236ca3fc40853ea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580137"
---
# <a name="pmssa"></a>!pmssa


**! Pmssa**拡張機能には、指定されたプロセッサの最小限の状態の保存領域 (最小 StateSave 領域とも呼ばれます) が表示されます。

この拡張機能は、対象の Itanium ベース コンピューターにのみ使用できます。

```dbgcmd
!pmssa Address
```

**重要な**  このコマンドが 10.0.14257 Windows デバッガーのバージョンでは非推奨以降されてし、は現在利用できません。

 

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
Min StateSave 領域、プロセッサのアドレスを指定します。

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

 

 

 






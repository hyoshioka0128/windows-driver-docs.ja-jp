---
title: psp
description: Psp 拡張機能では、指定したアドレスにプロセッサの状態のパラメーター (PSP) レジスタを表示します。
ms.assetid: 5ed36051-31e0-405f-ac30-88d888f9d915
keywords:
- プロセッサの状態パラメーター (PSP)
- PSP 登録
- Windows デバッグ psp
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- psp
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5214b39c5db25f64ae38ea49d2fb10dfeaac52db
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550740"
---
# <a name="psp"></a>! psp


**! Psp**拡張機能は、指定したアドレスでプロセッサ状態パラメーター (PSP) 登録を表示します。

この拡張機能は、対象の Itanium ベースのコンピューターでのみサポートされます。

```dbgcmd
!psp Address [DisplayLevel]
```

**重要な**  このコマンドが 10.0.14257 Windows デバッガーのバージョンでは非推奨以降されてし、は現在利用できません。

 

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
表示する PSP レジスタの 16 進数のアドレスを指定します。

<span id="_______DisplayLevel______"></span><span id="_______displaylevel______"></span><span id="_______DISPLAYLEVEL______"></span> *DisplayLevel*   
次のオプションのいずれかを指定できます。

<span id="0"></span>**0**  
PSP の各フィールドの値のみが表示されます。 これが既定値です。

<span id="1"></span>**1**  
予約済みまたは無視されていない PSP フィールドの各詳細な情報を表示します。

<span id="2"></span>**2**  
すべて無視するか予約されているものも含め、PSP フィールドの詳細な情報を表示します。

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

 

 

 






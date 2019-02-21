---
title: pmc
description: Pmc の拡張機能では、指定したアドレスにパフォーマンス モニター カウンター (PMC) の登録が表示されます。
ms.assetid: ff9a03af-f0e9-4aef-b583-c3092eb5f89c
keywords:
- パフォーマンス モニター カウンター (PMC)
- pmc Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pmc
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f2145f09a4554d72e778d79fa9e31a0ff10959ea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558028"
---
# <a name="pmc"></a>!pmc


**! Pmc**拡張機能は、指定したアドレスにパフォーマンス モニター カウンター (PMC) 登録を表示します。

この拡張機能は、Itanium ベースのターゲット コンピューター上でのみサポートされています。

```dbgcmd
!pmc [- Option] Expression [DisplayLevel]
```

**重要な**  このコマンドが 10.0.14257 Windows デバッガーのバージョンでは非推奨以降されてし、は現在利用できません。

 

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Option______"></span><span id="_______option______"></span><span id="_______OPTION______"></span> *オプション*   
次の値のいずれかを指定できます。

<span id="gen"></span><span id="GEN"></span>**汎用**  
汎用 PMC レジスタとして、登録が表示されます。

<span id="btb"></span><span id="BTB"></span>**btb**  
ブランチ トレース バッファー (BTB) PMC として登録のレジスタが表示されます。

<span id="_______Expression______"></span><span id="_______expression______"></span><span id="_______EXPRESSION______"></span> *式*   
PMC の 16 進数のアドレスを指定します。 式<strong>@kpfcgen</strong>と<strong>@kpfcbtb</strong>このパラメーターの値として使用できます。

場合*式*は <strong>@kpfcgen</strong>デバッガーを表示する、現在のプロセッサの PMC がジェネリックの PMC 登録として登録します。 PMC を設定して、汎用の PMC レジスタとして登録する、現在のプロセッサを表示することもできます*オプション*に**gen**を使用して、 <strong>@kpfc4</strong>、  <strong>。@kpfc5</strong>、 <strong>@kpfc6</strong>、または<strong>@kpfc7</strong>の*式*値。

場合*式*は <strong>@kpfcbtb</strong>デバッガーを表示する、現在のプロセッサの PMC を BTB PMC レジスタとして登録します。 PMC を設定して BTB PMC 登録として登録する、現在のプロセッサを表示することもできます。*オプション*に**btb**を使用して、@kpfc12の、*式*値。

<span id="_______DisplayLevel______"></span><span id="_______displaylevel______"></span><span id="_______DISPLAYLEVEL______"></span> *DisplayLevel*   
次の値のいずれかを指定できます。

<span id="0"></span>**0**  
フィールドを登録する各 PMC の値のみを表示します。 これが既定値です。

<span id="1"></span>**1**  
PMC について詳細情報を表示では、予約済みまたは無視されていないフィールドを登録します。

<span id="2"></span>**2**  
すべて PMC に関する詳細情報を表示では、無視するか予約されているものも含め、すべてのフィールドを登録します。

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

 

 

 






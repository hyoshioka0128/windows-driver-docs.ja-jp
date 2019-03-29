---
title: dcr
description: Dcr 拡張機能では、指定したアドレスに既定のコントロールの登録 (DCR) が表示されます。
ms.assetid: 294fc3a9-5182-47ae-a261-53be6389bcf1
keywords:
- DCR (既定のコントロールの登録)
- Windows デバッグ dcr
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dcr
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 80e3f305d137335cb84401f75007acade430656e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573285"
---
# <a name="dcr"></a>!dcr


**! Dcr**拡張機能では、指定したアドレスに既定制御レジスタ (DCR) が表示されます。

```dbgcmd
!dcr Expression [DisplayLevel]
```

**重要な**  このコマンドが 10.0.14257 Windows デバッガーのバージョンでは非推奨以降されてし、は現在利用できません。

 

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Expression______"></span><span id="_______expression______"></span><span id="_______EXPRESSION______"></span> *式*   
表示する DCR の 16 進数のアドレスを指定します。 式<strong>@dcr</strong>このパラメーターにも使用できます。 その場合は、現在のプロセッサ DCR に関する情報が表示されます。

<span id="_______DisplayLevel______"></span><span id="_______displaylevel______"></span><span id="_______DISPLAYLEVEL______"></span> *DisplayLevel*   
次のオプションのいずれかを指定できます。

<span id="0"></span>**0**  
表示するには、各 DCR フィールドの値のみをによりします。 これが既定値です。

<span id="1"></span>**1**  
予約済みまたは無視されていない DCR フィールドのそれぞれの詳細については、するためにディスプレイをによりします。

<span id="2"></span>**2**  
すべての無視するか予約されているものも含め、DCR フィールドの詳細については、表示をによりします。

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

 

この拡張機能のコマンドは、対象の Itanium ベース コンピューターにのみ使用できます。

<a name="remarks"></a>コメント
-------

DCR では、プロセッサのステータスの既定のパラメーターはレジスタ中断することで値を指定します。 DCR も、いくつか追加のグローバル コントロールを投機的な読み込みエラーを遅延できるかどうかも指定します。

いくつかの例を次に示します。

```dbgcmd
kd> !dcr @dcr
dcr:pp be lc dm dp dk dx dr da dd
1 0 1 1 1 1 1 1 1 1

kd> !dcr @dcr 2

  pp : 1 : Privileged Performance Monitor Default
  be : 0 : Big-Endian Default
  lc : 1 : IA-32 Lock check Enable
  rv : 0 : reserved1
  dm : 1 : Defer TLB Miss faults only
  dp : 1 : Defer Page Not Present faults only
  dk : 1 : Defer Key Miss faults only
  dx : 1 : Defer Key Permission faults only
  dr : 1 : Defer Access Rights faults only
  da : 1 : Defer Access Bit faults only
  dd : 0 : Defer Debug faults only
  rv : 0 : reserved2
```

 

 






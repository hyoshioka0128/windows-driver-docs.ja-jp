---
title: pcr
description: Pcr 拡張機能には、Intel Itanium 固有のプロセッサ コントロール レジスタが表示されます。
ms.assetid: 45a84a95-86df-4176-ba30-ac93b509f7f7
keywords:
- プロセッサ コントロール レジスタ (PCR)
- PCR (プロセッサ コントロール レジスタ)
- Windows デバッグ pcrs
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pcrs
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 17b42efee88384b3e7acabddcb345f0d5d3fd727
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335819"
---
# <a name="pcrs"></a>!pcrs


**! Pcrs**拡張機能には、Intel Itanium 固有プロセッサ コントロール レジスタが表示されます。

```dbgcmd
!pcrs Address
```

**重要な**  このコマンドが 10.0.14257 Windows デバッガーのバージョンでは非推奨以降されてし、は現在利用できません。

 

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
プロセッサ コントロールのアドレスは登録ファイルを指定します。

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

<a name="remarks"></a>注釈
-------

混同しないでください、 **! pcrs**拡張機能、 [ **! pcr** ](-pcr.md)拡張機能は、プロセッサの制御領域の現在の状態を表示します。

 

 






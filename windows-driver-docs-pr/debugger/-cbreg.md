---
title: cbreg
description: Cbreg 拡張機能が CardBus ソケットの登録を表示し、CardBus Exchangable カードのアーキテクチャ (ExCA) を登録します。
ms.assetid: 7943e152-b1c9-464c-a0ad-3beac48884d2
keywords:
- CardBus
- ExCA レジスタ
- Windows デバッグ cbreg
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- cbreg
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0633d985e91f628746d2bf30d1f055654c7320dd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336899"
---
# <a name="cbreg"></a>!cbreg


**! Cbreg** CardBus ソケットの登録を表示拡張機能と CardBus Exchangable カードのアーキテクチャ (ExCA) を登録します。

```dbgsyntax
    !cbreg [%%]Address 
```

## <a name="span-idddkcbregdbgspanspan-idddkcbregdbgspanparameters"></a><span id="ddk__cbreg_dbg"></span><span id="DDK__CBREG_DBG"></span>パラメーター


<span id="_______________"></span> **%%**   
示します*アドレス*は仮想アドレスではなく、物理アドレスです。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
表示されるレジスタのアドレスを指定します。

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

 

**! Cbreg**拡張機能は x86 ベースの移行先のコンピューターの使用のみ。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

[ **! Exca** ](-exca.md) PCIC ExCA レジスタをソケット数で表示拡張機能を使用できます。

 

 






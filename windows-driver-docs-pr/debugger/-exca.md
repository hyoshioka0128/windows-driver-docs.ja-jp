---
title: exca
description: Exca 拡張機能には、PC カード割り込みコント ローラー (PCIC) Exchangable カードのアーキテクチャ (ExCA) レジスタが表示されます。
ms.assetid: a395f7f3-0e1d-4f4c-80a1-018ca52a20fd
keywords:
- PCIC (PC カード割り込みコント ローラー)
- ExCA レジスタ
- Windows デバッグ exca
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- exca
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 474a70bed6dda22d453db1b7b4c462d4ecaaaf43
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582187"
---
# <a name="exca"></a>!exca


**! Exca**拡張機能には、PC カード割り込みコント ローラー (PCIC) Exchangable カードのアーキテクチャ (ExCA) レジスタが表示されます。

```dbgcmd
!exca BasePort.SocketNumber
```

## <a name="span-idddkexcadbgspanspan-idddkexcadbgspanparameters"></a><span id="ddk__exca_dbg"></span><span id="DDK__EXCA_DBG"></span>パラメーター


<span id="_______BasePort______"></span><span id="_______baseport______"></span><span id="_______BASEPORT______"></span> *BasePort*   
PCIC のベース ポートを指定します。

<span id="_______SocketNumber______"></span><span id="_______socketnumber______"></span><span id="_______SOCKETNUMBER______"></span> *SocketNumber*   
PCIC ExCA レジスタのソケット数を指定します。

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

 

**! Exca**拡張機能は x86 ベースの移行先のコンピューターの使用のみ。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

[ **! Cbreg** ](-cbreg.md)拡張機能を使用して、CardBus ソケットの登録を表示し、アドレスで CardBus ExCA を登録します。

 

 






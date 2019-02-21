---
title: openmaps
description: Openmaps 拡張機能には、参照先のバッファー制御ブロック (BCBs) と、指定された共有キャッシュのマップの制御ブロック (同時に Vacb) 仮想アドレスが表示されます。
ms.assetid: 4ecce331-c18e-462a-807a-b8929059b897
keywords:
- BCB (バッファーのコントロール ブロック)
- VACB (仮想アドレス コントロール ブロック)
- 共有キャッシュのマップ
- キャッシュ マネージャー
- Windows デバッグ openmaps
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- openmaps
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2496778b2ec95bd3941420766cf0087c241d0e78
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549263"
---
# <a name="openmaps"></a>! openmaps


**! Openmaps**拡張機能は、参照先のバッファーのコントロール ブロック (BCBs) を表示し、仮想アドレス コントロールが、指定された共有キャッシュのマップの (同時に Vacb) をブロックします。

```dbgcmd
!openmaps Address [Flag]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
共有キャッシュのマップのアドレスを指定します。

<span id="_______Flag______"></span><span id="_______flag______"></span><span id="_______FLAG______"></span> *フラグ*   
コントロール ブロックが表示されるかを決定します。 場合*フラグ*は**1**デバッガーですべてのコントロール ブロックを表示します。 場合*フラグ*は**0**デバッガーは、コントロール ブロックの参照のみが表示されます。 既定値は**0**します。

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

キャッシュの管理については、Microsoft Windows SDK のマニュアルを参照し、 *Microsoft Windows internals 』* Mark Russinovich と David Solomon します。 (これらのリソースできない場合がありますのいくつかの言語および国。)

その他のキャッシュ管理拡張機能については、次を参照してください。、 [ **! cchelp** ](-cchelp.md)拡張機能。

 

 






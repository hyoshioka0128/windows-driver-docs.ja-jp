---
title: bcb
description: Bcb 拡張機能では、指定したバッファーの制御ブロックが表示されます。
ms.assetid: 4e98e900-5e9d-40a4-9c39-4dc3611d8ea3
keywords:
- キャッシュ マネージャー
- Windows デバッグ bcb
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- bcb
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bd18387b76f6f7952ea061217a09cdb79f0dff97
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334729"
---
# <a name="bcb"></a>!bcb


**! Bcb**拡張機能には、指定したバッファーの制御ブロックが表示されます。

```dbgcmd
!bcb Address
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
バッファーのコントロール ブロックのアドレスを指定します。

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
<td align="left"><p>利用不可 (「解説」を参照してください セクション)</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

キャッシュの管理については、Microsoft Windows SDK のマニュアルを参照し、 *Microsoft Windows internals 』* Mark Russinovich と David Solomon します。 (これらのリソースできない場合がありますのいくつかの言語および国。)

その他のキャッシュ管理拡張機能については、使用、 [ **! cchelp** ](-cchelp.md)拡張機能。

<a name="remarks"></a>注釈
-------

この拡張機能は、Windows 2000 のみです。 Windows XP 以降を使用して、 [ **dt nt!\_BCB アドレス**](dt--display-type-.md)バッファーのコントロール ブロックを直接表示するコマンド。

 

 






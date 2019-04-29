---
title: scm
description: Scm の拡張機能は、指定された共有キャッシュのマップを表示します。
ms.assetid: 4333ee14-ca28-43af-b132-210996328af2
keywords:
- 共有キャッシュのマップ
- キャッシュ マネージャー
- scm Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- scm
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 58a985eb874522ff9289b0b038211fec30b7d3b0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330787"
---
# <a name="scm"></a>!scm


**! Scm**拡張機能は、指定された共有キャッシュのマップを表示します。

```dbgcmd
!scm Address
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
共有キャッシュのマップのアドレスを指定します。

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
<td align="left"><p>利用不可</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

キャッシュの管理については、Microsoft Windows SDK のマニュアルを参照し、 *Microsoft Windows internals 』* Mark Russinovich と David Solomon します。 (これらのリソースできない場合がありますのいくつかの言語および国。)

その他のキャッシュ管理拡張機能については、次を参照してください。、 [ **! cchelp** ](-cchelp.md)拡張機能。

<a name="remarks"></a>注釈
-------

Windows XP および以降のバージョンの Windows では、使用、 [ **dt nt!\_共有\_キャッシュ\_マップ アドレス**](dt--display-type-.md)コマンドの代わりに **! scm**します。

 

 






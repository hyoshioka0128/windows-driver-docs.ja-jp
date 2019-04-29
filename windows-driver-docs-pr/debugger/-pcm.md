---
title: pcm
description: Pcm の拡張機能は、指定されたプライベート キャッシュのマップを表示します。 この拡張機能は、Windows 2000 ではできるだけです。
ms.assetid: a6880ad0-5326-4bea-ac84-3311a2ec01da
keywords:
- プライベート キャッシュのマップ
- キャッシュ マネージャー
- pcm の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pcm
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1ede535bc8316dc8e5cb0e4c2ad37a5dcf3b9631
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334415"
---
# <a name="pcm"></a>!pcm


**! Pcm**拡張機能は、指定されたプライベート キャッシュのマップを表示します。 この拡張機能は、Windows 2000 ではできるだけです。

```dbgcmd
!pcm Address
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
プライベート キャッシュのマップのアドレスを指定します。

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

その他のキャッシュ管理拡張機能については、次を参照してください。、 [ **! cchelp** ](-cchelp.md)拡張機能の参照。

<a name="remarks"></a>注釈
-------

この拡張機能は、Windows 2000 でのみサポートされます。 Windows XP および以降のバージョンの Windows では、使用、 [ **dt nt!\_プライベート\_キャッシュ\_マップ アドレス**](dt--display-type-.md)コマンド。

 

 






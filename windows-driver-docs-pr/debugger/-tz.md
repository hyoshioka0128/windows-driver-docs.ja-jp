---
title: tz
description: Tz 拡張機能は、指定した電源熱ゾーン構造を表示します。
ms.assetid: f3cc9e54-a0db-4095-b707-380ec1dacf59
keywords:
- 温度のゾーン
- Windows デバッグ tz
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- tz
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 65a45d8e262acb6bac93a47f07c8e4690ca0326a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334166"
---
# <a name="tz"></a>!tz


**! Tz**拡張機能には、指定した電源熱ゾーン構造が表示されます。

```dbgcmd
!tz [Address]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
表示する電源の熱のゾーンのアドレス。 このパラメーターを省略した場合、表示には、ターゲット コンピューター上のすべての熱ゾーンが含まれます。

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

表示するには、システムの電源機能を使用して、 [ **! pocaps** ](-pocaps.md)拡張機能コマンド。 表示するには、システムの電源ポリシーを使用して、 [ **! popolicy** ](-popolicy.md)拡張機能コマンド。 電源機能、および電源ポリシーについては、Windows Driver Kit (WDK) ドキュメントを参照してくださいと*Microsoft Windows internals 』*、Mark Russinovich と David Solomon します。 (これらのリソースできない場合がありますのいくつかの言語および国。)

<a name="remarks"></a>注釈
-------

いつでも実行を停止するには、(WinDbg) では、CTRL + BREAK または (KD) では、CTRL + C キーを押します。

 

 






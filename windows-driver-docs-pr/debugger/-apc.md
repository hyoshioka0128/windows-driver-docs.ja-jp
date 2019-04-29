---
title: apc
description: Apc 拡張機能は、書式設定し、1 つの内容を表示または複数の非同期プロシージャ呼び出し (Apc)。
ms.assetid: 0c5a9d1e-ab61-4b14-b06b-25cde582cc73
keywords:
- apc の Windows デバッグ
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- apc
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 636f12b3f84be54af06a550fff1ff84fa6d20ae7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334753"
---
# <a name="apc"></a>!apc


**! Apc**複数の非同期プロシージャ呼び出し (Apc) または拡張機能は、書式設定し、1 つの内容を表示します。

```dbgcmd
    !apc
    !apc proc Process
    !apc thre Thread
    !apc KAPC
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="Process"></span><span id="process"></span><span id="PROCESS"></span>*プロセス*  
Apc を表示するか、プロセスのアドレスを指定します。

<span id="Thread"></span><span id="thread"></span><span id="THREAD"></span>*スレッド*  
Apc を表示するか、スレッドのアドレスを指定します。

<span id="_______KAPC______"></span><span id="_______kapc______"></span> *KAPC*   
表示される APC カーネルのアドレスを指定します。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


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

 

## <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報


Apc の詳細については、Windows Driver Kit (WDK) ドキュメントと Mark Russinovich と David Solomon Microsoft Windows internals 』 を参照してください。

<a name="remarks"></a>注釈
-------

任意のパラメーターを指定せず **! apc**すべて Apc が表示されます。

以下に例を示します。

```console
kd> !apc
*** Enumerating APCs in all processes
Process e0000000858ba8b0 System
Process e0000165fff86040 smss.exe
Process e0000165fff8c040 csrss.exe
Process e0000165fff4e1d0 winlogon.exe
Process e0000165fff101d0 services.exe
Process e0000165fffa81d0 lsass.exe
Process e0000165fff201d0 svchost.exe
Process e0000165fff8e040 svchost.exe
Process e0000165fff3e040 svchost.exe
Process e0000165fff6e040 svchost.exe
Process e0000165fff24040 spoolsv.exe
Process e000000085666640 wmiprvse.exe
Process e00000008501e520 wmiprvse.exe
Process e0000000856db480 explorer.exe
Process e0000165fff206a0 ctfmon.exe
Process e0000000850009d0 ctfmon.exe
Process e0000165fff51600 conime.exe
Process e000000085496340 taskmgr.exe
Process e000000085489c30 userinit.exe
```

 

 






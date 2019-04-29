---
title: 組み込み
description: 組み込みの拡張機能は、指定されたプロセッサの割り込みの履歴レコードを表示します。
ms.assetid: 4c81bde4-da8b-4c44-8013-6c586c08e22b
keywords:
- 割り込みの履歴レコード
- 組み込みの Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ih
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e2c6da77278c0c1b39062dba06c4983d31ed5a09
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336440"
---
# <a name="ih"></a>!ih


**! 組み込み**拡張機能には、指定されたプロセッサの割り込み履歴レコードが表示されます。

```dbgcmd
!ih Processor
```

**重要な**  このコマンドが 10.0.14257 Windows デバッガーのバージョンでは非推奨以降されてし、は現在利用できません。

 

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span> *プロセッサ*   
プロセッサを指定します。 場合*プロセッサ*は省略すると、現在のプロセッサが使用されます。

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

この拡張機能は、プログラム カウンターのシンボルを参照することがなく、割り込みの履歴レコードを表示します。 プログラム カウンターのシンボルを使用して、割り込みの履歴レコードを表示するには、使用、 [ **! his** ](-ihs.md)拡張機能。 割り込みの履歴レコードを有効にするには追加 **/configflag = 32**ブート エントリのオプションにします。

この拡張機能からの出力の例を次に示します。

```dbgcmd
kd> !ih
Total # of interruptions = 2093185
Vector              IIP                   IPSR          ExtraField 
 VHPT FAULT  e0000000830d3190      1010092a6018  IFA=      6fc00a0200c 
        VHPT FAULT  e0000000830d33d0      1010092a6018  IFA= 1ffffe00001de2d0 
 VHPT FAULT  e0000000830d33d0      1010092a6018  IFA= 1ffffe01befff338 
        VHPT FAULT  e0000000830d3190      1010092a6018  IFA=      6fc00a0200c 
        VHPT FAULT  e0000000830d33d0      1010092a6018  IFA= 1ffffe00001d9188 
        VHPT FAULT  e0000000830d3880      1010092a6018  IFA= 1ffffe01befff250 
        VHPT FAULT  e0000000830d3fb0      1010092a6018  IFA= e0000165f82dc1c0 
 VHPT FAULT  e000000083063390      1010092a6018  IFA= e0000000fffe0018 
     THREAD SWITCH  e000000085896040  e00000008588c040  OSP= e0000165f82dbd40 
        VHPT FAULT  e00000008329b130      1210092a6018  IFA= e0000165f7edaf30 
        VHPT FAULT  e0000165f7eda640      1210092a6018  IFA= e0000165fff968a9 
    PROCESS SWITCH  e0000000818bbe10  e000000085896040  OSP= e0000165f8281de0 
        VHPT FAULT  e00000008307cfc0      1010092a2018  IFA= e00000008189fe50 
EXTERNAL INTERRUPT  e0000000830623b0      1010092a6018  IVR=               d0 
        VHPT FAULT  e00000008314e310      1010092a2018  IFA= e0000165f88203f0 
        VHPT FAULT  e000000083580760      1010092a2018  IFA= e0000000f00ff3fd 
    PROCESS SWITCH  e00000008558c990  e0000000818bbe10  OSP= e00000008189fe20 
        VHPT FAULT  e00000008307cfc0      1010092a2018  IFA= e0000165f02433f0 
        VHPT FAULT          77cfbda0      1013082a6018  IFA=         77cfbda0 
 VHPT FAULT          77cfbdb0      1213082a6018  IFA=      6fbfee0ff98 
   DATA ACCESS BIT          77b8e150      1213082a6018  IFA=         77c16ab8 
        VHPT FAULT          77ed5d60      1013082a6018  IFA=      6fbfffa6048 
   DATA ACCESS BIT          77ed5d60      1213082a6018  IFA=         77c229c0 
 DATA ACCESS BIT          77b8e1b0      1013082a6018  IFA=         77c1c320 
      USER SYSCALL          77cafa40        10082a6018  Num=               42 
 VHPT FAULT  e00000008344dc20      1010092a6018  IFA= e000010600703784 
...
```

 

 






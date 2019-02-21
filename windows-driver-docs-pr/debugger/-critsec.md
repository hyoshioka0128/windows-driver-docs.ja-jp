---
title: critsec
description: Critsec 拡張機能では、クリティカル セクションが表示されます。
ms.assetid: 7e30efd5-2bdc-420c-b3ed-504280ddd8f7
keywords:
- Windows デバッグ critsec
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- critsec
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 37171ddd8dc73228f783bb2966c85a0858718336
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532244"
---
# <a name="critsec"></a>! critsec


**! Critsec**拡張機能がクリティカル セクションが表示されます。

```dbgsyntax
!critsec Address 
```

## <a name="span-idddkcritsecdbgspanspan-idddkcritsecdbgspanparameters"></a><span id="ddk__critsec_dbg"></span><span id="DDK__CRITSEC_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
クリティカル セクションの 16 進数のアドレスを指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ntsdexts.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Ntsdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

その他のコマンドとクリティカル セクションの情報を表示できる拡張機能では、次を参照してください。[クリティカル セクションを表示する](displaying-a-critical-section.md)します。 重要なセクションについては、Microsoft Windows SDK ドキュメントに、Windows Driver Kit (WDK) ドキュメントを参照してくださいと*Microsoft Windows internals 』* Mark Russinovich と David Solomon します。

<a name="remarks"></a>注釈
-------

使用する必要があります、クリティカル セクションのアドレスがわからない場合、 [ **! ntsdexts.locks** ](-locks---ntsdexts-locks-.md)拡張機能。 呼び出すことによって初期化されているすべての重要なセクションが表示されます**RtlInitializeCriticalSection**します。

以下に例を示します。

```dbgcmd
0:000> !critsec 3a8c0e9c

CritSec +3a8c0e9c at 3A8C0E9C
LockCount          1
RecursionCount     1
OwningThread       99
EntryCount         472
ContentionCount    1
*** Locked
```

 

 






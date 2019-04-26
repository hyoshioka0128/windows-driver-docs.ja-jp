---
title: storagekd.storloglist
description: Storagekd.storloglist 拡張機能には、Storport アダプターの内部のログ エントリが表示されます。
ms.assetid: 6308DDEF-8AB0-4D16-9245-3046114D5173
keywords:
- デバッグ storagekd.storloglist Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- storagekd.storloglist
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bad0a2d5c26f63bca91ef6cc546843c7a7eaa81d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339672"
---
# <a name="storagekdstorloglist"></a>!storagekd.storloglist


**! Storagekd.storloglist**拡張機能には、Storport アダプターの内部のログ エントリが表示されます。

```dbgcmd
!storagekd.storloglist <Address> [<starting_entry> [<ending_entry>]] [L <count>] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
Storport アダプター デバイス拡張機能またはデバイス オブジェクトのアドレスを指定します。

<span id="_______starting_entry______"></span><span id="_______STARTING_ENTRY______"></span> *starting\_entry*   
先頭のエントリを表示する範囲。 指定しない場合、最後の*カウント*エントリが表示されます。

<span id="_______ending_entry______"></span><span id="_______ENDING_ENTRY______"></span> *ending\_entry*   
表示する範囲の終了エントリ。 指定しない場合、*カウント*以降で指定された項目では、項目が表示されます*開始\_エントリ*します。

<span id="_______count______"></span><span id="_______COUNT______"></span> *count*   
表示されるエントリの数。 指定しない場合、値 50 が使用されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 8 以降</strong></p></td>
<td align="left"><p>Storagekd.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

次の例に示します **! storagekd.storloglist**表示。

**0: kd&gt; !storagekd.storloglist ffffe0010f5e01a0**

```dbgcmd
Storport RaidLogList
    Circular buffer location:  0xffffe0010f5e1720
    Total logs written: 8
    Displaying entries 0 through 7
    ---------------------------------------------------------------------
    [0]_[23:04:20.521] ResumeDevice.......... Caller: storport!RaidUnitPauseTimerDpcRoutine+0x28 (fffff800`fb4d0b28), P/P/T/L: 0/0/0/0, Pause count: 0, Resumed: True
    [1]_[23:04:20.646] ResumeDevice.......... Caller: storport!RaidUnitPauseTimerDpcRoutine+0x28 (fffff800`fb4d0b28), P/P/T/L: 0/0/0/0, Pause count: 0, Resumed: True
    [2]_[23:04:20.646] SpPauseDevice......... Caller: iaStorAV!RpiPauseDevice+0x67 (fffff800`fb70554f), P/T/L: 3/0/0, Timeout: 180, Adapter: 0xffffe0010f5e01a0
    [3]_[23:04:20.646] PauseDevice........... Caller: storport!StorPortPauseDevice+0x2f6 (fffff800`fb4b52d6), P/P/T/L: 0/3/0/0, Pause count: 1
    [4]_[23:04:20.646] SpResumeDevice........ Caller: iaStorAV!RpiResumeDevice+0x5f (fffff800`fb7055fb), P/T/L: 3/0/0, Adapter: 0xffffe0010f5e01a0
    [5]_[23:04:20.646] ResumeDevice.......... Caller: storport!StorPortResumeDevice+0x19 (fffff800`fb4aa23f), P/P/T/L: 0/3/0/0, Pause count: 0, Resumed: True
    [6]_[23:04:20.646] SpPauseDevice......... Caller: iaStorAV!RpiPauseDevice+0x67 (fffff800`fb70554f), P/T/L: 3/0/0, Timeout: 180, Adapter: 0xffffe0010f5e01a0
    [7]_[23:04:20.646] PauseDevice........... Caller: storport!StorPortPauseDevice+0x2f6 (fffff800`fb4b52d6), P/P/T/L: 0/3/0/0, Pause count: 1
```

 

 






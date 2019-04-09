---
title: Peb
description: Peb 拡張機能には、プロセスの環境ブロック (PEB) での情報の書式設定されたビューが表示されます。
ms.assetid: 01687f13-9eb7-48f0-a0d6-54fee00084ab
keywords:
- PEB (プロセスの環境ブロック)
- プロセス、プロセスの環境ブロック (PEB)
- Windows デバッグ peb
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- peb
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1b8d30605c25ad6839ab818329ef470d1b9d27de
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2019
ms.locfileid: "59238523"
---
# <a name="peb"></a>!peb


**! Peb**拡張機能では、プロセスの環境ブロック (PEB) で、情報の書式設定されたビューが表示されます。

```dbgcmd
!peb [PEB-Address]
```

## <a name="span-idddkpebdbgspanspan-idddkpebdbgspanparameters"></a><span id="ddk__peb_dbg"></span><span id="DDK__PEB_DBG"></span>パラメーター


<span id="_______PEB-Address______"></span><span id="_______peb-address______"></span><span id="_______PEB-ADDRESS______"></span> *PEB アドレス*   
プロセスを調べるの PEB の 16 進数のアドレス。 (これが、プロセスのカーネルの処理ブロックから派生したとして PEB のアドレス)場合*PEB アドレス*を省略すると、PEB ユーザー モードで、現在のプロセスが使用されます。 かどうかは、カーネル モードでは、現在に対応する PEB で省略[プロセス コンテキスト](changing-contexts.md#process-context)が表示されます。

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
Kdextx86.dll Ntsdexts.dll</td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Exts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

プロセスの環境ブロックについては、次を参照してください。 *Microsoft Windows internals 』* Mark Russinovich と David Solomon します。 

<a name="remarks"></a>注釈
-------

PEB は、Microsoft Windows プロセスの制御構造のユーザー モードの部分です。

場合、 **! peb**引数なしで拡張機能、エラーを表示カーネル モードでは、使用する必要があります、 [ **! プロセス**](-process.md)拡張機能を目的のプロセスの PEB アドレスを決定します。 確認、[プロセス コンテキスト](changing-contexts.md#process-context)が目的の処理 に設定し、引数として PEB アドレスを使用 **! peb**。

正確な出力が表示されるは、Windows バージョンとカーネル モードまたはユーザー モードでデバッグしているかどうかによって異なります。 次の例は、Windows Server 2003 のターゲットに接続されているカーネル デバッガーから取得されます。

```dbgcmd
kd> !peb
PEB at 7ffdf000
    InheritedAddressSpace:    No
    ReadImageFileExecOptions: No
    BeingDebugged:            No
    ImageBaseAddress:         4ad00000
    Ldr                       77fbe900
    Ldr.Initialized:          Yes
    Ldr.InInitializationOrderModuleList: 00241ef8 . 00242360
    Ldr.InLoadOrderModuleList:           00241e90 . 00242350
    Ldr.InMemoryOrderModuleList:         00241e98 . 00242358
            Base TimeStamp                     Module
        4ad00000 3d34633c Jul 16 11:17:32 2002 D:\WINDOWS\system32\cmd.exe
        77f40000 3d346214 Jul 16 11:12:36 2002 D:\WINDOWS\system32\ntdll.dll
        77e50000 3d3484ef Jul 16 13:41:19 2002 D:\WINDOWS\system32\kernel32.dll
....
    SubSystemData:     00000000
    ProcessHeap:       00140000
    ProcessParameters: 00020000
    WindowTitle:  'D:\Documents and Settings\Administrator\Desktop\Debuggers.lnk'
    ImageFile:    'D:\WINDOWS\system32\cmd.exe'
    CommandLine:  '"D:\WINDOWS\system32\cmd.exe" '
    DllPath:      'D:\WINDOWS\system32;D:\WINDOWS\system32;....
    Environment:  00010000
        ALLUSERSPROFILE=D:\Documents and Settings\All Users
        APPDATA=D:\Documents and Settings\UserTwo\Application Data
        CLIENTNAME=Console
....
        windir=D:\WINDOWS
```

同様、 [ **! teb** ](-teb.md)拡張機能は、スレッド環境ブロックを表示します。

 

 






---
title: dll
description: Dll の拡張機能では、すべての読み込まれたモジュールまたは指定したスレッドまたはプロセスを使用しているすべてのモジュールのテーブルのエントリが表示されます。
ms.assetid: a47ec828-ba5a-4f0d-be85-18633c4e4185
keywords:
- テーブルの DLL のエントリ
- Windows デバッグ dll
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dlls
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ecc7403b805161a95118a64dc92e015c06cccd00
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560712"
---
# <a name="dlls"></a>! dll


**! Dll**拡張機能が読み込まれたすべてのモジュールまたは指定したスレッドまたはプロセスを使用しているすべてのモジュールのテーブルのエントリが表示されます。

```dbgcmd
!dlls [Options] [LoaderEntryAddress] 
!dlls -h
```

## <a name="span-idddkdllsdbgspanspan-idddkdllsdbgspanparameters"></a><span id="ddk__dlls_dbg"></span><span id="DDK__DLLS_DBG"></span>パラメーター


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *オプション*   
出力のレベルを指定します。 このパラメーターは、次の値の任意の組み合わせを指定できます。

<span id="-f"></span><span id="-F"></span>**-f**  
ファイルのヘッダーを表示します。

<span id="-s"></span><span id="-S"></span>**-s**  
セクション ヘッダーを表示します。

<span id="-a"></span><span id="-A"></span>**-**  
表示は、モジュールの情報を完了します。 (このオプションは、-f-s に相当) です。

<span id="-c_ModuleAddress"></span><span id="-c_moduleaddress"></span><span id="-C_MODULEADDRESS"></span>**-c** **** *ModuleAddress*  
含むモジュールを表示します。 *ModuleAddress*します。

<span id="-i"></span><span id="-I"></span>**-i**  
初期化の順序で表示を並べ替えます。

<span id="-l"></span><span id="-L"></span>**-l**  
表示の読み込み順序を並べ替えます。 このような状況では、既定値です。

<span id="-m"></span><span id="-M"></span>**-m**  
メモリの順序で表示を並べ替えます。

<span id="-v"></span><span id="-V"></span>**-v**  
バージョン情報を表示します。 この情報は、各モジュールのリソース セクションから取得されます。

<span id="_______LoaderEntryAddress______"></span><span id="_______loaderentryaddress______"></span><span id="_______LOADERENTRYADDRESS______"></span> *LoaderEntryAddress*   
モジュールのローダーのエントリのアドレスを指定します。 このパラメーターを含める場合、デバッガーは、この特定のモジュールのみを表示します。

<span id="_______-h______"></span><span id="_______-H______"></span> **-h**   
この拡張機能のいくつかのヘルプ テキストが表示されます、[デバッガー コマンド ウィンドウ](debugger-command-window.md)します。

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

 

<a name="remarks"></a>注釈
-------

モジュールの一覧には、各モジュールにすべてのエントリ ポイントが含まれています。

**.Dll**拡張機能が (クラッシュ ダンプ分析) ではなく、ライブ デバッグでのみ動作します。

カーネル モードでは、この拡張機能は、現在のモジュールが表示されます。[プロセス コンテキスト](changing-contexts.md#process-context)します。 使用することはできません **! dll**システム プロセスまたはアイドル状態のプロセスとします。

次の例は、使用する方法を示します、 **! dll**拡張機能。

```dbgcmd
kd> !dlls -c 77f60000
Dump dll containing 0x77f60000:

0x00091f38: E:\WINDOWS\System32\ntdll.dll
      Base   0x77f60000  EntryPoint  0x00000000  Size        0x00097000
      Flags  0x00004004  LoadCount   0x0000ffff  TlsIndex    0x00000000
             LDRP_IMAGE_DLL
             LDRP_ENTRY_PROCESSED

kd> !dlls -a 91ec0

0x00091ec0: E:\WINDOWS\system32\winmine.exe
      Base   0x01000000  EntryPoint  0x01003e2e  Size        0x00020000
      Flags  0x00005000  LoadCount   0x0000ffff  TlsIndex    0x00000000
             LDRP_LOAD_IN_PROGRESS
             LDRP_ENTRY_PROCESSED

File Type: EXECUTABLE IMAGE
FILE HEADER VALUES
     14C machine (i386)
       3 number of sections
3A98E856 time date stamp Sun Feb 25 03:11:18 2001

       0 file pointer to symbol table
       0 number of symbols
      E0 size of optional header
     10F characteristics
            Relocations stripped
            Executable
            Line numbers stripped
            Symbols stripped
            32 bit word machine

OPTIONAL HEADER VALUES
     10B magic #
    7.00 linker version
    3A00 size of code
   19E00 size of initialized data
       0 size of uninitialized data
    3E2E address of entry point
    1000 base of code
         ----- new -----
01000000 image base
    1000 section alignment
     200 file alignment
       2 subsystem (Windows GUI)
    5.01 operating system version
    5.01 image version
    4.00 subsystem version
   20000 size of image
     400 size of headers
   21970 checksum
00040000 size of stack reserve
00001000 size of stack commit
00100000 size of heap reserve
00001000 size of heap commit
01000100 Opt Hdr
       0 [       0] address [size] of Export Directory
    40B4 [      B4] address [size] of Import Directory
    6000 [   19170] address [size] of Resource Directory
       0 [       0] address [size] of Exception Directory
       0 [       0] address [size] of Security Directory
       0 [       0] address [size] of Base Relocation Directory
    11B0 [      1C] address [size] of Debug Directory
       0 [       0] address [size] of Description Directory
       0 [       0] address [size] of Special Directory
       0 [       0] address [size] of Thread Storage Directory
       0 [       0] address [size] of Load Configuration Directory
     258 [      A8] address [size] of Bound Import Directory
    1000 [     1B0] address [size] of Import Address Table Directory
       0 [       0] address [size] of Reserved Directory
       0 [       0] address [size] of Reserved Directory
       0 [       0] address [size] of Reserved Directory


SECTION HEADER #1
   .text name
    3992 virtual size
    1000 virtual address
    3A00 size of raw data
     400 file pointer to raw data
       0 file pointer to relocation table
       0 file pointer to line numbers
       0 number of relocations
       0 number of line numbers
60000020 flags
         Code
         (no align specified)
         Execute Read


Debug Directories(1)
        Type       Size     Address  Pointer

        cv           1c        13d0      7d0    Format: NB10, 3a98e856, 1, winmi
ne.pdb

SECTION HEADER #2
   .data name
     BB8 virtual size
    5000 virtual address
     200 size of raw data
    3E00 file pointer to raw data
       0 file pointer to relocation table
       0 file pointer to line numbers
       0 number of relocations
       0 number of line numbers
C0000040 flags
         Initialized Data
         (no align specified)
         Read Write

SECTION HEADER #3
   .rsrc name
   19170 virtual size
    6000 virtual address
   19200 size of raw data
    4000 file pointer to raw data
       0 file pointer to relocation table
       0 file pointer to line numbers
       0 number of relocations
       0 number of line numbers
40000040 flags
         Initialized Data
         (no align specified)
         Read Only
```

 

 






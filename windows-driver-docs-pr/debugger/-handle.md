---
title: ハンドル
description: ハンドルの拡張機能がハンドルに関する情報を表示またはそのいずれかの処理またはターゲット システムのすべてのプロセスを所有します。
ms.assetid: ae3b7e7e-cdc1-4b83-88d7-63fe207044e3
keywords:
- ハンドル
- ハンドル、ハンドルの拡張機能
- Windows デバッグ ハンドル
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- handle
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3e4d4c011d120c66d8cd9ade7d019832bf63cca6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336559"
---
# <a name="handle"></a>!handle


**! 処理**ターゲット システムのすべてのプロセスを所有または拡張機能は、ハンドルに関する情報を表示またはそのいずれかを処理します。

ユーザー モード

```dbgcmd
!handle [Handle [UMFlags [TypeName]]] 
!handle -?
```

カーネル モード

```dbgcmd
    !handle [Handle [KMFlags [Process [TypeName]]]] 
```

## <a name="span-idddkhandledbgspanspan-idddkhandledbgspanparameters"></a><span id="ddk__handle_dbg"></span><span id="DDK__HANDLE_DBG"></span>パラメーター


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span> *ハンドル*   
表示を識別するハンドルのインデックスを指定します。 場合*処理*は-1 です。 または、デバッガーが、現在のプロセスに関連付けられているすべてのハンドルのデータを表示するこのパラメーターを省略した場合。 場合*処理*が 0 の場合、デバッガーは、すべてのハンドルのデータを表示します。

<span id="_______UMFlags______"></span><span id="_______umflags______"></span><span id="_______UMFLAGS______"></span> *UMFlags*   
(ユーザー モードのみ)表示に含める必要がありますを指定します。 このパラメーターは、次のビット値のいずれかの合計を指定できます。 (既定値は 0x1 です)。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
型情報の処理が表示されます。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>ビット 1 (0x2)  
ハンドルの基本的な情報が表示されます。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>ビット 2 (0x4)  
表示名の情報を処理します。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>ビット 3 (0x8)  
オブジェクト固有のハンドルは、使用可能な場合に表示されます。

<span id="_______KMFlags______"></span><span id="_______kmflags______"></span><span id="_______KMFLAGS______"></span> *KMFlags*   
(カーネル モードのみ)表示に含める必要がありますを指定します。 このパラメーターは、次のビット値のいずれかの合計を指定できます。 (既定値は、0x3 です)。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
ハンドルの基本的な情報が表示されます。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>ビット 1 (0x2)  
オブジェクトに関する情報を表示します。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>ビット 2 (0x4)  
無料の表示では、エントリを処理します。 このビットを設定しないかどうかを省略して*処理*またはセット ハンドルを解放して 0、表示されるハンドルの一覧には含まれません。 場合*処理*、無料の単一のハンドルを指定します。 このビットを設定しない場合でも表示されます。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>ビット 4 (0x10)  
現在のプロセスではなくカーネル ハンドル テーブルからハンドルを表示します。

<span id="Bit_5__0x20_"></span><span id="bit_5__0x20_"></span><span id="BIT_5__0X20_"></span>Bit 5 (0x20)  
スレッド ID またはプロセス ID としてハンドルを解釈し、対応するカーネル オブジェクトに関する情報を表示します。

<span id="_______Process______"></span><span id="_______process______"></span><span id="_______PROCESS______"></span> *プロセス*   
(カーネル モードのみ)プロセスを指定します。 プロセス ID またはプロセス オブジェクトの 16 進数のアドレスを使用することができます。 このパラメーターは、ターゲット システムで現在実行中のプロセスを参照する必要があります。 このパラメーターが-1 の場合、または省略した場合は、現在のプロセスが使用されます。 このパラメーターが 0 の場合は、すべてのプロセスからのハンドルの情報が表示されます。

<span id="_______TypeName______"></span><span id="_______typename______"></span><span id="_______TYPENAME______"></span> *TypeName*   
確認するハンドルの種類を指定します。 この型に一致するハンドルのみが表示されます。 *TypeName*は大文字小文字を区別します。 有効な型イベント、セクション、ファイル、ポート、ディレクトリ、SymbolicLink、変異形、WindowStation、セマフォ、キー、トークン、プロセス、スレッド、デスクトップ、IoCompletion、タイマー、ジョブ、および含める WaitablePort します。

<span id="_______-_______"></span> **-?**   
(ユーザー モードのみ)この拡張機能のいくつかのヘルプ テキストが表示されます、[デバッガー コマンド ウィンドウ](debugger-command-window.md)します。

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
Kdextx86.dll Uext.dll Ntsdexts.dll</td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p></p>
Kdexts.dll Uext.dll Ntsdexts.dll</td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ハンドルの詳細については、次を参照してください、 [ **! htrace** ](-htrace.md)拡張機能、Microsoft Windows SDK のドキュメントと*Microsoft Windows internals 』* Mark Russinovich が、。David Solomon します。 (これらのリソースできない場合がありますのいくつかの言語および国。)

<a name="remarks"></a>注釈
-------

使用することができます、 **! 処理**ユーザー モードおよびカーネル モードのライブ デバッグ中に拡張します。 カーネル モードのダンプ ファイルでこの拡張機能を使用することもできます。 ただし、ハンドルの情報を具体的に作成していない場合は、ユーザー モード ダンプのファイルでこの拡張機能を使用できません。 (このようなダンプ ファイルを使用して作成することができます、 [ **.dump/mh (ダンプ ファイルの作成)** ](-dump--create-dump-file-.md)コマンド)。

ライブ ユーザー モードでは、デバッグ時に使用することができます、 [ **(ハンドルを閉じる) .closehandle** ](-closehandle--close-handle-.md) 1 つまたは複数のハンドルを閉じるコマンド。

次の例のユーザー モードの使用例、 **! 処理**拡張機能。 次のコマンドは、すべてのハンドルの一覧を表示します。

```dbgcmd
0:000> !handle
Handle 4
  Type          Section
Handle 8
  Type          Event
Handle c
  Type          Event
Handle 10
  Type          Event
Handle 14
  Type          Directory
Handle 5c
  Type          File
6 Handles
Type            Count
Event           3
Section         1
File            1
Directory       1
```

次のコマンドでは、ハンドル 0x8 に関する詳細情報が表示されます。

```dbgcmd
0:000> !handle 8 f
Handle 8
  Type          Event
  Attributes    0
  GrantedAccess 0x100003:
         Synch
         QueryState,ModifyState
  HandleCount   2
  PointerCount  3
  Name          <none>
  Object Specific Information
    Event Type Auto Reset
    Event is Waiting
```

次の例のカーネル モードの使用例 **! 処理**します。 次のコマンドでは、空きハンドルを含む、すべてのハンドルが一覧表示します。

```dbgcmd
kd> !handle 0 4
processor number 0
PROCESS 80559800  SessionId: 0  Cid: 0000    Peb: 00000000  ParentCid: 0000
    DirBase: 00039000  ObjectTable: e1000d60  TableSize: 380.
    Image: Idle

New version of handle table at e1002000 with 380 Entries in use

0000: free handle, Entry address e1002000, Next Entry fffffffe
0004: Object: 80ed5238  GrantedAccess: 001f0fff
0008: Object: 80ed46b8  GrantedAccess: 00000000
000c: Object: e1281d00  GrantedAccess: 000f003f
0010: Object: e1013658  GrantedAccess: 00000000
......
0168: Object: ffb6c748  GrantedAccess: 00000003 (Protected)
016c: Object: ff811f90  GrantedAccess: 0012008b
0170: free handle, Entry address e10022e0, Next Entry 00000458
0174: Object: 80dfd5c8  GrantedAccess: 001f01ff
......
```

次のコマンドは、カーネル ハンドル テーブル内のハンドル 0x14 に関する詳細情報を表示します。

```dbgcmd
kd> !handle 14 13
processor number 0
PROCESS 80559800  SessionId: 0  Cid: 0000    Peb: 00000000  ParentCid: 0000
    DirBase: 00039000  ObjectTable: e1000d60  TableSize: 380.
    Image: Idle

Kernel New version of handle table at e1002000 with 380 Entries in use
0014: Object: e12751d0  GrantedAccess: 0002001f
Object: e12751d0  Type: (80ec8db8) Key
    ObjectHeader: e12751b8
        HandleCount: 1  PointerCount: 1
        Directory Object: 00000000  Name: \REGISTRY\MACHINE\SYSTEM\CONTROLSET001\CONTROL\SESSION MANAGER\EXECUTIVE
```

次のコマンドは、すべてのプロセスでセクション オブジェクトに対してすべてのハンドルに関する情報を示します。

```dbgcmd
!handle 0 3 0 Section
...
PROCESS fffffa8004f48940
    SessionId: none  Cid: 0138    Peb: 7f6639bf000  ParentCid: 0004
    DirBase: 10cb74000  ObjectTable: fffff8a00066f700  HandleCount:  39.
    Image: smss.exe

Handle table at fffff8a00066f700 with 39 entries in use

0040: Object: fffff8a000633f00  GrantedAccess: 00000006 (Inherit) Entry: fffff8a000670100
Object: fffff8a000633f00  Type: (fffffa80035fef20) Section
    ObjectHeader: fffff8a000633ed0 (new version)
        HandleCount: 1  PointerCount: 262144
...
```

 

 






---
title: ハンドル
description: ハンドルの拡張機能には、ターゲットシステム内の1つまたはすべてのプロセスが所有するハンドルまたはハンドルに関する情報が表示されます。
ms.assetid: ae3b7e7e-cdc1-4b83-88d7-63fe207044e3
keywords:
- ハンドル
- ハンドル、ハンドル拡張機能
- Windows のデバッグを処理する
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- handle
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f0f1b81b8f88633f7d64fe6e245f1917fa0ceb71
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025240"
---
# <a name="handle"></a>!handle


**! ハンドル**拡張機能には、ターゲットシステム内の1つまたはすべてのプロセスが所有するハンドルまたはハンドルに関する情報が表示されます。

ユーザーモード

```dbgcmd
!handle [Handle [UMFlags [TypeName]]] 
!handle -?
```

カーネルモード

```dbgcmd
    !handle [Handle [KMFlags [Process [TypeName]]]] 
```

## <a name="span-idddk__handle_dbgspanspan-idddk__handle_dbgspanparameters"></a><span id="ddk__handle_dbg"></span><span id="DDK__HANDLE_DBG"></span>パラメータ


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span>*ハンドル*   
表示するハンドルのインデックスを指定します。 *Handle*が-1 の場合、またはこのパラメーターを省略した場合、デバッガーは、現在のプロセスに関連付けられているすべてのハンドルのデータを表示します。 *Handle*が0の場合、デバッガーはすべてのハンドルのデータを表示します。

<span id="_______UMFlags______"></span><span id="_______umflags______"></span><span id="_______UMFLAGS______"></span>*Umflags*   
(ユーザーモードのみ)表示に含める内容を指定します。 このパラメーターには、次のいずれかのビット値を合計することができます。 (既定値は0x1 です)。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
ハンドルの種類の情報を表示します。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>ビット 1 (0x2)  
基本的なハンドル情報を表示します。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>ビット 2 (0x4)  
ハンドル名の情報を表示します。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>ビット 3 (0x8)  
オブジェクト固有のハンドル情報 (使用可能な場合) を表示します。

<span id="_______KMFlags______"></span><span id="_______kmflags______"></span><span id="_______KMFLAGS______"></span>*KMFlags*   
(カーネルモードのみ)表示に含める内容を指定します。 このパラメーターには、次のいずれかのビット値を合計することができます。 (既定値は0x3 です)。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
基本的なハンドル情報を表示します。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>ビット 1 (0x2)  
オブジェクトに関する情報を表示します。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>ビット 2 (0x4)  
空きハンドルエントリを表示します。 このビットを設定せず、 *Handle*を省略した場合、または0に設定した場合、表示されるハンドルの一覧には、空きハンドルは含まれません。 *Handle*が1つのフリーハンドルを指定すると、このビットを設定しない場合でも表示されます。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>ビット 4 (0x10)  
現在のプロセスではなく、カーネルハンドルテーブルからのハンドルを表示します。

<span id="Bit_5__0x20_"></span><span id="bit_5__0x20_"></span><span id="BIT_5__0X20_"></span>ビット 5 (0x20)  
ハンドルをスレッド ID またはプロセス ID として解釈し、対応するカーネルオブジェクトに関する情報を表示します。

<span id="_______Process______"></span><span id="_______process______"></span><span id="_______PROCESS______"></span>*プロセス*   
(カーネルモードのみ)プロセスを指定します。 プロセスオブジェクトのプロセス ID または16進数のアドレスを使用できます。 このパラメーターは、ターゲットシステムで現在実行中のプロセスを参照する必要があります。 このパラメーターが-1 の場合、またはこのパラメーターを省略した場合は、現在のプロセスが使用されます。 このパラメーターが0の場合、すべてのプロセスの情報を処理します。

<span id="_______TypeName______"></span><span id="_______typename______"></span><span id="_______TYPENAME______"></span>*TypeName*   
確認するハンドルの種類を指定します。 この型に一致するハンドルのみが表示されます。 *TypeName*では大文字と小文字が区別されます。 有効な型には、Event、Section、File、Port、Directory、SymbolicLink、ミュータント、WindowStation、セマフォ、Key、Token、Process、Thread、Desktop、IoCompletion、Timer、Job、および WaitablePort があります。

<span id="_______-_______"></span> **-?**    
(ユーザーモードのみ)[デバッガーコマンドウィンドウ](debugger-command-window.md)にこの拡張機能のヘルプテキストを表示します。

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
Kdextx86 Usdexを .dll にします。</td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p></p>
Kdexts .dll Uext .dll (.dll)</td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ハンドルの詳細については、 [ **! htrace**](-htrace.md)拡張機能、Microsoft Windows SDK のドキュメント、および*Microsoft Windows の内部構造*(Mark Russinovich と David ソロモン) を参照してください。

<a name="remarks"></a>コメント
-------

ユーザーモードとカーネルモードのライブデバッグ中に、 **! handle**拡張機能を使用できます。 この拡張機能は、カーネルモードのダンプファイルでも使用できます。 ただし、ハンドル情報を使用して明示的に作成しない限り、ユーザーモードのダンプファイルでこの拡張機能を使用することはできません。 (ダンプファイルを作成するには、 [ **. dump/mh (ダンプファイルの作成)** ](-dump--create-dump-file-.md)コマンドを使用します)。

ユーザーモードのライブデバッグ時には、 [**closehandle (ハンドルを閉じる)** ](-closehandle--close-handle-.md)コマンドを使用して1つ以上のハンドルを閉じることができます。

次の例は、 **! handle**拡張機能のユーザーモードの例です。 次のコマンドは、すべてのハンドルの一覧を表示します。

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

次のコマンドは、0x8 を処理するための詳細情報を表示します。

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

次の例は、 **! handle**のカーネルモードの例です。 次のコマンドは、すべてのハンドル (無料ハンドルを含む) を一覧表示します。

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

次のコマンドは、カーネルハンドルテーブルの0x14 の処理に関する詳細情報を表示します。

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

次のコマンドは、すべてのプロセスのセクションオブジェクトへのすべてのハンドルに関する情報を表示します。

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

 

 






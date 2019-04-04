---
title: cs
description: Cs 拡張機能には、1 つまたは複数の重要なセクションまたは全体のクリティカル セクションのツリーが表示されます。
ms.assetid: 767ad508-013b-4cf7-808d-38ff64418879
keywords:
- Windows デバッグ cs
ms.date: 11/15/2018
topic_type:
- apiref
api_name:
- cs
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f50f65fd8f710b6457e259d458d8aca995f0b394
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578624"
---
# <a name="cs"></a>!cs


**! Cs**拡張機能は、1 つまたは複数の重要なセクションまたは全体のクリティカル セクションのツリーが表示されます。

```dbgsyntax
!cs [-s] [-l] [-o] 
!cs [-s] [-o] Address 
!cs [-s] [-l] [-o] StartAddress EndAddress 
!cs [-s] [-o] -d InfoAddress 
!cs [-s] -t [TreeAddress] 
!cs -? 
```

## <a name="parameters"></a>パラメーター

パラメーター | 説明
|---------|-------------|
**-s**  | この情報は、使用可能な場合は、各クリティカル セクションの初期化のスタック トレースを表示します。
**-l**  |ロックされたクリティカル セクションのみを表示します。
**-o**   |表示されているすべてのロックされたクリティカル セクションの所有者のスタックを表示します。
*アドレス* |表示するクリティカル セクションのアドレスを指定します。 このパラメーターを省略した場合、デバッガーには、現在のプロセスですべての重要なセクションが表示されます。
*StartAddress*   | クリティカル セクションを検索するアドレス範囲の先頭を指定します。
*endAddress*   | クリティカル セクションを検索するアドレス範囲の末尾を指定します。
**-d**    | DebugInfo に関連付けられている重要なセクションが表示されます。
*InfoAddress*   | DebugInfo のアドレスを指定します。
**-t**    | クリティカル セクションのツリーが表示されます。 使用する前に、 **-t**アクティブ化する必要がありますオプション、 [Application Verifier](application-verifier.md)を選択して対象プロセス、**ロックの使用状況をチェック**オプション。
*TreeAddress*    | クリティカル セクションのツリーのルートのアドレスを指定します。 このパラメーターを省略して、0 を指定するか、デバッガーには、現在のプロセスのクリティカル セクションのツリーが表示されます。
**-?**    | この拡張機能のいくつかのヘルプ テキストが表示されます、[デバッガー コマンド ウィンドウ](debugger-command-window.md)します。

### <a name="dll"></a>DLL

Exts.dll
 

### <a name="additional-information"></a>追加情報

その他のコマンドとクリティカル セクションの情報を表示できる拡張機能では、[クリティカル セクションを表示する](displaying-a-critical-section.md)を参照してください。 クリティカル セクションの詳細については、Microsoft Windows SDK ドキュメントに、Windows Driver Kit (WDK) ドキュメントを参照してくださいと*Microsoft Windows internals 』* Mark Russinovich と David Solomon します。 

#### <a name="remarks"></a>コメント

**! Cs**拡張機能は、デバッグ中のプロセス、Ntdll.dll (型情報を含む) 完全なシンボルが必要です。 Ntdll.dll のシンボルがないを参照してください。 [Windows シンボル ファイルのインストール](installing-windows-symbol-files.md)します。

次の例は、使用する方法を示します **! cs**します。 次のコマンドは、アドレス 0x7803B0F8 にクリティカル セクションに関する情報を表示し、その初期化のスタック トレースを示します。

```dbgcmd
0:001> !cs -s 0x7803B0F8
Critical section   = 0x7803B0F8 (MSVCRT!__app_type+0x4)
DebugInfo          = 0x6A262080
NOT LOCKED
LockSemaphore      = 0x0
SpinCount          = 0x0

Stack trace for DebugInfo = 0x6A262080:

0x6A2137BD: ntdll!RtlInitializeCriticalSectionAndSpinCount+0x9B
0x6A207A4C: ntdll!LdrpCallInitRoutine+0x14
0x6A205569: ntdll!LdrpRunInitializeRoutines+0x1D9
0x6A20DCE1: ntdll!LdrpInitializeProcess+0xAE5
```

次のコマンドは、ある DebugInfo が 0x6A262080 アドレスでは、クリティカル セクションの情報を表示します。

```dbgcmd
0:001> !cs -d 0x6A262080
DebugInfo          = 0x6A262080
Critical section   = 0x7803B0F8 (MSVCRT!__app_type+0x4)
NOT LOCKED
LockSemaphore      = 0x0
SpinCount          = 0x0
```

次のコマンドでは、現在のプロセスの中にすべてのアクティブな重要なセクションについての情報が表示されます。

```dbgcmd
## 0:001> !cs

DebugInfo          = 0x6A261D60
Critical section   = 0x6A262820 (ntdll!RtlCriticalSectionLock+0x0)
LOCKED
LockCount          = 0x0
OwningThread       = 0x460
RecursionCount     = 0x1
LockSemaphore      = 0x0
## SpinCount          = 0x0

DebugInfo          = 0x6A261D80
Critical section   = 0x6A262580 (ntdll!DeferedCriticalSection+0x0)
NOT LOCKED
LockSemaphore      = 0x7FC
## SpinCount          = 0x0

DebugInfo          = 0x6A262600
Critical section   = 0x6A26074C (ntdll!LoaderLock+0x0)
NOT LOCKED
LockSemaphore      = 0x0
## SpinCount          = 0x0

DebugInfo          = 0x77fbde20
Critical section   = 0x77c8ba60 (GDI32!semColorSpaceCache+0x0)
LOCKED
LockCount          = 0x0
OwningThread       = 0x00000dd8
RecursionCount     = 0x1
LockSemaphore      = 0x0
## SpinCount          = 0x00000000

...
```

次のコマンドは、クリティカル セクションのツリーを表示します。

```dbgcmd
0:001> !cs -t

Tree root 00bb08c0

Level     Node       CS    Debug  InitThr EnterThr  WaitThr TryEnThr LeaveThr EnterCnt  WaitCnt
## 


    0 00bb08c0 77c7e020 77fbcae0      4c8      4c8        0        0      4c8        c        0
 1 00dd6fd0 0148cfe8 01683fe0      4c8      4c8        0        0      4c8        2        0
 2 00bb0aa0 008e8b84 77fbcc20      4c8        0        0        0        0        0        0
    3 00bb09e0 008e8704 77fbcba0      4c8        0        0        0        0        0        0
    4 00bb0a40 008e8944 77fbcbe0      4c8        0        0        0        0        0        0
    5 00bb0a10 008e8824 77fbcbc0      4c8        0        0        0        0        0        0
    5 00bb0a70 008e8a64 77fbcc00      4c8        0        0        0        0        0        0
    3 00bb0b00 008e8dc4 77fbcc60      4c8        0        0        0        0        0        0
    4 00bb0ad0 008e8ca4 77fbcc40      4c8        0        0        0        0        0        0
    4 00bb0b30 008e8ee4 77fbcc80      4c8        0        0        0        0        0        0
    5 00dd4fd0 0148afe4 0167ffe0      4c8        0        0        0        0        0        0
    2 00bb0e90 77c2da98 00908fe0      4c8      4c8        0        0      4c8       3a        0
 3 00bb0d70 77c2da08 008fcfe0      4c8        0        0        0        0        0        0
```

これで、次のものが表示される **! cs t**表示。

-   **InitThr**は CS を初期化したスレッドのスレッド ID です。

-   **EnterThr**を呼び出したスレッドの id **EnterCriticalSection**最後の時間します。

-   **WaitThr**がクリティカル セクションの他のスレッドを検出したスレッドの ID で所有し、最後の時間を待機します。

-   **TryEnThr**を呼び出したスレッドの id **TryEnterCriticalSection**最後の時間します。

-   **LeaveThr**を呼び出したスレッドの id**により**最後の時間

-   **EnterCnt**の数は、 **EnterCriticalSection**します。

-   **WaitCnt**は競合の数です。



 






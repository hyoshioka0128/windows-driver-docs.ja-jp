---
title: クリティカル セクションを表示します。
description: クリティカル セクションを表示します。
ms.assetid: d55971f6-9112-417d-8fb6-e299c7fc90a7
keywords:
- クリティカル セクション
- クリティカル セクション、概要
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 625a4c5361746a3c3e56a3c1cc174b28c76dad20
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538060"
---
# <a name="displaying-a-critical-section"></a>クリティカル セクションを表示します。


## <span id="ddk_displaying_a_critical_section_dbg"></span><span id="DDK_DISPLAYING_A_CRITICAL_SECTION_DBG"></span>


重要なセクションは、さまざまな方法でユーザー モードで表示できます。 各フィールドの正確な意味は、使用している Microsoft Windows のバージョンによって異なります。

### <a name="span-iddisplayingcriticalsectionsspanspan-iddisplayingcriticalsectionsspandisplaying-critical-sections"></a><span id="displaying_critical_sections"></span><span id="DISPLAYING_CRITICAL_SECTIONS"></span>クリティカル セクションを表示します。

クリティカル セクションを表示できます、 **! ntsdexts.locks**拡張機能を **! critsec**拡張機能を **! cs**拡張機能、および**dt (表示の種類)** コマンド。

[ **! Ntsdexts.locks** ](-locks---ntsdexts-locks-.md)拡張機能は、現在のプロセスに関連付けられているクリティカル セクションの一覧を表示します。 場合、 **-v**オプションが使用される、すべての重要なセクションが表示されます。 以下に例を示します。

```dbgcmd
0:000> !locks

CritSec ntdll!FastPebLock+0 at 77FC49E0
LockCount          0
RecursionCount     1
OwningThread       c78
EntryCount         0
ContentionCount    0
*** Locked

....
Scanned 37 critical sections
```

使用することができますを表示する、クリティカル セクションのアドレスがわかっている場合、 [ **! critsec** ](-critsec.md)拡張機能。 これにより、情報の同じコレクションが表示されます。 **! ntsdexts.locks**します。 次に、例を示します。

```dbgcmd
0:000> !critsec 77fc49e0

CritSec ntdll!FastPebLock+0 at 77FC49E0
LockCount          0
RecursionCount     1
OwningThread       c78
EntryCount         0
ContentionCount    0
*** Locked
```

[ **! Cs** ](-cs.md)拡張機能は、そのアドレスに基づいてクリティカル セクションを表示、クリティカル セクションは、アドレス範囲を検索、および各クリティカル セクションに関連付けられたスタック トレースを表示することもできます。 これらの機能の一部には、適切に機能する完全な Windows シンボルが必要です。 Application Verifier は、アクティブな場合 **! cs t**クリティカル セクションのツリーを表示するために使用できます。 参照してください、 **! cs**リファレンス ページの詳細と例。

によって表示される情報 **! cs**は若干異なるで示されている **! ntsdexts.locks**と **! critsec**します。 次に、例を示します。

```dbgcmd
## 0:000> !cs 77fc49e0

Critical section   = 0x77fc49e0 (ntdll!FastPebLock+0x0)
DebugInfo          = 0x77fc3e00
LOCKED
LockCount          = 0x0
OwningThread       = 0x00000c78
RecursionCount     = 0x1
LockSemaphore      = 0x0
SpinCount          = 0x00000000
```

[ **Dt (型の表示)** ](dt--display-type-.md) 、右から左へのリテラルの内容を表示するコマンドを使用できます\_重大\_セクションの構造体。 次に、例を示します。

```dbgcmd
0:000> dt RTL_CRITICAL_SECTION 77fc49e0
   +0x000 DebugInfo        : 0x77fc3e00 
   +0x004 LockCount        : 0
   +0x008 RecursionCount   : 1
   +0x00c OwningThread     : 0x00000c78 
   +0x010 LockSemaphore    : (null) 
   +0x014 SpinCount        : 0
```

### <a name="span-idinterpretingcriticalsectionfieldsinwindowsxpandwindows2000spanspan-idinterpretingcriticalsectionfieldsinwindowsxpandwindows2000spaninterpreting-critical-section-fields-in-windows-xp-and-windows-2000"></a><span id="interpreting_critical_section_fields_in_windows_xp_and_windows_2000"></span><span id="INTERPRETING_CRITICAL_SECTION_FIELDS_IN_WINDOWS_XP_AND_WINDOWS_2000"></span>クリティカル セクションのフィールドでは、Windows XP および Windows 2000 の解釈

クリティカル セクションの構造体の最も重要なフィールドは次のとおりです。

-   Microsoft Windows 2000、および Windows XP、 **LockCount**フィールドは、任意のスレッドが呼び出される回数を示します、 **EnterCriticalSection**から 1 を引いたこの重要なセクションの日常的な。 このフィールドは、ロック解除のクリティカル セクションに達すると-1 から開始されます。 各呼び出し**EnterCriticalSection**このインクリメント値以外の各呼び出し**により**デクリメントこと。 たとえば場合、 **LockCount** 5 は、この重要なセクションがロックされている、1 つのスレッドが取得した、および追加の 5 つのスレッドは、このロックを待機しています。

-   **RecursionCount**フィールドを所有しているスレッドが呼び出される回数を示します**EnterCriticalSection**ここで重要です。

-   **EntryCount**フィールドを所有しているスレッド以外のスレッドが呼び出される回数を示します**EnterCriticalSection**ここで重要です。

新しく初期化されたクリティカル セクションのようになります。

```dbgcmd
0:000> !critsec 433e60
CritSec mymodule!cs+0 at 00433E60
LockCount          NOT LOCKED 
RecursionCount     0
OwningThread       0
EntryCount         0
ContentionCount    0
```

デバッガーを表示する「ロックされていない」の値として**LockCount**します。 ロック解除のクリティカル セクションには、このフィールドの実際の値は-1 です。 これを確認する、 **dt (表示の種類)** コマンド。

```dbgcmd
0:000> dt RTL_CRITICAL_SECTION 433e60
   +0x000 DebugInfo        : 0x77fcec80
   +0x004 LockCount        : -1
   +0x008 RecursionCount   : 0
   +0x00c OwningThread     : (null) 
   +0x010 LockSemaphore    : (null) 
   +0x014 SpinCount        : 0
```

最初のスレッドを呼び出すと、 **EnterCriticalSection**ルーチン、クリティカル セクションの**LockCount**、 **RecursionCount**、 **EntryCount**と**ContentionCount**フィールドはすべて、1 つずつインクリメントし、 **OwningThread**呼び出し元のスレッド ID になります。 **EntryCount**と**ContentionCount**が差し引かれることはありません。 次に、例を示します。

```dbgcmd
0:000> !critsec 433e60
CritSec mymodule!cs+0 at 00433E60
LockCount          0
RecursionCount     1
OwningThread       4d0
EntryCount         0
ContentionCount    0
```

この時点では、4 つの異なる処理が行われますことができます。

1.  所有しているスレッド呼び出し**EnterCriticalSection**もう一度です。 これが増分**LockCount**と**RecursionCount**します。 **EntryCount**は加算されません。

    ```dbgcmd
    0:000> !critsec 433e60
    CritSec mymodule!cs+0 at 00433E60
    LockCount          1
    RecursionCount     2
    OwningThread       4d0
    EntryCount         0
    ContentionCount    0
    ```

2.  別のスレッドを呼び出す**EnterCriticalSection**します。 これが増分**LockCount**と**EntryCount**します。 **RecursionCount**は加算されません。

    ```dbgcmd
    0:000> !critsec 433e60
    CritSec mymodule!cs+0 at 00433E60
    LockCount          1
    RecursionCount     1
    OwningThread       4d0
    EntryCount         1
    ContentionCount    1
    ```

3.  所有しているスレッド呼び出し**により**します。 これをデクリメントする**LockCount** (-1) と**RecursionCount** (0) にはリセットと**OwningThread**を 0 にします。

    ```dbgcmd
    0:000> !critsec 433e60
    CritSec mymodule!cs+0 at 00433E60
    LockCount          NOT LOCKED 
    RecursionCount     0
    OwningThread       0
    EntryCount         0
    ContentionCount    0
    ```

4.  別のスレッド呼び出し**により**します。 所有しているスレッドの呼び出し元と同じ結果が生成されます**により**--デクリメントすること**LockCount** (-1) と**RecursionCount** (0) にリセットされます**OwningThread**を 0 にします。

ときにいずれかのスレッド呼び出し**により**、Windows デクリメント**LockCount**と**RecursionCount**します。 この機能は、長所も短所の側面があります。 デバイス ドライバーを 1 つのスレッドのクリティカル セクションを入力し、別のスレッドで、クリティカル セクションのままにできます。 ただし、これもできるようになりますを誤って呼び出す**により**間違ったスレッド、または呼び出す**により**多くの時間と原因**LockCount**-1 より小さい値に到達します。 これは、重要なセクションが破損し、クリティカル セクションを無制限に待機するすべてのスレッド。

### <a name="span-idinterpretingcriticalsectionfieldsinwindowsserver2003sp1andlaspanspan-idinterpretingcriticalsectionfieldsinwindowsserver2003sp1andlaspaninterpreting-critical-section-fields-in-windows-server-2003-sp1-and-later"></a><span id="interpreting_critical_section_fields_in_windows_server_2003_sp1_and_la"></span><span id="INTERPRETING_CRITICAL_SECTION_FIELDS_IN_WINDOWS_SERVER_2003_SP1_AND_LA"></span>Windows Server 2003 SP1 以降、クリティカル セクションのフィールドの解釈

Microsoft Windows Server 2003 Service Pack 1、Windows の以降のバージョンで、 **LockCount**フィールドは次のように解析されます。

-   最下位ビットは、ロックの状態を示しています。 このビットが 0 の場合、クリティカル セクションがロックされています。1 の場合は、クリティカル セクションをロックしません。

-   次のビットは、このロックのスレッドがウェイク アップされているかどうかを示します。 このビットが 0 の場合、スレッドがされてウェイク; このロック1 の場合は、スレッドをウェイクされてはありません。

-   残りのビットは、ロックを待機しているスレッドの数の補数です。

例として、たとえば、 **LockCount**は ~ 22 日。 最下位ビットは、この方法で決定できます。

```dbgcmd
0:009> ? 0x1 & (-0n22)
Evaluate expression: 0 = 00000000
```

この方法で、[次へ] の最下位ビットを決定できます。

```dbgcmd
0:009> ? (0x2 & (-0n22)) >> 1
Evaluate expression: 1 = 00000001
```

残りのビットの 1 の補数は、この方法で決定できます。

```dbgcmd
0:009> ? ((-1) - (-0n22)) >> 2
Evaluate expression: 5 = 00000005
```

この例では、最初のビットが 0 とクリティカル セクションがロックされているためです。 2 番目のビットは 1 であり、ためスレッドがされてウェイク アップしないこのロック。 残りのビットの補数は 5 であり、これがこのロックを待機している 5 つのスレッド。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

クリティカル セクションのタイムアウトをデバッグする方法については、次を参照してください。[クリティカル セクション タイムアウト](critical-section-time-outs.md)します。 重要なセクションについては、Microsoft Windows SDK、Windows Driver Kit (WDK) を参照してください。 または*Microsoft Windows internals 』* Mark Russinovich と David Solomon します。 (これらのリソースできない場合がありますのいくつかの言語および国。)

 

 






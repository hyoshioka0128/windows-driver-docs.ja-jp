---
title: クリティカル セクションの表示
description: クリティカル セクションの表示
ms.assetid: d55971f6-9112-417d-8fb6-e299c7fc90a7
keywords:
- クリティカルセクション
- クリティカルセクション、概要
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8de3960552ca94b1f53e30f741bbcd16ba4a14ba
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025312"
---
# <a name="displaying-a-critical-section"></a>クリティカル セクションの表示


## <span id="ddk_displaying_a_critical_section_dbg"></span><span id="DDK_DISPLAYING_A_CRITICAL_SECTION_DBG"></span>


重要なセクションは、さまざまな方法でユーザーモードで表示できます。 各フィールドの正確な意味は、使用している Microsoft Windows のバージョンによって異なります。

### <a name="span-iddisplaying_critical_sectionsspanspan-iddisplaying_critical_sectionsspandisplaying-critical-sections"></a><span id="displaying_critical_sections"></span><span id="DISPLAYING_CRITICAL_SECTIONS"></span>表示 (クリティカルセクションを)

クリティカルセクションは、 **! ntsdexts. locks**拡張機能、 **! critsec**拡張機能、 **! cs**拡張機能、および**dt (Display Type)** コマンドで表示できます。

[ **! Ntsdexts**](-locks---ntsdexts-locks-.md)拡張子は、現在のプロセスに関連付けられているクリティカルセクションの一覧を表示します。 **-V**オプションを使用すると、すべての重要なセクションが表示されます。 以下に例を示します。

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

表示するクリティカルセクションのアドレスがわかっている場合は、 [ **! critsec**](-critsec.md)拡張機能を使用できます。 これにより、と同じ情報のコレクションが **! ntsdexts**に表示されます。 次に、例を示します。

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

[ **! Cs**](-cs.md)拡張機能では、アドレスに基づいてクリティカルセクションを表示したり、重要なセクションのアドレス範囲を検索したり、各クリティカルセクションに関連付けられているスタックトレースを表示したりすることができます。 これらの機能の中には、完全な Windows シンボルが正常に機能するために必要なものもあります。 アプリケーション検証ツールがアクティブである場合は、 **! cs-t**を使用してクリティカルセクションツリーを表示できます。 詳細と例については、「 **! cs**リファレンス」ページを参照してください。

**! Cs**によって表示される情報は、 **! ntsdexts. locks**および **! critsec**とは少し異なります。 次に、例を示します。

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

[ [**Dt (Display Type)** ](dt--display-type-.md) ] コマンドを使用すると、RTL\_クリティカル\_セクション構造のリテラルコンテンツを表示できます。 次に、例を示します。

```dbgcmd
0:000> dt RTL_CRITICAL_SECTION 77fc49e0
   +0x000 DebugInfo        : 0x77fc3e00 
   +0x004 LockCount        : 0
   +0x008 RecursionCount   : 1
   +0x00c OwningThread     : 0x00000c78 
   +0x010 LockSemaphore    : (null) 
   +0x014 SpinCount        : 0
```

### <a name="span-idinterpreting_critical_section_fields_in_windows_xp_and_windows_2000spanspan-idinterpreting_critical_section_fields_in_windows_xp_and_windows_2000spaninterpreting-critical-section-fields-in-windows-xp-and-windows-2000"></a><span id="interpreting_critical_section_fields_in_windows_xp_and_windows_2000"></span><span id="INTERPRETING_CRITICAL_SECTION_FIELDS_IN_WINDOWS_XP_AND_WINDOWS_2000"></span>Windows XP および Windows 2000 での重要なセクションフィールドの解釈

クリティカルセクションの構造の最も重要なフィールドは次のとおりです。

-   Microsoft Windows 2000 および Windows XP では、 **[Lockcount]** フィールドは、スレッドがこのクリティカルセクションの**EnterCriticalSection**ルーチンを呼び出した回数-1 を引いた回数を示します。 このフィールドは、ロック解除されたクリティカルセクションの場合は-1 から始まります。 **EnterCriticalSection**を呼び出すたびに、この値が増加します。**LeaveCriticalSection**を呼び出すたびに、それがデクリメントされます。 たとえば、 **Lockcount**が5の場合、このクリティカルセクションはロックされ、1つのスレッドがそれを取得し、5つの追加スレッドがこのロックを待機しています。

-   **RecursionCount**フィールドは、所有しているスレッドがこのクリティカルセクションの**EnterCriticalSection**を呼び出した回数を示します。

-   **Entrycount**フィールドは、所有スレッド以外のスレッドがこのクリティカルセクションの**EnterCriticalSection**を呼び出した回数を示します。

新しく初期化されたクリティカルセクションは次のようになります。

```dbgcmd
0:000> !critsec 433e60
CritSec mymodule!cs+0 at 00433E60
LockCount          NOT LOCKED 
RecursionCount     0
OwningThread       0
EntryCount         0
ContentionCount    0
```

デバッガーでは、 **Lockcount**の値として "NOT LOCKED" と表示されます。 ロック解除されたクリティカルセクションのこのフィールドの実際の値は-1 です。 これを確認するには、 **dt (Display Type)** コマンドを使用します。

```dbgcmd
0:000> dt RTL_CRITICAL_SECTION 433e60
   +0x000 DebugInfo        : 0x77fcec80
   +0x004 LockCount        : -1
   +0x008 RecursionCount   : 0
   +0x00c OwningThread     : (null) 
   +0x010 LockSemaphore    : (null) 
   +0x014 SpinCount        : 0
```

最初のスレッドが**EnterCriticalSection**ルーチンを呼び出すと、クリティカルセクションの**lockcount**、 **RecursionCount**、 **entrycount** 、および**ContentionCount**の各フィールドがすべて1つずつインクリメントされ、 **OwningThread**は、呼び出し元のスレッド ID になります。 **Entrycount**と**ContentionCount**はデクリメントされません。 次に、例を示します。

```dbgcmd
0:000> !critsec 433e60
CritSec mymodule!cs+0 at 00433E60
LockCount          0
RecursionCount     1
OwningThread       4d0
EntryCount         0
ContentionCount    0
```

この時点で、4つの異なることが発生する可能性があります。

1.  所有スレッドは**EnterCriticalSection**を再度呼び出します。 これにより、 **Lockcount**と**RecursionCount**がインクリメントされます。 **Entrycount**はインクリメントされません。

    ```dbgcmd
    0:000> !critsec 433e60
    CritSec mymodule!cs+0 at 00433E60
    LockCount          1
    RecursionCount     2
    OwningThread       4d0
    EntryCount         0
    ContentionCount    0
    ```

2.  別のスレッドが**EnterCriticalSection**を呼び出しています。 これにより、 **lockcount**と**entrycount**がインクリメントされます。 **RecursionCount**はインクリメントされません。

    ```dbgcmd
    0:000> !critsec 433e60
    CritSec mymodule!cs+0 at 00433E60
    LockCount          1
    RecursionCount     1
    OwningThread       4d0
    EntryCount         1
    ContentionCount    1
    ```

3.  所有スレッドが**LeaveCriticalSection**を呼び出します。 これにより、 **Lockcount** (-1) と**RecursionCount** (0) が減少し、 **OwningThread**が0にリセットされます。

    ```dbgcmd
    0:000> !critsec 433e60
    CritSec mymodule!cs+0 at 00433E60
    LockCount          NOT LOCKED 
    RecursionCount     0
    OwningThread       0
    EntryCount         0
    ContentionCount    0
    ```

4.  別のスレッドが**LeaveCriticalSection**を呼び出しています。 これにより、 **LeaveCriticalSection**を呼び出している所有スレッドと同じ結果が生成されます。これにより、 **lockcount** (-1) と**RecursionCount** (0) が減少し、 **OwningThread**が0にリセットされます。

いずれかのスレッドが**LeaveCriticalSection**を呼び出すと、Windows は**Lockcount**と**RecursionCount**をデクリメントします。 この機能には、優れた側面と悪い面があります。 これにより、デバイスドライバーが1つのスレッドにクリティカルセクションを入力し、クリティカルセクションを別のスレッドに残しておくことができます。 ただし、間違ったスレッドで誤って**LeaveCriticalSection**を呼び出したり、 **LeaveCriticalSection**を何度も呼び出して、 **lockcount**が-1 より小さい値になるようにしたりすることもできます。 これにより、クリティカルセクションが破損し、すべてのスレッドがクリティカルセクションで無制限に待機します。

### <a name="span-idinterpreting_critical_section_fields_in_windows_server_2003_sp1_and_laspanspan-idinterpreting_critical_section_fields_in_windows_server_2003_sp1_and_laspaninterpreting-critical-section-fields-in-windows-server-2003-sp1-and-later"></a><span id="interpreting_critical_section_fields_in_windows_server_2003_sp1_and_la"></span><span id="INTERPRETING_CRITICAL_SECTION_FIELDS_IN_WINDOWS_SERVER_2003_SP1_AND_LA"></span>Windows Server 2003 SP1 以降の重要なセクションフィールドの解釈

Microsoft Windows Server 2003 Service Pack 1 以降のバージョンの Windows では、 **Lockcount**フィールドは次のように解析されます。

-   最下位のビットは、ロックの状態を示します。 このビットが0の場合、クリティカルセクションはロックされています。1の場合、クリティカルセクションはロックされていません。

-   次のビットは、スレッドがこのロックに対してウェイクアップされているかどうかを示します。 このビットが0の場合、スレッドはこのロックに対してウェイクアップされています。1の場合、スレッドはウェイクアップされていません。

-   残りのビットは、ロックを待機しているスレッドの数の 1 ~ 補数です。

例として、 **Lockcount**が-22 であるとします。 最下位ビットは、次の方法で決定できます。

```dbgcmd
0:009> ? 0x1 & (-0n22)
Evaluate expression: 0 = 00000000
```

次の最下位ビットは、次のように決定できます。

```dbgcmd
0:009> ? (0x2 & (-0n22)) >> 1
Evaluate expression: 1 = 00000001
```

残りのビットの1補数は、次のように決定できます。

```dbgcmd
0:009> ? ((-1) - (-0n22)) >> 2
Evaluate expression: 5 = 00000005
```

この例では、最初のビットが0であるため、クリティカルセクションはロックされています。 2番目のビットは1であるため、このロックに対してスレッドがウェイクアップされていません。 残りのビットの補数は5であるため、このロックを待機している5つのスレッドがあります。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

クリティカルセクションのタイムアウトをデバッグする方法の詳細については、「[クリティカルセクション](critical-section-time-outs.md)のタイムアウト」を参照してください。 重要なセクションに関する一般的な情報については、「Microsoft Windows SDK」、「Windows Driver Kit (WDK)」、または「 *Microsoft windows の内部構造*(Mark Russinovich と David ソロモン)」を参照してください。

 

 






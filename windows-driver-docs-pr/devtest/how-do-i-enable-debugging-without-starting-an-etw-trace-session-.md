---
title: ETW トレース セッションを開始せずにデバッグ有効にする方法
description: ETW トレース セッションを開始せずにデバッグ有効にする方法
ms.assetid: d0487973-c66a-4ede-bc94-2e7e2060ab54
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 072381d0cf6574056d28cb08088db4b944dec515
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359472"
---
# <a name="how-do-i-enable-debugging-without-starting-an-etw-trace-session"></a>ETW トレース セッションを開始せずにデバッグを有効にする方法


ETW トレース セッションを開始せず、問題をデバッグするには、追加、 **WPP\_デバッグ**マクロ定義ソース コードにします。

WDK Tracedrv.sys サンプル ドライバーの例を次に示します。

```
#define WPP_DEBUG(b) DbgPrint b, DbgPrint("\n")
```

ほとんどの形式および引数で使用できる**WPP\_デバッグ**します。 ただし、% などの拡張形式の仕様を使用することはできません。16 進ダンプ! % をこのマクロに置き換えます。

参照してください[ユーザー モード デバッガーにトレース メッセージを送信する方法でしょうか。](how-do-i-send-trace-messages-to-a-user-mode-debugger-.md)します。

### <a name="span-idwhenusingthekerneldebuggerspanspan-idwhenusingthekerneldebuggerspanwhen-using-the-kernel-debugger"></a><span id="when_using_the_kernel_debugger"></span><span id="WHEN_USING_THE_KERNEL_DEBUGGER"></span>カーネル デバッガーを使用する場合

カーネル デバッガーを使用している場合は、WPP 制御構造のレベルとフラグの値を設定します。

1.  次のように、WPP 制御構造のアドレスを見つけます。
    ```
     kd>   x tracedrv!WPP_MAIN_CB    // tracedrv is the WPP instrumented driver
    9fbf3040 tracedrv!WPP_MAIN_CB = union WPP_PROJECT_CONTROL_BLOCK [1]
    kd>dt WPP_TRACE_CONTROL_BLOCK 9fbf3040  
    +0x000 Callback : 0x9fbf127c tracedrv!WppTraceCallback+0
    +0x004 ControlGuid : 0x9fbf206c _GUID {d58c126f-b309-11d1-969e-0000f875a5bc}
    +0x008 Next : (null) 
    +0x010 Logger : 0
    +0x018 RegistryPath : (null) 
    +0x01c FlagsLen : 0x1 ''
    +0x01d Level : 0x0 ''    <--- Set the Level
    +0x01e Reserved : 0
    +0x020 Flags : [1] 0x0  <--- Set the Flag
    ```

2.  レベルの値を設定**5**とするフラグの**0 xf**、次のように。
    ```
    kd>eb 9fbf305d 5    // setting the level value to 5
    ```

    ```
    kd>ed 9fbf3060 0xf    // setting the flag value to 0xf
    ```

3.  (Windows Vista および Windows の以降のバージョン)次のようにメッセージを受信するフィルターのマスクを有効にします。
    ```
    kd>ed nt!Kd_DEFAULT_Mask 0xff
    ```

 

 






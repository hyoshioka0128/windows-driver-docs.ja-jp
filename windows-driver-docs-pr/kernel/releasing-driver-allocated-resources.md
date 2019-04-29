---
title: ドライバーによって割り当てられたリソースの解放
description: ドライバーによって割り当てられたリソースの解放
ms.assetid: b286b4b0-54f2-4798-a77b-c08743502552
keywords:
- ルーチン WDK カーネルでは、非 PnP ドライバーをアンロードします。
- WDK カーネルの日常的な非 PnP アンロード
- ドライバーによって割り当てられたリソースを解放します。
- ドライバーによって割り当てられたリソースは、WDK のカーネルを解放します。
- リソースの解放 WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15e1ab0e35537ef046d5b8d41c8d0001c8e1a2c0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324260"
---
# <a name="releasing-driver-allocated-resources"></a>ドライバーによって割り当てられたリソースの解放





ドライバーが、レジストリを使用する方法の詳細、システム オブジェクトとそのデバイスの拡張機能、コント ローラー拡張機能または非ページ プールのドライバーに割り当てられたリソースをセットでは、ドライバーが異なります。 ただし、すべて[*アンロード*](https://msdn.microsoft.com/library/windows/hardware/ff564886)ルーチンは、段階的に、ドライバーを使用してリソースを解放する必要があります。

任意のドライバーの*アンロード*ルーチンする必要があることを確認しないその他のドライバーのルーチンが現在使用してすぐを使用して特定のリソースをそのリソースを解放する前にします。

一般に、*アンロード*ルーチンは、次の段階ですべてのドライバーに割り当てられたリソースを解放します。

1.  ドライバーが既に実行していない場合は、可能な場合、任意の物理デバイスの割り込みを無効にするを呼び出して[ **IoDisconnectInterrupt** ](https://msdn.microsoft.com/library/windows/hardware/ff549089)割り込みを無効にするようになります。

2.  その他のドライバーのルーチン参照できるようにしないリソースを*アンロード*ルーチンにリリースする予定です。

    たとえば、*アンロード*ルーチンを呼び出す必要があります[ **IoStopTimer** ](https://msdn.microsoft.com/library/windows/hardware/ff550377)場合、ドライバーの[ *IoTimer* ](https://msdn.microsoft.com/library/windows/hardware/ff550381)ルーチンは特定のデバイス オブジェクトの現在有効です。 ドライバーのディスパッチャー オブジェクトのいずれかを待機しているスレッドがないへの呼び出しのキューにそのタイマー オブジェクトがないことが必ずその[ *CustomTimerDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542983)ルーチンの記憶域を解放する前に、ディスパッチャー オブジェクト。 呼び出す必要があります[ **KeRemoveQueueDpc** ](https://msdn.microsoft.com/library/windows/hardware/ff553169)がある場合、 [ *CustomDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542972) ISR がキューに置かれた可能性がありますが、ルーチンとします。

    ドライバーが呼び出された場合[ **IoQueueWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff549466)、作業項目が完了していることを確認する必要があります。 **IoQueueWorkItem**は関連付けられているデバイス オブジェクトの参照を out; のような参照が残っている場合は、ドライバーをアンロードすることはできません。

    ドライバーが呼び出された場合[ **PsCreateSystemThread**](https://msdn.microsoft.com/library/windows/hardware/ff559932)、*アンロード*ルーチンもする必要がありますが発生する実行スレッド自体はを呼び出すことができるようにするドライバーが作成したスレッド[ **PsTerminateSystemThread** ](https://msdn.microsoft.com/library/windows/hardware/ff559959)ドライバーが読み込まれる前にします。 ドライバーは、呼び出すことによってシステムのドライバーが作成したスレッドを解放できません[ **ZwClose** ](https://msdn.microsoft.com/library/windows/hardware/ff566417)で、 *ThreadHandle*によって返される**PsCreateSystemThread**.

3.  ドライバーが割り当てられているデバイスに固有のリソースを解放します。 これにより、次のシステム サポート ルーチンを呼び出すことになる場合があります。
    -   [**IoDeleteSymbolicLink** ](https://msdn.microsoft.com/library/windows/hardware/ff549085)場合、 [ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)または[*を再初期化*](https://msdn.microsoft.com/library/windows/hardware/ff561022) というルーチン[**IoCreateSymbolicLink** ](https://msdn.microsoft.com/library/windows/hardware/ff549043)または[ **IoCreateUnprotectedSymbolicLink**](https://msdn.microsoft.com/library/windows/hardware/ff549050)、および[ **IoDeassignArcName** ](https://msdn.microsoft.com/library/windows/hardware/ff549076)ドライバーが呼び出された場合[ **IoAssignArcName**](https://msdn.microsoft.com/library/windows/hardware/ff548282)します。

    -   [**ExFreePool** ](https://msdn.microsoft.com/library/windows/hardware/ff544590)場合**DriverEntry**またはその他のルーチンのドライバーと呼ばれる[ **exallocatepoolwithtag に**](https://msdn.microsoft.com/library/windows/hardware/ff544520)ドライバーがまだリリースされていないと割り当てられたメモリ。

    -   [**MmUnmapIoSpace** ](https://msdn.microsoft.com/library/windows/hardware/ff556387)場合、 **DriverEntry**または*を再初期化*というルーチン[ **MmMapIoSpace**](https://msdn.microsoft.com/library/windows/hardware/ff554618)します。

    -   [**MmFreeNonCachedMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff554516)場合、 **DriverEntry**または*を再初期化*というルーチン[ **MmAllocateNonCachedMemory**](https://msdn.microsoft.com/library/windows/hardware/ff554479).

    -   [**MmFreeContiguousMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff554503)場合、 **DriverEntry**または*を再初期化*というルーチン[ **MmAllocateContiguousMemory**](https://msdn.microsoft.com/library/windows/hardware/ff554460).

    -   [**FreeCommonBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff546511)場合、 **DriverEntry**または*を再初期化*というルーチン[ **AllocateCommonBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff540575).

    -   [**IoAssignResources** ](https://msdn.microsoft.com/library/windows/hardware/ff548285)または[ **IoReportResourceUsage** ](https://msdn.microsoft.com/library/windows/hardware/ff549616)場合、 **DriverEntry**または*を再初期化*これらのルーチンと呼ばれる 1 サポート ルーチンまたは[ **HalAssignSlotResources** ](https://msdn.microsoft.com/library/windows/hardware/ff546580)自体やその物理デバイスの構成のレジストリ内のハードウェア リソースを要求するには個別にします。

4.  システム オブジェクトとリソースを解放する、 **DriverEntry**または*を再初期化*ルーチンまたはコント ローラー オブジェクトのコント ローラー拡張機能にデバイス オブジェクトの拡張機能でデバイスを設定する (場合、作成されたいずれか)。 具体的には、ドライバーする必要があります、次の操作には、デバイス オブジェクトを削除する前に ([**IoDeleteDevice**](https://msdn.microsoft.com/library/windows/hardware/ff549083)) またはコント ローラーのオブジェクト ([**IoDeleteController**](https://msdn.microsoft.com/library/windows/hardware/ff549078)):
    -   呼び出す[ **IoDisconnectInterrupt** ](https://msdn.microsoft.com/library/windows/hardware/ff549089)対応するデバイスまたはコント ローラー拡張機能に格納されている割り込みオブジェクト ポインターを解放します。
    -   呼び出す[ **ObDereferenceObject** ](https://msdn.microsoft.com/library/windows/hardware/ff557724)呼び出される場合に、次の下位ドライバーのファイル オブジェクトへのポインターが[ **IoGetDeviceObjectPointer** ](https://msdn.microsoft.com/library/windows/hardware/ff549198)デバイスまたはコント ローラーの拡張機能にこのポインターを格納します。
    -   呼び出す[ **IoDetachDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff549087)呼び出される場合、下位のドライバーのデバイス オブジェクトへのポインターが[ **IoAttachDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff548294)または[ **IoAttachDeviceToDeviceStack** ](https://msdn.microsoft.com/library/windows/hardware/ff548300)され、デバイスまたはコント ローラーの拡張機能にこのポインターを格納します。

5.  ハードウェア リソースを解放する、 **DriverEntry**または*を再初期化*ルーチンは、下のレジストリに存在する場合、ドライバーの物理デバイスでは、要求、 **\\レジストリ\\マシン\\ハードウェア\\ResourceMap**ツリー。

6.  そのデバイスのすべての名前を削除する、 **DriverEntry**または*を再初期化*ルーチンの下のレジストリに格納されている、 **\\レジストリ.\\DeviceMap**ツリーもします。

デバイス、システム、およびハードウェア リソースに、ドライバーがリリースされた後、次のセクションで説明した、デバイスとコント ローラーのオブジェクトを削除できます。

 

 





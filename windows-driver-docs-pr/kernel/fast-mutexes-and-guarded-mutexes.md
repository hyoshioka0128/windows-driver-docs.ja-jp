---
title: 高速なミュー テックスと保護されたミュー テックス
description: 高速なミュー テックスと保護されたミュー テックス
ms.assetid: 8c8014bf-6b81-4039-ae93-d4cedd6d6fed
keywords:
- 同期 WDK カーネルでは、高速なミュー テックス
- 同期 WDK カーネルでは、保護されたミュー テックス
- 保護されたミュー テックス WDK カーネル
- 高速なミュー テックス WDK カーネル
- ミュー テックス WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 212263c52417da6fcbe0ba80ffb3e8b347c59d82
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557596"
---
# <a name="fast-mutexes-and-guarded-mutexes"></a>高速なミュー テックスと保護されたミュー テックス


ドライバーを使用できます Windows 2000 以降、*ミュー テックスを高速*IRQL で実行されるコードの相互排他のオーバーヘッドの少ない形式を必要な場合&lt;APC を =\_レベル。 高速なミュー テックスは、一度に 1 つのスレッドによって入力必要のあるコード パスを保護できます。 スレッドである保護されたコード パスを入力する*取得*ミュー テックスです。 別のスレッドがミュー テックスを取得済みの場合、ミュー テックスが解放されるまで、現在のスレッドの実行は中断されます。 保護されているコードのパスをスレッドを終了する*解放*ミュー テックスです。

Windows Server 2003 以降では、ドライバーも使用できます*ミュー テックスを保護された*します。 保護されたミュー テックスは高速なミュー テックスに置き換わりますが、パフォーマンスが向上します。 保護されたミュー テックスは、高速のミュー テックスなど、一度に 1 つのスレッドによって入力必要のあるコード パスを保護できます。 ただし、ミュー テックスの実行が高速なミュー テックスを使用するコードをより迅速に保護を使用するコード。

Windows 8 の前に Windows のバージョンでは、保護されたミュー テックスは、高速なミュー テックスを異なる方法で実装されます。 IRQL で高速なミュー テックスによって保護されているコード パスが実行される = APC\_レベル。 IRQL で保護されたミュー テックスによって保護されているコード パスが実行される&lt;APC を =\_レベルがすべての Apc が無効になっています。 これら以前のバージョンの Windows では、保護されたミュー テックスの取得より高速なミュー テックスの取得も高速な操作です。 ただし、これら 2 種類のミュー テックスは、動作は同じです、同じ制限が適用されます。 具体的には、カーネルのルーチンはないを IRQL で呼び出す APC を =\_レベルは、高速なミュー テックスまたは保護されたミュー テックスによって保護されているコード パスから呼び出すことはできません。

Windows 8 以降、保護されたミュー テックスは、高速なミュー テックスとして実装されます。 保護されたミュー テックスまたは高速のミュー テックスによって保護されているコード パスで[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)処理として IRQL で発生しているカーネル ルーチン = APC\_レベル。 APC で有効でない呼び出し、Windows の以前のバージョンと\_レベルは、保護されたミュー テックスまたは高速なミュー テックスによって保護されているコード パスで無効です。

### <a name="fast-mutexes"></a>高速なミュー テックス

高速なミュー テックスがによって表される、 [**高速\_ミュー テックス**](https://msdn.microsoft.com/library/windows/hardware/ff545715)構造体。 ドライバーの独自のストレージを割り当てます、**高速\_ミュー テックス**構造体に呼び出し、 [ **ExInitializeFastMutex** ](https://msdn.microsoft.com/library/windows/hardware/ff545293)ルーチンを構造体を初期化します。

スレッドでは、次のいずれかの方法で高速のミュー テックスを取得します。

-   呼び出す、 [ **ExAcquireFastMutex** ](https://msdn.microsoft.com/library/windows/hardware/ff544337)ルーチン。 ミュー テックスは、別のスレッドによって既に取得されていますが、ミュー テックスができるまで、呼び出し元のスレッドの実行が中断されます。

-   呼び出す、 [ **ExTryToAcquireFastMutex** ](https://msdn.microsoft.com/library/windows/hardware/ff545647)ルーチンを現在のスレッドを中断することがなく、高速、ミュー テックスを取得しようとしています。 ルーチンは、ミュー テックスが取得されているかどうかに関係なく、すぐに返します。 **ExTryToAcquireFastMutex**返します**TRUE** ; 呼び出し元のミュー テックスを正常に取得した場合、それを返します**FALSE**します。

スレッドが[ **ExReleaseFastMutex** ](https://msdn.microsoft.com/library/windows/hardware/ff545549)いずれかで取得された高速なミュー テックスを解放する**ExAcquireFastMutex**または**ExTryToAcquireFastMutex**.

IRQL で高速なミュー テックスによって保護されているコード パスが実行される = APC\_レベル。 **ExAcquireFastMutex**と**ExTryToAcquireFastMutex** APC を現在の IRQL を発生させる\_レベル、および**ExReleaseFastMutex**元の IRQL が復元されます。 そのため、スレッドが高速なミュー テックスを保持している間、すべての Apc が無効です。

APC で常に実行するかどうかに、コード パスは保証\_レベル、ドライバーは呼び出すことができます代わりに[ **ExAcquireFastMutexUnsafe** ](https://msdn.microsoft.com/library/windows/hardware/ff544340)と[ **ExReleaseFastMutexUnsafe** ](https://msdn.microsoft.com/library/windows/hardware/ff545567)を取得し、高速なミュー テックスを解放します。 これらのルーチンが現在の IRQL を変更しないでくださいし、安全に使用できる現在の IRQL が APC が場合にのみ\_レベル。

高速なミュー テックスは、取得した再帰的にすることはできません。 高速なミュー テックスが既に保持しているスレッドは、それを取得しようとすると、そのスレッドがデッドロックが発生します。 高速なミュー テックスは IRQL で実行されるコードでのみ使用できます&lt;APC を =\_レベル。

### <a name="guarded-mutexes"></a>保護されたミュー テックス

Windows Server 2003 以降から使用できますが、保護されたミュー テックスより高いパフォーマンスが、高速なミュー テックスは、同じ関数を実行します。

Windows 8 以降、保護されたミュー テックスと高速なミュー テックス実装されます同じです。

Windows 8 の前に Windows のバージョンでは、保護されたミュー テックスは、高速なミュー テックスを異なる方法で実装されます。 APC を現在の IRQL を発生させる、高速なミュー テックスを獲得\_レベルをすばやく処理、保護された領域を入力して、保護されたミュー テックスを取得します。 保護された領域の詳細については、次を参照してください。[クリティカル領域および領域の保護された](critical-regions-and-guarded-regions.md)します。

保護されたミュー テックスがによって表される、 [ **KGUARDED\_ミュー テックス**](https://msdn.microsoft.com/library/windows/hardware/ff554235)構造体。 ドライバーの独自のストレージを割り当て、 **KGUARDED\_ミュー テックス**構造体に呼び出し、 [ **KeInitializeGuardedMutex** ](https://msdn.microsoft.com/library/windows/hardware/ff552144)ルーチンを初期化するために、構造体。

スレッドは、次のいずれかの方法で保護されたミュー テックスを取得します。

-   呼び出す[ **KeAcquireGuardedMutex**](https://msdn.microsoft.com/library/windows/hardware/ff551892)します。 ミュー テックスは、別のスレッドによって既に取得されていますが、ミュー テックスができるまで、呼び出し元のスレッドの実行が中断されます。

-   呼び出す[ **KeTryToAcquireGuardedMutex** ](https://msdn.microsoft.com/library/windows/hardware/ff553307)現在のスレッドを中断することがなく、保護された、ミュー テックスを取得しようとします。 ルーチンは、ミュー テックスが取得されているかどうかに関係なく、すぐに返します。 **KeTryToAcquireGuardedMutex**返します**TRUE** ; 呼び出し元のミュー テックスを正常に取得した場合、それを返します**FALSE**します。

スレッドが[ **KeReleaseGuardedMutex** ](https://msdn.microsoft.com/library/windows/hardware/ff553124)いずれかで取得された保護されたミュー テックスを解放する**KeAcquireGuardedMutex**または**KeTryToAcquireGuardedMutex**します。

保護された領域内で保護されたミュー テックスを暗黙的に保持しているスレッドが実行されます。 **KeAcquireGuardedMutex**と**KeTryToAcquireGuardedMutex** 、保護された領域を入力中に**KeReleaseGuardedMutex**が終了します。 スレッドが保護されたミュー テックスを保持している間は、すべての Apc が無効です。

代わりに、ドライバーを使用できる場合、コード パスが無効になっているすべての Apc を実行することが保証、 [ **KeAcquireGuardedMutexUnsafe** ](https://msdn.microsoft.com/library/windows/hardware/ff551894)と[ **KeReleaseGuardedMutexUnsafe**](https://msdn.microsoft.com/library/windows/hardware/ff553125)を取得し、保護されたミュー テックスを解放します。 これらのルーチンがない入力または保護された領域を終了し、既存の保護された領域内でのみ使用できますまたは IRQL = APC\_レベル。

保護されたミュー テックスは、獲得再帰的にすることはできません。 保護されたミュー テックスが既に保持しているスレッドは、それを取得しようとすると、そのスレッドがデッドロックが発生します。 保護されたミュー テックスは IRQL で実行されるコードでのみ使用できます&lt;APC を =\_レベル。

 

 





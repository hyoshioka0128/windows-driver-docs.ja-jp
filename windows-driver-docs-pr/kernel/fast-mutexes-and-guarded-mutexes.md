---
title: 高速ミューテックスと保護されたミューテックス
description: 高速ミューテックスと保護されたミューテックス
ms.assetid: 8c8014bf-6b81-4039-ae93-d4cedd6d6fed
keywords:
- 同期 WDK カーネル、高速ミューテックス
- 同期 WDK カーネル、保護されたミューテックス
- 保護された mutex WDK カーネル
- 高速ミューテックス WDK カーネル
- mutex WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4139553213606144b0559b725fb23adeafb80c4b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838694"
---
# <a name="fast-mutexes-and-guarded-mutexes"></a>高速ミューテックスと保護されたミューテックス


Windows 2000 以降では、IRQL &lt;= APC\_レベルで実行されるコードに対して、低オーバーヘッド形式の相互排他が必要な場合、ドライバーは*高速ミューテックス*を使用できます。 高速ミューテックスは、一度に1つのスレッドでのみ入力する必要があるコードパスを保護できます。 保護されたコードパスを入力するために、スレッドはミューテックスを*取得*します。 別のスレッドが既にミューテックスを取得している場合、ミューテックスが解放されるまで、現在のスレッドの実行は中断されます。 保護されたコードパスを終了するために、スレッドはミューテックスを*解放*します。

Windows Server 2003 以降では、ドライバーは保護された*ミューテックス*を使用することもできます。 保護されたミューテックスは、高速ミューテックスのドロップイン置換ですが、パフォーマンスが向上します。 高速ミューテックスと同様に、保護されたミューテックスは、一度に1つのスレッドだけが入力する必要があるコードパスを保護できます。 ただし、保護されたミューテックスを使用するコードは、高速ミューテックスを使用するコードよりも高速に実行されます。

Windows 8 より前のバージョンの Windows では、保護されたミューテックスが高速ミューテックスとは異なる方法で実装されています。 高速ミューテックスによって保護されているコードパスは、IRQL = APC\_レベルで実行されます。 保護されたミューテックスによって保護されているコードパスは、IRQL &lt;= APC\_レベルで実行されますが、すべての Apc は無効になっています。 以前のバージョンの Windows では、保護されたミューテックスを取得する操作は高速ミューテックスの取得よりも高速です。 ただし、これらの2種類のミューテックスは同じように動作し、同じ制限が適用されます。 特に、IRQL = APC\_LEVEL で呼び出すことができないカーネルルーチンは、高速ミューテックスまたは保護されたミューテックスで保護されているコードパスからは呼び出さないでください。

Windows 8 以降では、保護されたミューテックスは高速ミューテックスとして実装されています。 保護されたミューテックスまたは高速ミューテックスによって保護されているコードパスでは、[ドライバーの検証ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)は、IRQL = APC\_レベルで発生するようにカーネルルーチンへの呼び出しを処理します。 以前のバージョンの Windows と同様に、APC\_レベルでは無効な呼び出しは、保護されたミューテックスまたは高速ミューテックスによって保護されているコードパスでは無効です。

### <a name="fast-mutexes"></a>高速ミューテックス

高速ミューテックスは、[**高速\_mutex**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)構造体によって表されます。 ドライバーは、**高速\_MUTEX**構造用に独自のストレージを割り当ててから、 [**Exinitializefastmutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializefastmutex)ルーチンを呼び出して構造体を初期化します。

スレッドは、次のいずれかの方法で高速ミューテックスを取得します。

-   [**ExAcquireFastMutex**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff544337(v=vs.85))ルーチンを呼び出しています。 ミューテックスが既に別のスレッドによって取得されている場合、ミューテックスが使用可能になるまで、呼び出し元スレッドの実行は中断されます。

-   [**ExTryToAcquireFastMutex**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545647(v=vs.85))ルーチンを呼び出して、現在のスレッドを中断せずに高速ミューテックスを取得しようとしています。 このルーチンは、ミューテックスが取得されたかどうかに関係なく、直ちに戻ります。 **ExTryToAcquireFastMutex**は、呼び出し元のミューテックスを正常に取得した場合、 **TRUE**を返します。それ以外の場合は**FALSE**を返します。

スレッドは、 [**Exreleasefastmutex**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545549(v=vs.85))を呼び出して、 **ExAcquireFastMutex**または**ExTryToAcquireFastMutex**のいずれかによって取得された高速ミューテックスを解放します。

高速ミューテックスによって保護されているコードパスは、IRQL = APC\_レベルで実行されます。 **ExAcquireFastMutex**と**ExTryToAcquireFastMutex**は、現在の IRQL を APC\_レベルに上げ、 **exreleasefastmutex**は元の irql を復元します。 したがって、スレッドが高速ミューテックスを保持している間は、すべての Apc が無効になります。

コードパスが常に APC\_レベルで実行されることが保証されている場合、ドライバーは[**ExAcquireFastMutexUnsafe**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff544340(v=vs.85))と[**ExReleaseFastMutexUnsafe**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545567(v=vs.85))を呼び出して、高速ミューテックスを取得して解放することができます。 これらのルーチンは、現在の IRQL を変更せず、現在の IRQL が APC\_レベルの場合にのみ安全に使用できます。

高速ミューテックスを再帰的に取得することはできません。 既に高速ミューテックスを保持しているスレッドがそのスレッドを取得しようとすると、そのスレッドはデッドロック状態になります。 高速ミューテックスは、IRQL &lt;= APC\_レベルで実行されるコード内でのみ使用できます。

### <a name="guarded-mutexes"></a>保護されたミューテックス

Windows Server 2003 以降で使用可能な保護されたミューテックスは、高速ミューテックスと同じ機能を実行しますが、パフォーマンスは高くなります。

Windows 8 以降では、保護されたミューテックスと高速ミューテックスは同じように実装されています。

Windows 8 より前のバージョンの Windows では、保護されたミューテックスが高速ミューテックスとは異なる方法で実装されています。 高速ミューテックスを取得すると、現在の IRQL が APC\_レベルに上がりますが、保護されたミューテックスを取得すると、保護された領域に入ります。これは、より高速な操作です。 保護されたリージョンの詳細については、「[クリティカルなリージョンと保護](critical-regions-and-guarded-regions.md)されたリージョン」を参照してください。

保護されたミューテックスは、 [**Kguarded**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)された\_mutex 構造体によって表されます。 ドライバーは、 **\_kguarded の MUTEX**構造用に独自のストレージを割り当ててから、 [](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializeguardedmutex)ルーチンを呼び出して構造体を初期化します。

スレッドは、次のいずれかの方法で、保護されたミューテックスを取得します。

-   [**KeAcquireGuardedMutex**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551892(v=vs.85))を呼び出しています。 ミューテックスが既に別のスレッドによって取得されている場合、ミューテックスが使用可能になるまで、呼び出し元スレッドの実行は中断されます。

-   [**KeTryToAcquireGuardedMutex**](https://msdn.microsoft.com/library/windows/hardware/ff553307)を呼び出して、現在のスレッドを中断せずに、保護されたミューテックスを取得しようとしています。 このルーチンは、ミューテックスが取得されたかどうかに関係なく、直ちに戻ります。 **KeTryToAcquireGuardedMutex**は、呼び出し元のミューテックスを正常に取得した場合、 **TRUE**を返します。それ以外の場合は**FALSE**を返します。

スレッドは、 [**KeReleaseGuardedMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseguardedmutex)を呼び出して、 **KeAcquireGuardedMutex**または**KeTryToAcquireGuardedMutex**のいずれかによって取得された保護されたミューテックスを解放します。

保護されたミューテックスを保持するスレッドは、保護された領域内で暗黙的に実行されます。 **KeAcquireGuardedMutex**と**KeTryToAcquireGuardedMutex**は保護されたリージョンを入力しますが、 **KeReleaseGuardedMutex**は終了します。 スレッドが保護されたミューテックスを保持している間、すべての Apc が無効になります。

すべての Apc を無効にしてコードパスを確実に実行することが保証されている場合、ドライバーは[**KeAcquireGuardedMutexUnsafe**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551894(v=vs.85))と[**KeReleaseGuardedMutexUnsafe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseguardedmutexunsafe)を使用して、保護されたミューテックスを取得して解放できます。 これらのルーチンは保護されたリージョンを入力したり終了したりすることはなく、既に保護されているリージョン内、または IRQL = APC\_レベルでのみ使用できます。

保護されたミューテックスを再帰的に取得することはできません。 保護されたミューテックスを既に保持しているスレッドがそのスレッドを取得しようとすると、そのスレッドはデッドロック状態になります。 保護されたミューテックスは、IRQL &lt;= APC\_レベルで実行されるコードでのみ使用できます。

 

 





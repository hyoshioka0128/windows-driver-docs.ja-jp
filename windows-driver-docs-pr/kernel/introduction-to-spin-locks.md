---
title: スピンロックの概要
description: スピンロックの概要
ms.assetid: a37c0db4-ff9c-4958-a9f4-62b671458d03
keywords:
- KSPIN_LOCK
- executive スピンロック WDK カーネル
- 割り込みスピンロックの WDK カーネル
- キューに置かれたスピンロック WDK カーネル
- スピンロック WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 963bc0811925ce8eb4fc28bb02c421e3563002e9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838621"
---
# <a name="introduction-to-spin-locks"></a>スピンロックの概要





スピンロックは、カーネルによって定義された、カーネルモードのみの同期機構であり、非透過型としてエクスポートされます。 KSPIN\_LOCK です。 スピンロックを使用すると、SMP コンピューターで同時に実行できるルーチンと IRQL &gt;= DISPATCH\_レベルのルーチンによって、共有データまたは共有リソースを同時アクセスから保護することができます。

多くのコンポーネントでは、ドライバーなどのスピンロックを使用します。 どのような種類のドライバーでも、1つまたは複数の*executive スピンロック*を使用できます。 たとえば、ほとんどのファイルシステムでは、ファイルシステムのワーカースレッドコールバックルーチンと FSD の両方で処理される Irp を格納するために、ファイルシステムドライバーの (FSD) デバイス拡張機能でインタロックされていないワークキューを使用します。 インタロックされた作業キューは executive スピンロックによって保護されます。これにより、Irp をキューに挿入しようとしている FSD と、Irp を削除しようとするすべてのスレッドの競合が解決されます。 別の例として、システムフロッピーコントローラードライバーは2つの executive スピンロックを使用します。 1つの executive スピンロックは、このドライバーのデバイス専用スレッドと共有されている、インタロックされていないワークキューを保護します。もう1つは、3つのドライバールーチンによって共有されるタイマーオブジェクトを保護します。

Microsoft Windows XP およびそれ以降のバージョンの Windows 用ドライバーでは、 [**KeAcquireInStackQueuedSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))と[**KeReleaseInStackQueuedSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlock)を使用して、スピンロックを取得し、キューに置かれた*スピンロック*として解放できます。 キューに置かれたスピンロックは、マルチプロセッサコンピューターでの競合の多いロックに対する通常のスピンロックよりも優れたパフォーマンスを提供します。 詳細については、「キューに置かれた[スピンロック](queued-spin-locks.md)」を参照してください。 Windows 2000 用のドライバーでは、 [**KeAcquireSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)と[**KeReleaseSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock)を使用して、スピンロックを通常のスピンロックとして取得および解放できます。

単純なデータ構造へのアクセスを同期するために、ドライバーは任意の**Exinterlocked ロック * Xxx*** ルーチンを使用して、データ構造へのアトミックアクセスを可能にします。 これらのルーチンを使用するドライバーは、スピンロックを明示的に取得または解放する必要はありません。

ISR を持つすべてのドライバーは、ISR とその[*SynchCritSection*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine)ルーチン間で共有されるデータまたはハードウェアを保護するために、*割り込みスピンロック*を使用します。これは通常、 [*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチンと[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)ルーチンから呼び出されます。 割り込みスピンロックは、「ISR の登録」で説明されているように、ドライバーが[**Ioconnectinterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterrupt)を呼び出すときに作成される割り込みオブジェクトのセットに関連付けられます。

**ドライバーでのスピンロックの使用については、次のガイドラインに従ってください。**

-   スピンロックによって保護されているデータまたはリソースのストレージと、常駐システム領域メモリ内の対応するスピンロックのストレージを提供します ([仮想メモリ空間と物理メモリ](overview-of-windows-memory-space.md)の図を参照)。 ドライバーは、使用する executive スピンロックのストレージを提供する必要があります。 ただし、デバイスドライバーには、「ISR の登録」で説明されているように、multivector ISR があるか、複数の ISR がある場合を除き、割り込みスピンロックのストレージを提供する必要はありません。

-   [**Keinitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializespinlock)を使用して、保護する共有データまたはリソースへのアクセスを同期する前に、ドライバーがストレージを提供する各スピンロックを初期化します。

-   適切な IRQL でスピンロックを使用するすべてのサポートルーチンを呼び出します。通常は、executive スピンロックの場合は &lt;= ディスパッチ\_レベル、ドライバーの interrupt オブジェクトに関連付けられている割り込みスピンロックの場合は &lt;= DIRQL です。

-   スピンロックを保持しながら、できるだけ早く実行するルーチンを実装します。 どのルーチンも、25マイクロ秒を超えるスピンロックを保持する必要はありません。

-   スピンロックを保持した状態で、次のいずれかを実行するルーチンを実装しないでください。

    -   ハードウェアの例外を発生させたり、ソフトウェアの例外を発生させたりします。

    -   ページング可能メモリにアクセスしようとしました。

    -   デッドロックの原因となる再帰呼び出しを作成するか、またはスピンロックが25マイクロ秒より長く保持されるようにします。

    -   別のスピンロックを取得しようとすると、デッドロックが発生する可能性があります。

    -   上記の規則に違反する外部ルーチンを呼び出します。

 

 





---
title: ドライバーで作成されたスレッドを使用したインタロックされたキューの管理
description: ドライバーで作成されたスレッドを使用したインタロックされたキューの管理
ms.assetid: e2712d52-e98a-4450-b010-9278db3a7a1e
keywords:
- インタロック IRP キュー WDK カーネル
- ドライバーで作成されたスレッド WDK Irp
- 二重リンクされた Irp WDK カーネル
- ドライバー専用スレッドの WDK Irp
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6741447d1b52b83b6267d580064c89d3cd61921c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838547"
---
# <a name="managing-interlocked-queues-with-a-driver-created-thread"></a>ドライバーで作成されたスレッドを使用したインタロックされたキューの管理





新しいドライバーでは、このセクションで説明する方法を優先して、[キャンセルセーフの IRP キュー](cancel-safe-irp-queues.md)フレームワークを使用する必要があります。

システムフロッピーコントローラードライバーと同様に、 [*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチンではなく、デバイス専用のスレッドを使用するドライバーは、通常、二重にリンクされたインタロックされたキューにある irp の独自のキューを管理します。 デバイスで実行する作業がある場合、ドライバーのスレッドは、そのインタロックされたキューから Irp をプルします。

一般に、スレッドとスレッドの同期は、スレッドとその他のドライバールーチン間で共有されているリソースとの間で管理する必要があります。 また、ドライバーによって作成されたスレッドに対して、Irp がキューに登録されていることを通知する方法も必要です。 通常、スレッドは、デバイス拡張機能に格納されているディスパッチャーオブジェクトを待機します。これにより、IRP がインタロックされたキューに挿入された後に、ドライバーのディスパッチルーチンによってディスパッチャーオブジェクトがシグナル状態に設定されます。

ドライバーのディスパッチルーチンが呼び出されると、は、入力 IRP の i/o スタックの場所にあるパラメーターをチェックし、有効である場合は、後続の処理のために要求をキューに配置します。 ドライバー専用スレッドにキューに置かれている各 IRP について、ディスパッチルーチンは、 **ExInterlockedInsert*Xxx*リスト**を呼び出す前に、その irp を処理する必要がある任意のコンテキストを設定する必要があります。 各 IRP 内のドライバーの i/o スタックの場所によって、ドライバーのスレッドがターゲットデバイスオブジェクトのデバイス拡張機能にアクセスできるようになります。この場合、スレッドはキューから各 IRP を削除するため、ドライバーはコンテキスト情報をスレッドと共有できます。

取り消し可能な Irp をキューに置いているドライバーは、[*キャンセル*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)ルーチンを実装する必要があります。 Irp は非同期にキャンセルされるため、ドライバーが結果として発生する可能性のある競合状態を回避する必要があります。 Irp のキャンセルに関連する競合状態とその回避方法の詳細については、「 [irp のキャンセルの同期](synchronizing-irp-cancellation.md)」を参照してください。

ドライバーによって作成されたスレッドは、ドライバーが[**PsCreateSystemThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pscreatesystemthread)を呼び出したときにあらかじめ設定された、IRQL = パッシブ\_レベルおよび基本ランタイムの優先順位で実行されます。 IRP がドライバーの内部キューから削除されている間に、 [**ExInterlockedRemoveHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff545427)へのスレッドの呼び出しにより、現在のプロセッサ上で\_レベルをディスパッチする IRQL が一時的に発生します。 元の IRQL は、この呼び出しから戻ったときにパッシブ\_レベルに復元されます。

**ドライバースレッド (またはドライバーによって提供されるワーカースレッドコールバック) は、実行される IRQLs を慎重に管理する必要があります。たとえば、次の点を考慮してください。**

-   システムスレッドは一般に IRQL = パッシブ\_レベルで実行されるため、カーネル定義のディスパッチャーオブジェクトがシグナル状態に設定されるのをドライバースレッドが待機する可能性があります。

    たとえば、デバイス専用のスレッドは、他のドライバーがイベントを満たし、スレッドが[**IoBuildSynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildsynchronousfsdrequest)で設定した一部の部分転送 irp を完了するまで待機する場合があります。

-   ただし、このようなデバイス専用スレッドは、特定のサポートルーチンを呼び出す前に、現在のプロセッサ上で IRQL を発生させる必要があります。

    たとえば、ドライバーが DMA を使用する場合、デバイス専用のスレッドは、これらのルーチンや特定のルーチンなどの理由で、 [**Keraiseirql**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirql)と[**ke低 irql**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kelowerirql)の呼び出しの間に、 [**Allocateadapterchannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel)と[**freeadapterchannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_adapter_channel)への呼び出しを入れ子にする必要があります。DMA 操作のサポートルーチンは、IRQL = ディスパッチ\_レベルで呼び出す必要があります。

    [*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチンはディスパッチ\_レベルで実行されるので、DMA を使用するドライバーは*StartIo*ルーチンから**Ke*Xxx*Irql**ルーチンを呼び出す必要がないことに注意してください。

-   ドライバーで作成されたスレッドは、IRQL = パッシブ\_レベルでは任意のスレッドコンテキストで実行されるため、ページング可能なメモリにアクセスできますが、他の多くの標準ドライバールーチンは IRQL &gt;= ディスパッチ\_レベルで実行されます。 ドライバーによって作成されたスレッドが、このようなルーチンからアクセスできるメモリを割り当てる場合は、非ページプールからメモリを割り当てる必要があります。 たとえば、デバイス専用のスレッドが、後でドライバーの ISR または[*SynchCritSection*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine)、 [*adaptercontrol*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control)、 [*AdapterListControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_list_control)、[*コントローラー*](https://msdn.microsoft.com/library/windows/hardware/ff542049)、および[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)[*によってアクセスされるバッファーを割り当てる場合、CustomDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine)、 [*iotimer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_timer_routine)、 [*customtimerdpc*](https://msdn.microsoft.com/library/windows/hardware/ff542983)、または上位レベルのドライバーの[*iotimer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンでは、スレッドに割り当てられたメモリをページングすることはできません。

-   ドライバーが共有状態情報またはリソースをデバイス拡張機能に保持している場合、ドライバースレッド ( *StartIo*ルーチンなど) は、同じデバイスにアクセスする他のルーチンと共に、物理デバイスと共有データへのアクセスを同期する必要があります。、メモリ位置、またはリソース。

    スレッドがデバイスまたは状態を ISR と共有している場合は、 [**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)を使用して、デバイスをプログラムしたり、共有状態にアクセスしたりするために、ドライバーによって提供される[*SynchCritSection*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine)ルーチンを呼び出す必要があります。 「[クリティカルセクションの使用」を](using-critical-sections.md)参照してください。

    スレッドが、ISR 以外のルーチンで状態またはリソースを共有する場合、ドライバーは、ドライバーによって提供される、ドライバーで初期化された executive スピンロックを使用して、共有状態またはリソースを保護する必要があります。 詳細については、「[スピンロック](spin-locks.md)」を参照してください。

低速デバイスのドライバースレッドを使用したの設計上のトレードオフの詳細については、「[デバイスのポーリング](avoid-polling-devices.md)」を参照してください。 「[ハードウェアの優先順位の管理](managing-hardware-priorities.md)」も参照してください。 特定のサポートルーチンの IRQLs に関する具体的な情報については、ルーチンのリファレンスページを参照してください。

 

 





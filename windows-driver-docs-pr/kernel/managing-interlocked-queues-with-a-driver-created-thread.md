---
title: ドライバーによって作成されたスレッドを使用したインタロック キューの管理
description: ドライバーによって作成されたスレッドを使用したインタロック キューの管理
ms.assetid: e2712d52-e98a-4450-b010-9278db3a7a1e
keywords:
- インタロックされた IRP キュー WDK カーネル
- ドライバーで作成されたスレッド WDK Irp
- ダブルリンク Irp WDK カーネル
- WDK Irp ドライバー専用のスレッド
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b9f3bdcbcb9ce3964fa5df67f4661ee146a89a3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386016"
---
# <a name="managing-interlocked-queues-with-a-driver-created-thread"></a>ドライバーによって作成されたスレッドを使用したインタロック キューの管理





新しいドライバーを使用する必要があります、[キャンセル セーフ IRP キュー](cancel-safe-irp-queues.md)メソッドのこのセクションで概説した方が優先的フレームワーク。

などのシステムのフロッピー コント ローラー ドライバー デバイス専用のスレッドでは、ドライバーではなく[ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)ルーチンが通常の Irp の独自キューでダブルリンク インタロックされたキューを管理します。 ドライバーのスレッドでは、デバイスで実行する作業がある場合に Irp のインタロックされたキューから取り出します。

一般に、ドライバーは、スレッドとその他のドライバーのルーチンの間で共有リソースには、そのスレッドとの同期を管理する必要があります。 ドライバーもそのドライバーが作成したスレッド Irp がキューに置かれたことを通知する手段が必要です。 通常、スレッドは、ドライバーのディスパッチ ルーチン IRP インタロックされたキューに挿入した後にディスパッチャー オブジェクトをシグナルされた状態に設定するまで、デバイスの拡張機能に格納する dispatcher オブジェクトで待機します。

ドライバーのディスパッチ ルーチンが呼び出されると、各入力 IRP の I/O スタックの場所では、パラメーターを調べが、有効である場合は、さらに処理要求をキューします。 ディスパッチ ルーチンは、どのようなコンテキストを処理する必要があるそのスレッド前に IRP の呼び出しを設定する必要があります各 IRP がドライバー専用のスレッドにキューに入れ、 **ExInterlockedInsert*Xxx*一覧**します。 各 IRP のドライバーの I/O スタックの場所、ドライバーのスレッドにアクセス対象のデバイス オブジェクトのデバイスの拡張機能場所ドライバー情報を共有できますコンテキスト、そのスレッドでスレッドがキューから各 IRP を削除します。

キャンセル可能な irp がドライバーを実装する必要があります、 [*キャンセル*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel)ルーチン。 Irp が非同期に取り消されたため、ドライバーがつながる可能性がある競合状態を回避ことを確認する必要があります。 参照してください[同期 IRP キャンセル](synchronizing-irp-cancellation.md)Irp とその回避手法のキャンセルに関連付けられている競合状態の詳細についてはします。

IRQL でいずれかのドライバーが作成したスレッドが実行される = パッシブ\_レベルと、ドライバーが呼び出されたときに以前に設定された基本ランタイムの優先順位[ **PsCreateSystemThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pscreatesystemthread)します。 スレッドの呼び出しを[ **ExInterlockedRemoveHeadList** ](https://msdn.microsoft.com/library/windows/hardware/ff545427)ディスパッチに IRQL を一時的に上げる\_IRP がドライバーから削除されるときに、現在のプロセッサ上のレベルの内部キューです。 元の IRQL がパッシブに復元される\_レベルであるこの呼び出しからの戻り値。

**ドライバー スレッド (やワーカー スレッドをドライバーが指定したコールバック) では、実行する時刻 Irql 慎重に管理する必要があります。たとえば、次の点を考慮してください。**

-   システムのスレッドは、IRQL で通常実行されるため = パッシブ\_レベル、ドライバー スレッド カーネル定義のディスパッチャー オブジェクトがシグナル状態に設定を待機することができます。

    たとえば、デバイス専用のスレッドは、イベントを満たすし、いくつかの部分でスレッドを設定する Irp を転送を完了するには、その他のドライバーの待機可能性があります[ **IoBuildSynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildsynchronousfsdrequest)します。

-   ただし、デバイス専用スレッド上げる必要があります IRQL、現在のプロセッサの特定のサポート ルーチンを呼び出す前にします。

    たとえば、ドライバーは、DMA を使用している場合、デバイス専用のスレッド入れ子にしなければなりませんへの呼び出し[ **AllocateAdapterChannel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pallocate_adapter_channel)と[ **FreeAdapterChannel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pfree_adapter_channel)呼び出しの間で[ **KeRaiseIrql** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keraiseirql)と[ **KeLowerIrql** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kelowerirql)のため、これらのルーチンとその他の特定IRQL で DMA 操作を呼び出す必要があるルーチンのサポートのディスパッチを =\_レベル。

    注意して[ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)ルーチンは、ディスパッチに実行\_レベル、DMA を使用するドライバーが呼び出しを行うことが必要であるため、 **Ke*Xxx*Irql**ルーチンからその*StartIo*ルーチン。

-   ドライバーが作成したスレッドは、実行されるため、nonarbitrary スレッド コンテキストに (独自) ページング可能なメモリにアクセスできる IRQL = パッシブ\_IRQL でレベルが他の多くの標準のドライバー ルーチンの実行&gt;= ディスパッチ\_レベル。 ドライバーが作成したスレッドは、このようなルーチンによってアクセスできるメモリを割り当て場合、は、非ページ プールからメモリを割り当てする必要があります。 たとえば、デバイス専用のスレッドが、ドライバーの ISR によって後でアクセスされるすべてのバッファーを割り当てまたは[ *SynchCritSection*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ksynchronize_routine)、 [ *AdapterControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_control)、 [ *AdapterListControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_list_control)、 [ *ControllerControl*](https://msdn.microsoft.com/library/windows/hardware/ff542049)、 [ *DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine)、 [ *CustomDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kdeferred_routine)、 [ *IoTimer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_timer_routine)、 [*CustomTimerDpc*](https://msdn.microsoft.com/library/windows/hardware/ff542983)、またはより高度なドライバー、 [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine) 、日常的なスレッドに割り当てられたメモリすることはできませんページング可能な。

-   ドライバーは、共有状態の情報やデバイスの拡張機能、ドライバーのスレッド内のリソースを保持する場合 (など、 *StartIo*ルーチン) 物理デバイスと、共有のアクセスを同期する必要があります、ドライバーを使用したデータの他のルーチンを同じデバイス、メモリ位置、またはリソースにアクセスします。

    これを使用する必要があります、スレッドは、ISR でデバイスまたは状態を共有する場合[ **KeSynchronizeExecution** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesynchronizeexecution)を呼び出すドライバーによって提供される[ *SynchCritSection* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ksynchronize_routine)ルーチンまたは共有の状態にアクセスするデバイスをプログラミングします。 参照してください[クリティカル セクションを使用して](using-critical-sections.md)します。

    スレッドは、ISR 以外のルーチンに状態またはリソースを共有する場合、ドライバーの共有状態またはドライバーが、記憶域を提供するドライバー初期化 executive スピン ロックでリソースを保護する必要があります。 詳細については、次を参照してください。[スピン ロック](spin-locks.md)します。

低速のデバイスのドライバーのスレッドを使用して、設計上のトレードオフの詳細については、次を参照してください。[デバイスのポーリング](avoid-polling-devices.md)します。 参照してください[ハードウェアの優先度を管理する](managing-hardware-priorities.md)します。 特定のサポート ルーチンの Irql の特定については、ルーチンのリファレンス ページを参照してください。

 

 





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
ms.openlocfilehash: 7be720cc186db2dc10f4e3511953d72c09e21144
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360280"
---
# <a name="managing-interlocked-queues-with-a-driver-created-thread"></a>ドライバーによって作成されたスレッドを使用したインタロック キューの管理





新しいドライバーを使用する必要があります、[キャンセル セーフ IRP キュー](cancel-safe-irp-queues.md)メソッドのこのセクションで概説した方が優先的フレームワーク。

などのシステムのフロッピー コント ローラー ドライバー デバイス専用のスレッドでは、ドライバーではなく[ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858)ルーチンが通常の Irp の独自キューでダブルリンク インタロックされたキューを管理します。 ドライバーのスレッドでは、デバイスで実行する作業がある場合に Irp のインタロックされたキューから取り出します。

一般に、ドライバーは、スレッドとその他のドライバーのルーチンの間で共有リソースには、そのスレッドとの同期を管理する必要があります。 ドライバーもそのドライバーが作成したスレッド Irp がキューに置かれたことを通知する手段が必要です。 通常、スレッドは、ドライバーのディスパッチ ルーチン IRP インタロックされたキューに挿入した後にディスパッチャー オブジェクトをシグナルされた状態に設定するまで、デバイスの拡張機能に格納する dispatcher オブジェクトで待機します。

ドライバーのディスパッチ ルーチンが呼び出されると、各入力 IRP の I/O スタックの場所では、パラメーターを調べが、有効である場合は、さらに処理要求をキューします。 ディスパッチ ルーチンは、どのようなコンテキストを処理する必要があるそのスレッド前に IRP の呼び出しを設定する必要があります各 IRP がドライバー専用のスレッドにキューに入れ、 **ExInterlockedInsert*Xxx*一覧**します。 各 IRP のドライバーの I/O スタックの場所、ドライバーのスレッドにアクセス対象のデバイス オブジェクトのデバイスの拡張機能場所ドライバー情報を共有できますコンテキスト、そのスレッドでスレッドがキューから各 IRP を削除します。

キャンセル可能な irp がドライバーを実装する必要があります、 [*キャンセル*](https://msdn.microsoft.com/library/windows/hardware/ff540742)ルーチン。 Irp が非同期に取り消されたため、ドライバーがつながる可能性がある競合状態を回避ことを確認する必要があります。 参照してください[同期 IRP キャンセル](synchronizing-irp-cancellation.md)Irp とその回避手法のキャンセルに関連付けられている競合状態の詳細についてはします。

IRQL でいずれかのドライバーが作成したスレッドが実行される = パッシブ\_レベルと、ドライバーが呼び出されたときに以前に設定された基本ランタイムの優先順位[ **PsCreateSystemThread**](https://msdn.microsoft.com/library/windows/hardware/ff559932)します。 スレッドの呼び出しを[ **ExInterlockedRemoveHeadList** ](https://msdn.microsoft.com/library/windows/hardware/ff545427)ディスパッチに IRQL を一時的に上げる\_IRP がドライバーから削除されるときに、現在のプロセッサ上のレベルの内部キューです。 元の IRQL がパッシブに復元される\_レベルであるこの呼び出しからの戻り値。

**ドライバー スレッド (やワーカー スレッドをドライバーが指定したコールバック) では、実行する時刻 Irql 慎重に管理する必要があります。たとえば、次の点を考慮してください。**

-   システムのスレッドは、IRQL で通常実行されるため = パッシブ\_レベル、ドライバー スレッド カーネル定義のディスパッチャー オブジェクトがシグナル状態に設定を待機することができます。

    たとえば、デバイス専用のスレッドは、イベントを満たすし、いくつかの部分でスレッドを設定する Irp を転送を完了するには、その他のドライバーの待機可能性があります[ **IoBuildSynchronousFsdRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548330)します。

-   ただし、デバイス専用スレッド上げる必要があります IRQL、現在のプロセッサの特定のサポート ルーチンを呼び出す前にします。

    たとえば、ドライバーは、DMA を使用している場合、デバイス専用のスレッド入れ子にしなければなりませんへの呼び出し[ **AllocateAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff540573)と[ **FreeAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff546507)呼び出しの間で[ **KeRaiseIrql** ](https://msdn.microsoft.com/library/windows/hardware/ff553079)と[ **KeLowerIrql** ](https://msdn.microsoft.com/library/windows/hardware/ff552968)のため、これらのルーチンとその他の特定IRQL で DMA 操作を呼び出す必要があるルーチンのサポートのディスパッチを =\_レベル。

    注意して[ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858)ルーチンは、ディスパッチに実行\_レベル、DMA を使用するドライバーが呼び出しを行うことが必要であるため、 **Ke*Xxx*Irql**ルーチンからその*StartIo*ルーチン。

-   ドライバーが作成したスレッドは、実行されるため、nonarbitrary スレッド コンテキストに (独自) ページング可能なメモリにアクセスできる IRQL = パッシブ\_IRQL でレベルが他の多くの標準のドライバー ルーチンの実行&gt;= ディスパッチ\_レベル。 ドライバーが作成したスレッドは、このようなルーチンによってアクセスできるメモリを割り当て場合、は、非ページ プールからメモリを割り当てする必要があります。 たとえば、デバイス専用のスレッドが、ドライバーの ISR によって後でアクセスされるすべてのバッファーを割り当てまたは[ *SynchCritSection*](https://msdn.microsoft.com/library/windows/hardware/ff563928)、 [ *AdapterControl* ](https://msdn.microsoft.com/library/windows/hardware/ff540504)、 [ *AdapterListControl*](https://msdn.microsoft.com/library/windows/hardware/ff540513)、 [ *ControllerControl*](https://msdn.microsoft.com/library/windows/hardware/ff542049)、 [ *DpcForIsr*](https://msdn.microsoft.com/library/windows/hardware/ff544079)、 [ *CustomDpc*](https://msdn.microsoft.com/library/windows/hardware/ff542972)、 [ *IoTimer*](https://msdn.microsoft.com/library/windows/hardware/ff550381)、 [*CustomTimerDpc*](https://msdn.microsoft.com/library/windows/hardware/ff542983)、またはより高度なドライバー、 [ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354) 、日常的なスレッドに割り当てられたメモリすることはできませんページング可能な。

-   ドライバーは、共有状態の情報やデバイスの拡張機能、ドライバーのスレッド内のリソースを保持する場合 (など、 *StartIo*ルーチン) 物理デバイスと、共有のアクセスを同期する必要があります、ドライバーを使用したデータの他のルーチンを同じデバイス、メモリ位置、またはリソースにアクセスします。

    これを使用する必要があります、スレッドは、ISR でデバイスまたは状態を共有する場合[ **KeSynchronizeExecution** ](https://msdn.microsoft.com/library/windows/hardware/ff553302)を呼び出すドライバーによって提供される[ *SynchCritSection* ](https://msdn.microsoft.com/library/windows/hardware/ff563928)ルーチンまたは共有の状態にアクセスするデバイスをプログラミングします。 参照してください[クリティカル セクションを使用して](using-critical-sections.md)します。

    スレッドは、ISR 以外のルーチンに状態またはリソースを共有する場合、ドライバーの共有状態またはドライバーが、記憶域を提供するドライバー初期化 executive スピン ロックでリソースを保護する必要があります。 詳細については、次を参照してください。[スピン ロック](spin-locks.md)します。

低速のデバイスのドライバーのスレッドを使用して、設計上のトレードオフの詳細については、次を参照してください。[デバイスのポーリング](avoid-polling-devices.md)します。 参照してください[ハードウェアの優先度を管理する](managing-hardware-priorities.md)します。 特定のサポート ルーチンの Irql の特定については、ルーチンのリファレンス ページを参照してください。

 

 





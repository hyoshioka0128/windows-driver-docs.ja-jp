---
title: ハードウェアの優先度の管理
description: ハードウェアの優先度の管理
ms.assetid: c27eb357-49d7-4f50-9554-643b70ca33dc
keywords:
- 優先順位を付ける条件 WDK カーネル
- ハードウェアの優先順位の WDK カーネル
- IRQL レベル WDK カーネル
- PASSIVE_LEVEL WDK
- APC_LEVEL WDK
- DISPATCH_LEVEL WDK
- DIRQL WDK
- 割り込みサービス ルーチン WDK カーネル、ハードウェアの優先順位
- Isr WDK カーネルでは、ハードウェアの優先順位
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: 051aac20bc8a3b0f142efb27444f69c19b741b07
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579843"
---
# <a name="managing-hardware-priorities"></a>ハードウェアの優先度の管理





ドライバーのルーチンが実行される IRQL では、カーネル モード ドライバー サポート ルーチンを呼び出すことが決定します。 たとえば、一部のドライバー サポート ルーチンが必要と IRQL で実行されている呼び出し元を = ディスパッチ\_レベル。 呼び出し元がパッシブより大きい IRQL で実行されている場合に安全に他のユーザーということはできません\_レベル。

最もよく実装の標準のドライバーのルーチンを呼びます Irql の一覧を次に示します。 Irql は低いものから最も高い優先順位を一覧表示されます。

<a href="" id="passive-level"></a>**パッシブ\_レベル**  
**マスクされた割り込み**-None。

**ドライバーのルーチンで呼び出さ**パッシブ\_レベル- [**DriverEntry**](https://msdn.microsoft.com/library/windows/hardware/ff544113)、 [ *AddDevice*](https://msdn.microsoft.com/library/windows/hardware/ff540521)、 [*を再初期化*](https://msdn.microsoft.com/library/windows/hardware/ff561022)、 [*アンロード*](https://msdn.microsoft.com/library/windows/hardware/ff564886)ルーチン、ほとんどのディスパッチ ルーチンは、ドライバーが作成したスレッド、ワーカー スレッドのコールバック。

<a href="" id="apc-level"></a>**APC\_レベル**  
**マスク オフ割り込み**— APC\_レベル割り込み、マスク オフに指定します。

**ドライバーで呼び出されるルーチン**APC\_レベル: 一部のディスパッチ ルーチン (を参照してください[ディスパッチ ルーチンは、Irql](dispatch-routines-and-irqls.md))。

<a href="" id="dispatch-level"></a>**ディスパッチ\_レベル**  
**マスク オフ割り込み** -ディスパッチ\_レベルと APC\_レベル割り込み、マスク オフに指定します。 デバイス、時計、および電源障害の中断が発生することができます。

**ドライバーのルーチンで呼び出さ**ディスパッチ\_レベル- [*StartIo*](https://msdn.microsoft.com/library/windows/hardware/ff563858)、 [ *AdapterControl*](https://msdn.microsoft.com/library/windows/hardware/ff540504)、 [ *AdapterListControl*](https://msdn.microsoft.com/library/windows/hardware/ff540513)、 [ *ControllerControl*](https://msdn.microsoft.com/library/windows/hardware/ff542049)、 [ *IoTimer* ](https://msdn.microsoft.com/library/windows/hardware/ff550381)、 [*キャンセル*](https://msdn.microsoft.com/library/windows/hardware/ff540742) (キャンセル スピン ロックを保持) 中、 [ *DpcForIsr*](https://msdn.microsoft.com/library/windows/hardware/ff544079)、 [ *CustomTimerDpc*](https://msdn.microsoft.com/library/windows/hardware/ff542983)、 [ *CustomDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542972)ルーチン。

<a href="" id="dirql"></a>**DIRQL**  
**マスク オフ割り込み** — IRQL ですべての割り込み&lt;ドライバーの割り込みのオブジェクトの DIRQL を = です。 クロックと電源の障害割り込みと共に、DIRQL 値の大きいデバイスの中断が発生することができます。

ドライバーで DIRQL ルーチンと呼ばれます- [*InterruptService*](https://msdn.microsoft.com/library/windows/hardware/ff547958)、 [ *SynchCritSection* ](https://msdn.microsoft.com/library/windows/hardware/ff563928)ルーチン。

APC の唯一の違い\_レベルとパッシブ\_レベルから APC にプロセス実行\_レベル APC 割り込みを取得できません。 両方は、Irql がスレッド コンテキストを示すもので、両方は、コードをページ アウトできることを意味するもので。

最下位レベルのドライバーでは、Irql の 3 つのいずれかで実行中に Irp を処理します。

-   パッシブ\_レベル、マスクがオフで、ドライバーのディスパッチ routine(s)、プロセッサの割り込み

    **DriverEntry**、 *AddDevice*、*を再初期化*、および*アンロード*ルーチンは、パッシブで実行されても\_レベルにどのドライバーが作成できます。システム スレッドです。

-   ディスパッチ\_レベル、ディスパッチ\_レベルと APC\_レベルの割り込みをプロセッサ上ではオフ マスク、 *StartIo*ルーチン

    *AdapterControl*、 *AdapterListControl*、 *ControllerControl*、 *IoTimer*、*キャンセル*(保持している間、キャンセル スピン ロック) と*CustomTimerDpc*ルーチンは、ディスパッチで実行されても\_レベルには*DpcForIsr*と*CustomDpc*ルーチン。

-   デバイスの IRQL (DIRQL)、以下にあるすべての割り込みを*SynchronizeIrql*プロセッサで ISR のマスクされたドライバーの割り込みのオブジェクトのおよび*SynchCritSection*ルーチン

最も高度なドライバーは、2 つの Irql のいずれかで実行中に Irp を処理します。

-   パッシブ\_レベル、マスクがオフ、ドライバーのディスパッチ ルーチンで、プロセッサの割り込み

    **DriverEntry**、*を再初期化*、 *AddDevice*、および*アンロード*ルーチンは、パッシブで実行されても\_レベルにどのドライバーが作成できます。システムのスレッドまたはワーカー スレッド コールバック ルーチンまたはファイル システム ドライバー。

-   ディスパッチ\_レベル、ディスパッチ\_レベルと APC\_レベルの割り込みをプロセッサのドライバーのマスク オフに指定*IoCompletion* routine(s)

    *IoTimer*、*キャンセル*、および*CustomTimerDpc*ルーチンは、ディスパッチで実行されても\_レベル。

いくつかの状況では、大容量記憶装置の中間的な最下位レベルのドライバーは IRQL APC で呼び出されます\_レベル。 ファイル システム ドライバーの送信をページ フォールトに具体的には、この発生することができます、 [ **IRP\_MJ\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/ff550794)ドライバーを削減する要求。

最も標準的なドライバーのルーチンは、単に、適切なサポート ルーチンを呼び出すことを許可する IRQL で実行されます。 たとえば、デバイス ドライバーを呼び出す必要があります[ **AllocateAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff540573) IRQL ディスパッチで実行中に\_レベル。 ほとんどのデバイス ドライバーからこれらのルーチンを呼び出すため、 *StartIo*ルーチン、通常は実行されているディスパッチで\_既にレベルします。

なお、デバイス ドライバーがない*StartIo*ルーチンを設定し、Irp のキューを管理するため、必ずしも実行されていないディスパッチで\_レベル IRQL ときに呼び出す必要があります**AllocateAdapterChannel**. このようなドライバーは、その呼び出しを入れ子にしなければなりません**AllocateAdapterChannel**呼び出しの間で[ **KeRaiseIrql** ](https://msdn.microsoft.com/library/windows/hardware/ff553079)と[ **KeLowerIrql**](https://msdn.microsoft.com/library/windows/hardware/ff552968)を呼び出すときに必要な IRQL で実行するよう**AllocateAdapterChannel**し、呼び出し元のルーチンは、コントロールを得たときに、元の IRQL を復元します。

ドライバー サポート ルーチンを呼び出すときに、次の注意します。

- 呼び出す[ **KeRaiseIrql** ](https://msdn.microsoft.com/library/windows/hardware/ff553079) 、入力の*NewIrql*はより小さい値は現在の IRQL で致命的なエラーが発生します。 呼び出す[ **KeLowerIrql** ](https://msdn.microsoft.com/library/windows/hardware/ff552968)以外に、元の IRQL を復元します (つまり、呼び出しの後に**KeRaiseIrql**) も、致命的なエラーが発生します。

- IRQL での実行中に&gt;= ディスパッチ\_レベル、呼び出す[ **kewaitforsingleobject の 1** ](https://msdn.microsoft.com/library/windows/hardware/ff553350)または[ **KeWaitForMultipleObjects**](https://msdn.microsoft.com/library/windows/hardware/ff553324)カーネル定義のディスパッチャー オブジェクトになるまで待機する間隔を 0 以外の場合に、致命的なエラーが発生します。

- イベント、セマフォ、ミュー テックス、またはシグナル状態に設定するタイマーを安全に待機できる唯一のドライバー ルーチンは、IRQL パッシブで nonarbitrary スレッド コンテキストで実行される\_ドライバーで作成されたスレッドなどのレベル、 **DriverEntry**と*を再初期化*ルーチン、または (ほとんどのデバイスの I/O 制御要求) などの本質的な同期 I/O 操作のディスパッチ ルーチン。

- IRQL パッシブで実行されている中でも\_レベル、ページング可能なドライバーのコードを呼び出す必要がありますいない[ **KeSetEvent**](https://msdn.microsoft.com/library/windows/hardware/ff553253)、 [ **KeReleaseSemaphore** ](https://msdn.microsoft.com/library/windows/hardware/ff553143)、または[ **KeReleaseMutex** ](https://msdn.microsoft.com/library/windows/hardware/ff553140)入力*待機*パラメーターに設定**TRUE**します。 このような呼び出しには、致命的なページ フォールトを可能性があります。

- IRQL APC よりも大きい値で実行されている任意のルーチン\_レベルはページ プールからメモリを割り当てるもページ プールのメモリを安全にアクセスします。 場合 APC より大きい IRQL で実行されているルーチン\_レベルでは、ページ フォールトは致命的なエラーです。

- ドライバーは、IRQL のディスパッチで実行する必要があります\_を呼び出すときにレベル[ **KeAcquireSpinLockAtDpcLevel** ](https://msdn.microsoft.com/library/windows/hardware/ff551921)と[ **KeReleaseSpinLockFromDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/ff553150).

  IRQL でドライバーを実行できる&lt;= ディスパッチ\_を呼び出すときにレベル**KeAcquireSpinLock**が呼び出すことによってそのスピン ロックを解放する必要がありますには**KeReleaseSpinLock**します。 指定されたスピン ロックを解放するプログラミング エラーはつまり、 **KeAcquireSpinLock**呼び出して**KeReleaseSpinLockFromDpcLevel**します。

  ドライバーを呼び出してはならない**KeAcquireSpinLockAtDpcLevel**、 **KeReleaseSpinLockFromDpcLevel**、 **KeAcquireSpinLock**、または**KeReleaseSpinLock** IRQL での実行中に&gt;ディスパッチ\_レベル。

- など、スピン ロックを使用するサポート ルーチンを呼び出す、 **ExInterlocked * Xxx*** ルーチンを発生させます IRQL、現在のプロセッサにディスパッチするいずれか\_レベルまたは DIRQL、呼び出し元が発生した IRQL で既に実行されていない場合。

- IRQL で実行されるドライバー コード&gt;パッシブ\_レベルが可能な限り早く実行する必要があります。 可能な限り早く実行するには、そのルーチンをチューニングする優れた全体的なパフォーマンスのためは、さらに重要なルーチンを実行するほどの IRQL します。 呼び出すドライバーなど**KeRaiseIrql**相互の呼び出しを行う必要があります**KeLowerIrql**ことだけです。

優先順位を確認する方法の詳細については、次を参照してください。、[スケジュールやスレッドのコンテキストでは、IRQL](https://go.microsoft.com/fwlink/p/?linkid=59757)ホワイト ペーパー。

 

 





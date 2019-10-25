---
title: キャンセル セーフの IRP キュー
description: キャンセル セーフの IRP キュー
ms.assetid: a759d1e0-120f-4db9-9b84-ff921f2f5ba4
keywords:
- キャンセル-セーフな IRP キュー WDK カーネル
- コールバックルーチン WDK Irp
- WDK Irp の同期
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b23cf557de0c42d54618a4fc5887decb87ec4065
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828578"
---
# <a name="cancel-safe-irp-queues"></a>キャンセル セーフの IRP キュー





独自の IRP キューを実装するドライバーは、*キャンセルセーフな irp キュー*フレームワークを使用する必要があります。 キャンセルセーフな IRP キューは、IRP 処理を2つの部分に分割します。

1. ドライバーは、ドライバーの IRP キューに対する標準操作を実装するコールバックルーチンのセットを提供します。 指定された操作には、キューに対する Irp の挿入と削除、およびキューのロックとロック解除が含まれます。 「[キャンセルセーフな IRP キューの実装](#ddk-implementing-the-cancel-safe-irp-queue-kg)」を参照してください。

2. ドライバーがキューから IRP を実際に挿入または削除する必要がある場合は常に、システムによって提供される**IoCsq * Xxx*** ルーチンを使用します。 これらのルーチンは、ドライバーのすべての同期および IRP キャンセルロジックを処理します。

キャンセルセーフの IRP キューを使用するドライバーは、IRP のキャンセルをサポートするための[*キャンセル*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)ルーチンを実装しません。

このフレームワークにより、ドライバーによって Irp がアトミックに挿入され、キューから削除されるようになります。 また、IRP のキャンセルが正しく実装されていることも確認します。 フレームワークを使用しないドライバーは、挿入と削除を実行する前に、手動でキューをロックおよびロック解除する必要があります。 また、*キャンセル*ルーチンを実装するときに発生する可能性がある競合状態を回避する必要があります。 (発生する可能性のある競合状態の説明については、「 [IRP のキャンセルの同期](synchronizing-irp-cancellation.md)」を参照してください)。

キャンセルセーフな IRP キューフレームワークは、Windows XP 以降のバージョンの Windows に含まれています。 Windows 2000 および Windows 98/Me でも動作する必要があるドライバーは、Windows Driver Kit (WDK) に含まれている Csq .lib ライブラリにリンクできます。 Csq .lib ライブラリは、このフレームワークの実装を提供します。

**IoCsq * Xxx*** ルーチンは、Windows XP 以降のバージョンの Wdm と Ntddk で宣言されています。 Windows 2000 および Windows 98/Me でも動作する必要があるドライバーは、宣言に Csq を含める必要があります。

キャンセルセーフな IRP キューを使用する方法の完全なデモについては、「\\src\\全般\\WDK のディレクトリをキャンセルする」を参照してください。 これらのキューの詳細については、「[キャンセルセーフ IRP キューの制御フロー](https://go.microsoft.com/fwlink/p/?linkid=57844) 」ホワイトペーパーを参照してください。

### <a href="" id="ddk-implementing-the-cancel-safe-irp-queue-kg"></a>キャンセルセーフな IRP キューの実装

キャンセルセーフな IRP キューを実装するには、ドライバーが次のルーチンを提供する必要があります。

-   キューに Irp を挿入するには、次のいずれかのルーチンを実行します: [*Csqinsertirp*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_csq_insert_irp)または[*csqの*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_csq_insert_irp_ex)挿入 *Csqの Tirpq ex*は*Csqcmtirp*の拡張バージョンです。キューは、1つまたは他のを使用して実装されます。

-   指定された IRP をキューから削除する[*Csqremoveirp*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_csq_remove_irp)ルーチン。

-   キュー内の指定された IRP に続く次の IRP へのポインターを返す[*CsqPeekNextIrp*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_csq_peek_next_irp)ルーチン。 ここで、システムは[**IoCsqRemoveNextIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqremovenextirp)から受け取った*PeekContext*値を渡します。 ドライバーは、その値を任意の方法で解釈できます。

-   システムが IRP キュー: [*CsqAcquireLock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_csq_acquire_lock)と[*csqreleaselock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_csq_release_lock)をロックおよびロック解除できるルーチンは、次の2つです。

-   取り消された IRP を完了する[*CsqCompleteCanceledIrp*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_csq_complete_canceled_irp)ルーチン。

ドライバーのルーチンへのポインターは、キューを記述する[**IO\_CSQ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)構造体に格納されます。 ドライバーは、 **IO\_CSQ**構造のストレージを割り当てます。 **IO\_CSQ**構造は固定サイズのままであることが保証されているので、ドライバーはそのデバイス拡張機能内に構造を安全に埋め込むことができます。

ドライバーは、 [**IoCsqInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinitialize)または[**IoCsqInitializeEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinitializeex)のいずれかを使用して構造体を初期化します。 キューに[*CsqIoCsqInitialize Tirp*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_csq_insert_irp)が実装されている場合は、IoCsqInitializeEx を使用します。キューが*Csq tirpq ex*を実装している場合はを使用します。

ドライバーは、各コールバックルーチンに不可欠な機能のみを提供する必要があります。 たとえば、ロック処理を実装するのは、 *CsqAcquireLock*と*csqreleaselock*ルーチンだけです。 システムはこれらのルーチンを自動的に呼び出し、必要に応じてキューをロックおよびロック解除します。

適切なディスパッチルーチンが提供されていれば、任意の種類の IRP キューメカニズムをドライバーに実装できます。 たとえば、ドライバーはリンクリストとして、または優先キューとしてキューを実装できます。

[*Csqcmtirpq ex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_csq_insert_irp_ex)は、 [*Csqcmtirp*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_csq_insert_irp)よりもキューに対するより柔軟なインターフェイスを提供します。 ドライバーは、戻り値を使用して操作の結果を示すことができます。エラーコードが返された場合、挿入は失敗します。 *Csqの Tirp*ルーチンは値を返さないため、挿入が失敗したことを示す単純な方法はありません。 また、 *Csqinserttirpq ex*では、ドライバーによって定義された追加の*insertcontext*パラメーターを使用して、キューの実装で使用するドライバー固有の追加情報を指定できます。

ドライバーは*Csqの Tirpq ex*を使用して、より高度な IRP 処理を実装できます。 たとえば、保留中の Irp が存在しない場合、 *Csqの*セットアップルーチンはエラーコードを返すことができ、ドライバーは irp を直ちに処理できます。 同様に、Irp がキューに登録されなくなった場合は、 *Csqの*設定によってエラーコードを返すことができます。

ドライバーは、すべての IRP キャンセル処理から分離されています。 システムは、キュー内の Irp に対して[*キャンセル*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)ルーチンを提供します。 このルーチンは[*Csqremoveirp*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_csq_remove_irp)を呼び出して、キューから irp を削除し、 [*CsqCompleteCanceledIrp*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_csq_complete_canceled_irp)を実行して irp の取り消しを完了します。

次の図は、IRP のキャンセルの制御フローを示しています。

![irp キャンセルの制御フローを示す図](images/5cancelingirp.png)

[*CsqCompleteCanceledIrp*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_csq_complete_canceled_irp)の基本的な実装は次のとおりです。

```cpp
VOID CsqCompleteCanceledIrp(PIO_CSQ Csq, PIRP Irp) {
  Irp->IoStatus.Status = STATUS_CANCELLED;
  Irp->IoStatus.Information = 0;

  IoCompleteRequest(Irp, IO_NO_INCREMENT);
}
```

ドライバーは、任意のオペレーティングシステムの同期プリミティブを使用して、 [*CsqAcquireLock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_csq_acquire_lock)および[*Csqreleaselock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_csq_release_lock)ルーチンを実装できます。 使用可能な同期プリミティブには、[スピンロック](spin-locks.md)と[ミューテックスオブジェクト](mutex-objects.md)があります。

ドライバーがスピンロックを使用してロックを実装する方法の例を次に示します。

```cpp
/* 
  The driver has previously initialized the SpinLock variable with
  KeInitializeSpinLock.
 */

VOID CsqAcquireLock(PIO_CSQ IoCsq, PKIRQL PIrql)
{
    KeAcquireSpinLock(SpinLock, PIrql);
}

VOID CsqReleaseLock(PIO_CSQ IoCsq, KIRQL Irql)
{
    KeReleaseSpinLock(SpinLock, Irql);
}
```

システムは、IRQL 変数へのポインターを*CsqAcquireLock*と*Csqreleaselock*に渡します。 ドライバーがスピンロックを使用してキューのロックを実装している場合、ドライバーは、この変数を使用して、キューがロックされているときに現在の IRQL を格納できます。

スピンロックを使用するためにドライバーは必要ありません。 たとえば、ドライバーはミューテックスを使用してキューをロックできます。 ドライバーで使用できる同期方法の詳細については、「[同期方法](synchronization-techniques.md)」を参照してください。

### <a href="" id="ddk-using-the-cancel-safe-irp-queue-kg"></a>キャンセルセーフな IRP キューの使用

ドライバーは、Irp をキューに置いてデキューするときに、次のシステムルーチンを使用します。

-   次のいずれかの方法で、IRP をキューに挿入します: [**IoCsqInsertIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinsertirp)または[**IoCsqInsertIrpEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinsertirpex)。

-   [**IoCsqRemoveNextIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqremovenextirp)は、キュー内の次の IRP を削除します。 ドライバーは、必要に応じてキー値を指定できます。

次の図は、 [**IoCsqRemoveNextIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqremovenextirp)の制御フローを示しています。

![iocsqremovenextirp の制御フローを示す図](images/4iocsqremovenextirp.png)

-   [**IoCsqRemoveIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqremoveirp)は、指定された IRP をキューから削除します。

次の図は、 [**IoCsqRemoveIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqremoveirp)の制御フローを示しています。

![iocsqremoveirp の制御フローを示す図](images/3iocsqremoveirp.png)

これらのルーチンは、ドライバーによって提供されるルーチンにディスパッチされます。

[**IoCsqInsertIrpEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinsertirpex)ルーチンを使用すると、 *csqの*拡張機能にアクセスできます。 *Csqcmtirpq ex*によって返された状態値を返します。 呼び出し元は、この値を使用して、IRP が正常にキューに登録されたかどうかを判断できます。 また、 **IoCsqInsertIrpEx**では、呼び出し元が*Csqinsertti Ex*の insertcontext パラメーターの値を指定することもできます。

**IoCsqInsertIrp**と**IoCsqInsertIrpEx**の両方をキャンセルセーフキューで呼び出すことができることに注意してください。これは、キューに*csq Tirp*ルーチンまたは*csqの*設定済みルーチンがあるかどうかによって異なります。 どちらの場合も、 **IoCsqInsertIrp**は同じように動作します。 *CsqIoCsqInsertIrpEx Tirp*ルーチンを持つキューが渡されると、 **IoCsqInsertIrp**と同じように動作します。

次の図は、 [**IoCsqInsertIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinsertirp)の制御フローを示しています。

![iocsqinsertirp の制御フローを示す図](images/iocsqinsertirp.png)

次の図は、 [**IoCsqInsertIrpEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinsertirpex)の制御フローを示しています。

![iocsqinsertirpex の制御フローを示す図](images/2iocsqinitializeex.png)

**IoCsq * Xxx*** ルーチンを使用して、irp のキューとデキューを行うには、いくつかの自然な方法があります。 たとえば、ドライバーは単に Irp をキューに配置して、受信した順序で処理することができます。 ドライバーは、次のように IRP をキューに置いています。

```cpp
    status = IoCsqInsertIrpEx(IoCsq, Irp, NULL, NULL);
```

ドライバーが特定の Irp を区別する必要がない場合は、次のようにキューに登録されている順序で単にデキューできます。

```cpp
    IoCsqRemoveNextIrp(IoCsq, NULL);
```

また、ドライバーは特定の Irp をキューに置いてデキューすることもできます。 ルーチンは、非透過[**IO\_CSQ\_IRP\_CONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)構造体を使用して、キュー内の特定の irp を識別します。 ドライバーは、次のように IRP をキューに置いています。

```cpp
    IO_CSQ_IRP_CONTEXT ParticularIrpInQueue;
    IoCsqInsertIrp(IoCsq, Irp, &ParticularIrpInQueue);
```

その後、ドライバーは、 **IO\_CSQ\_irp\_コンテキスト**値を使用して同じ irp をデキューできます。

```cpp
    IoCsqRemoveIrp(IoCsq, Irp, &ParticularIrpInQueue);
```

ドライバーは、特定の条件に基づいてキューから Irp を削除することが必要になる場合もあります。 たとえば、ドライバーが各 IRP に優先順位を関連付け、優先度の高い Irp が最初にデキューされるようにします。 ドライバーは、 *PeekContext*値を[**IoCsqRemoveNextIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqremovenextirp)に渡すことがあります。この値は、システムがキューの次の IRP を要求したときにドライバーに戻されます。

 

 





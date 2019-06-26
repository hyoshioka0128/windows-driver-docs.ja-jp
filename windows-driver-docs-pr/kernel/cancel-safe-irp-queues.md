---
title: キャンセル セーフの IRP キュー
description: キャンセル セーフの IRP キュー
ms.assetid: a759d1e0-120f-4db9-9b84-ff921f2f5ba4
keywords:
- キャンセルの安全な IRP キュー WDK カーネル
- WDK Irp のコールバック ルーチン
- WDK Irp の同期
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34bd7a6dd81b0343e3ca6a0dd45f772206791cea
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377240"
---
# <a name="cancel-safe-irp-queues"></a>キャンセル セーフの IRP キュー





独自の IRP キューを実装するドライバーを使用する必要があります、*キャンセル セーフ IRP キュー*フレームワーク。 キャンセルの安全な IRP キュー IRP の処理を 2 つの部分に分かれています。

1. ドライバーは、一連の標準的なドライバーの IRP のキュー操作を実装するコールバック ルーチンを提供します。 指定された操作には、挿入と、キュー、およびロックとロック解除、キューからの Irp の削除が含まれます。 参照してください[キャンセル セーフ IRP のキューを実装する](#ddk-implementing-the-cancel-safe-irp-queue-kg)します。

2. システム標準を使用して、ドライバーは、実際に挿入または IRP をキューから削除する必要があります、たびに**IoCsq * Xxx*** ルーチン。 これらのルーチンでは、すべての同期と IRP がドライバーのロジックのキャンセルを処理します。

キャンセルの安全な IRP のキューを使用するドライバーを実装しない[*キャンセル*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel) IRP のキャンセルをサポートするルーチン。

フレームワークにより、ドライバーを挿入し、Irp をアトミックにそのキューから削除します。 IRP の取り消しを正しく実装することも確認します。 フレームワークを使用しないでくださいドライバーは、ロックし、任意の挿入および削除を実行する前に、キューのロックを解除する必要があります手動でします。 実装する場合に生じる競合状態を避ける必要がありますもこれらを*キャンセル*ルーチン。 (生じる可能性のある競合状態の説明は、次を参照してください[同期 IRP キャンセル](synchronizing-irp-cancellation.md)。)。

キャンセルの安全な IRP のキュー framework では、Windows XP および Windows の以降のバージョンに含まれています。 ドライバーが Windows 2000 および Windows 98 でも動作する必要があります]、[Windows Driver Kit (WDK) で含まれている Csq.lib ライブラリにリンクできます。 Csq.lib ライブラリは、このフレームワークの実装を提供します。

**IoCsq * Xxx*** ルーチンは、Windows XP と Wdm.h と Ntddk.h の以降のバージョンで宣言されます。 ドライバーが Windows 2000 および Windows 98 でも動作する必要があります]、[自分の宣言では、Csq.h を含める必要があります。

キャンセルの安全な IRP のキューを使用する方法の完全なデモを確認できます、 \\src\\全般\\WDK のディレクトリをキャンセルします。 これらのキューの詳細についてを参照してくださいも、[キャンセル セーフ IRP のキューのフローの制御](https://go.microsoft.com/fwlink/p/?linkid=57844)ホワイト ペーパー。

### <a href="" id="ddk-implementing-the-cancel-safe-irp-queue-kg"></a>キャンセルの安全な IRP のキューの実装

キャンセルの安全な IRP のキューを実装するには、ドライバーは、次のルーチンを提供する必要があります。

-   Irp をキューに挿入する次のルーチンのいずれか:[*CsqInsertIrp* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_csq_insert_irp)または[ *CsqInsertIrpEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_csq_insert_irp_ex)します。 *CsqInsertIrpEx*の拡張バージョンは、 *CsqInsertIrp*; キューは、どちらか一方を使用して実装されます。

-   A [ *CsqRemoveIrp* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_csq_remove_irp)ルーチンを指定した IRP をキューから削除します。

-   A [ *CsqPeekNextIrp* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_csq_peek_next_irp)ルーチンを次のキューに指定した IRP [次へ] の IRP にポインターを返します。 これは、システムが渡されます、 *PeekContext*から受信した値[ **IoCsqRemoveNextIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqremovenextirp)します。 ドライバーは、任意の方法では、その値を解釈できます。

-   両方のシステムをロックおよび IRP のキューをロック解除を許可するのには、次のルーチン:[*CsqAcquireLock* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_csq_acquire_lock)と[ *CsqReleaseLock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_csq_release_lock)します。

-   A [ *CsqCompleteCanceledIrp* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_csq_complete_canceled_irp)取り消された IRP の完了ルーチン。

ドライバーのルーチンへのポインターが格納されている、 [ **IO\_CSQ** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)キューを記述する構造体。 ドライバーの記憶域の割り当て、 **IO\_CSQ**構造体。 **IO\_CSQ**構造のため、ドライバーは、そのデバイスの拡張機能内の構造体を埋め込むことが安全に、固定サイズを維持することが保証されます。

ドライバーを使用するか[ **IoCsqInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqinitialize)または[ **IoCsqInitializeEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqinitializeex)構造体を初期化します。 使用**IoCsqInitialize**キューが実装されている場合[ *CsqInsertIrp*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_csq_insert_irp)、または**IoCsqInitializeEx**キューを実装している場合*CsqInsertIrpEx*します。

ドライバーは、各コールバック ルーチンで重要な機能を提供する必要がのみです。 例については、のみ、 *CsqAcquireLock*と*CsqReleaseLock*ルーチンは、ロック処理を実装します。 システムは、これらのルーチンをロックし、必要に応じて、キューのロック解除を自動的に呼び出します。

適切なディスパッチ ルーチンが用意されている限り、ドライバーでは、任意の種類の IRP のキュー メカニズムを実装できます。 などのドライバーは、リンク リスト、または優先順位キューとしてなどに、キューを実装します。

[*CsqInsertIrpEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_csq_insert_irp_ex)よりもより柔軟なインターフェイスをキューに[ *CsqInsertIrp*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_csq_insert_irp)します。 ドライバーは、その戻り値を使用して、操作の結果を示しますエラー コードが返された場合、挿入に失敗しました。 A *CsqInsertIrp*挿入が失敗したことを示す簡単な方法がないルーチンは、値を返しません。 また、 *CsqInsertIrpEx*追加ドライバー定義は*InsertContext*パラメーター キューの実装で使用される追加のドライバー固有の情報を指定するために使用できます。

ドライバーを使用できる*CsqInsertIrpEx*より高度な IRP の処理を実装します。 たとえば、保留中の Irp がない場合、 *CsqInsertIrpEx*ルーチンがエラー コードと、ドライバーは IRP をすぐに処理を返すことができます。 同様に、Irp をキューに不要になったことができる場合、 *CsqInsertIrpEx*事実を示すエラー コードを返すことができます。

ドライバーは IRP 取り消し処理をすべてから隔離されています。 システムが提供、 [*キャンセル*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel)キューに Irp の日常的な。 このルーチンを呼び出す[ *CsqRemoveIrp* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_csq_remove_irp) IRP をキューから削除して[ *CsqCompleteCanceledIrp* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_csq_complete_canceled_irp) IRP を完了するにはキャンセルします。

次の図は、IRP のキャンセルの制御のフローを示しています。

![irp のキャンセルの制御のフローを示す図](images/5cancelingirp.png)

基本的な実装[ *CsqCompleteCanceledIrp* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_csq_complete_canceled_irp)のとおりです。

```cpp
VOID CsqCompleteCanceledIrp(PIO_CSQ Csq, PIRP Irp) {
  Irp->IoStatus.Status = STATUS_CANCELLED;
  Irp->IoStatus.Information = 0;

  IoCompleteRequest(Irp, IO_NO_INCREMENT);
}
```

ドライバーは、オペレーティング システムの同期プリミティブのいずれかを実装に使用できる、 [ *CsqAcquireLock* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_csq_acquire_lock)と[ *CsqReleaseLock* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_csq_release_lock)ルーチン。 利用可能な同期プリミティブを含める[スピンロック](spin-locks.md)と[ミュー テックス オブジェクト](mutex-objects.md)します。

ドライバーをスピン ロックを使用してロック実装方法の例を次に示します。

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

システムが IRQL 変数へのポインターを渡します*CsqAcquireLock*と*CsqReleaseLock*します。 ドライバーは、キューのロックを実装するために、スピン ロックを使用している場合、ドライバーは、キューがロックされているときに、現在の IRQL を格納するこの変数を使用できます。

ドライバーは、スピン ロックを使用する必要はありません。 たとえば、ドライバーは、キューをロックするのにミュー テックスを使用できます。 ドライバーを利用できる同期手法については、次を参照してください。[同期手法](synchronization-techniques.md)します。

### <a href="" id="ddk-using-the-cancel-safe-irp-queue-kg"></a>キャンセルの安全な IRP のキューを使用します。

ドライバーは、キューとデキューを Irp ときに、次のシステム ルーチンを使用します。

-   IRP をキューに挿入するには、次のいずれか:[**IoCsqInsertIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqinsertirp)または[ **IoCsqInsertIrpEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqinsertirpex)します。

-   [**IoCsqRemoveNextIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqremovenextirp)をキューに IRP が [次へ] を削除します。 ドライバーは、キーの値を必要に応じて指定できます。

次の図は、フローの制御の[ **IoCsqRemoveNextIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqremovenextirp)します。

![iocsqremovenextirp の制御のフローを示す図](images/4iocsqremovenextirp.png)

-   [**IoCsqRemoveIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqremoveirp)指定 IRP をキューから削除します。

次の図は、フローの制御の[ **IoCsqRemoveIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqremoveirp)します。

![iocsqremoveirp の制御のフローを示す図](images/3iocsqremoveirp.png)

これらのルーチンは、さらに、ドライバーによって提供されるルーチンにディスパッチします。

[ **IoCsqInsertIrpEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqinsertirpex)ルーチンの拡張機能へのアクセスを提供する、 *CsqInsertIrpEx*ルーチン。 によって返されたステータス値を返す*CsqInsertIrpEx*します。 呼び出し元は、かどうか IRP が正常にキューに置かれたかどうかを判断するのにこの値を使用できます。 **IoCsqInsertIrpEx** 、呼び出し元の InsertContext パラメーターの値を指定することができます*CsqInsertIrpEx*します。

なお両方**IoCsqInsertIrp**と**IoCsqInsertIrpEx**キューがあるかどうか、すべてのキャンセルの安全なキューで呼び出すことができます、 *CsqInsertIrp*ルーチンまたは*CsqInsertIrpEx*ルーチン。 **IoCsqInsertIrp**いずれの場合も同じ動作です。 場合**IoCsqInsertIrpEx**を持つキューが渡される、 *CsqInsertIrp* 、日常的な動作と同様に**IoCsqInsertIrp**します。

次の図は、フローの制御の[ **IoCsqInsertIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqinsertirp)します。

![iocsqinsertirp の制御のフローを示す図](images/iocsqinsertirp.png)

次の図は、フローの制御の[ **IoCsqInsertIrpEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqinsertirpex)します。

![iocsqinsertirpex の制御のフローを示す図](images/2iocsqinitializeex.png)

使用するいくつかの自然な方法がある、 **IoCsq * Xxx*** ルーチンをキューに登録し、Irp をデキューします。 たとえば、ドライバーでは、Irp が受信した順序で処理される可能性がありますキューにだけです。 ドライバーは IRP をとおり queue でした。

```cpp
    status = IoCsqInsertIrpEx(IoCsq, Irp, NULL, NULL);
```

ドライバーが特定の Irp を区別するために必要ない場合、でしたし、単にデキューを入れられた、次のように順番。

```cpp
    IoCsqRemoveNextIrp(IoCsq, NULL);
```

または、ドライバーは、キューし、特定の Irp のデキューします。 ルーチンは、使用、不透明な[ **IO\_CSQ\_IRP\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)キュー内の特定の Irp を識別するために構造体。 ドライバーは IRP を次のようにキューします。

```cpp
    IO_CSQ_IRP_CONTEXT ParticularIrpInQueue;
    IoCsqInsertIrp(IoCsq, Irp, &ParticularIrpInQueue);
```

ドライバーを使用して同じ IRP をデキューできますし、 **IO\_CSQ\_IRP\_コンテキスト**値。

```cpp
    IoCsqRemoveIrp(IoCsq, Irp, &ParticularIrpInQueue);
```

ドライバーは Irp を特定の条件に基づくキューから削除する必要もあります。 たとえば、ドライバー可能性があります、優先順位を関連付ける各 IRP では、優先順位の高い Irp が最初にデキューを取得するよう。 ドライバーに合格しても、 *PeekContext*値を[ **IoCsqRemoveNextIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocsqremovenextirp)キュー内の [次へ] の IRP を要求する場合に、ドライバーに、システムを通過します。

 

 





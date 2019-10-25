---
title: IRP をキャンセルするときに考慮すべき点
description: IRP をキャンセルするときに考慮すべき点
ms.assetid: 16a47033-7147-43a2-a9f8-a215f7e90ff1
keywords:
- Irp の取り消し、ガイドライン
- キャンセルルーチン、ガイドライン
- 取り消し可能 Irp WDK カーネル
- 現在の状態 WDK Irp
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: 204fede34d4eee53b48e570630e45659a6dcca00
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827667"
---
# <a name="points-to-consider-when-canceling-irps"></a>IRP をキャンセルするときに考慮すべき点





ここでは、キャンセルルーチンを実装し、*キャンセル*可能な irp を処理するためのガイドラインについて説明します。 取り消し可能な Irp の処理の詳細については、「[キャンセルセーフ Irp キューの制御フロー](https://go.microsoft.com/fwlink/p/?linkid=57844)」を参照してください。

### <a name="general-guidelines-for-all-cancel-routines"></a>すべてのキャンセルルーチンに関する一般的なガイドライン

I/o マネージャーは、ドライバーの*キャンセル*ルーチンを呼び出すたびに、キャンセルスピンロックを保持します。 そのため、すべての*キャンセル*ルーチンは次のことを行う必要があります。

-   制御を返す前に[**IoReleaseCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))を呼び出してください。

-   **IoReleaseCancelSpinLock**を最初に呼び出す場合を除き、 [**IoAcquireCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548196(v=vs.85))を呼び出しません。

-   **IoAcquireCancelSpinLock**に対して行われる各呼び出しに対して、 **IoReleaseCancelSpinLock**の相互呼び出しを作成します。

*キャンセル*ルーチンが**IoReleaseCancelSpinLock**を呼び出すたびに、最後の呼び出しによって返された IRQL を**IoAcquireCancelSpinLock**に渡す必要があります。 I/o マネージャーによって取得された (*キャンセル*ルーチンが呼び出されたときに保持されていた) スピンロックを解除する場合、*キャンセル*ルーチンは、 **Irp&gt;cancelirql**に渡す必要があります。

デッドロックが発生する可能性があるため、スピンロックを保持したまま、ドライバーが外部ルーチン ( **IoCompleteRequest**など) を呼び出すことはできません。

### <a href="" id="using-the-queue-defined-by-the-i-o-manager-"></a>I/o マネージャーによって定義されたキューを使用する

ドライバーが Irp の内部キューを管理する場合を除き、*キャンセル*ルーチンは次のいずれかの受信 irp で呼び出されます。

-   入力ターゲットデバイスオブジェクトの中**Entirp**

-   ターゲットデバイスオブジェクトに関連付けられているデバイスキュー内のエントリ

ドライバーが Irp の内部キューを管理する場合を除き、*キャンセル*ルーチンは、ターゲットデバイスオブジェクトに関連付けられたデバイスキュー内のエントリであるかどうかをテストするために、入力 IRP で[**Keremoveentrydevicequeue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keremoveentrydevicequeue)を呼び出す必要があります。 ドライバーの*キャンセル*ルーチンは、指定された IRP がデバイスキュー内の特定の位置にあることを想定できないため、 **keremovedevicequeue**または**keremovebykeydevicequeue**を呼び出す*ことができません*。

### <a name="current-state-of-the-input-irp"></a>入力 IRP の現在の状態

ドライバーが既に i/o 処理を開始している IRP で*キャンセル*ルーチンが呼び出され、要求が間もなく完了する場合、*キャンセル*ルーチンはシステムのキャンセルスピンロックを解除し、制御を戻します。

入力 IRP の現在の状態が保留中の場合、*キャンセル*ルーチンは次の操作を行う必要があります。

1.  **ステータスが [キャンセル**] で、**情報**が0の場合は、入力 IRP の i/o 状態ブロックを\_に設定します。

2.  システムのキャンセルスピンロックを含め、保持しているすべてのスピンロックを解除します。

3.  指定された IRP で[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出します。

### <a name="holding-irps-in-a-cancelable-state"></a>Irp をキャンセル可能な状態に保持する

キャンセル可能な状態の IRP を保持するドライバールーチンは、 [**Iomarkirppending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)を呼び出す必要があります。また、irp 内の*キャンセル*ルーチンのエントリポイントを設定するには、 [**iosetcancelルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcancelroutine)を呼び出す必要があります。 その後は、そのドライバールーチンが**Iostartpacket**、 **IoAllocateController**、ExInterlockedInsert などの追加のサポートルーチンを呼び出すことができます。 **リスト**ルーチン。

その後、キャンセル可能な Irp を処理するすべてのドライバールーチンは、要求を満たすために操作を開始する前に、IRP が既にキャンセルされているかどうかを確認する必要があります。 ルーチンは、IRP 内の*Cancel*ルーチンのエントリポイントを**NULL**にリセットするために**iosetcancelroutine**を呼び出す必要があります。 そのルーチンが、入力 IRP の i/o 処理を開始できるようになります。

場合によっては、IRP 内の*キャンセル*ルーチンのエントリポイントもリセットする必要があります。これにより、他のドライバールーチンによってさらに処理するために irp が渡され、それらの irp がキャンセル可能な状態で保持される場合があります。

IRP をキャンセル可能な状態に保持する上位レベルのドライバーは、 **IoCallDriver**を使用して irp を次の下位のドライバーに渡す前に、その*取り消し*エントリポイントを**NULL**にリセットする必要があります。

### <a name="canceling-an-irp"></a>IRP をキャンセルする

上位レベルのドライバーはいずれも、割り当てられて渡された IRP を使用して[**Iocancelirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocancelirp)を呼び出し、下位レベルのドライバーによる処理をさらに進めることができます。 ただし、このようなドライバーでは、指定された IRP が、下位のドライバーによってキャンセルされた状態\_、完了したと見なすことはできません。

### <a name="synchronization"></a>同期

ドライバーは、Irp の取り消し可能な状態を追跡するために、デバイス拡張機能に追加の状態情報を保持します (または、その設計によっては必要があります)。 この状態が、IRQL &lt;= ディスパッチ\_レベルで実行されているドライバールーチンによって共有されている場合は、ドライバーによって割り当てられた、初期化されたスピンロックを使用して共有データを保護する必要があります。

ドライバーは、システムのキャンセルスピンロックとその独自のスピンロックの購入とリリースを慎重に管理する必要があります。 システムのキャンセルスピンロックは、可能な限り最短の間隔で保持する必要があります。 取り消し可能な IRP にアクセスする前に、このようなドライバーは常に[**Iosetcancelroutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcancelroutine)の戻り値をチェックして、*キャンセル*ルーチンが既に実行されている (または実行しようとしている) かどうかを確認する必要があります。その場合は、*キャンセル*ルーチンで IRP を完了させる必要があります。

デバイスドライバーが、さまざまなドライバールーチンが ISR と共有するキャンセル可能な Irp に関する状態情報を保持する場合、これらのルーチンは、ISR との共有状態へのアクセスを同期する必要があります。 マルチプロセッサセーフな方法で、ISR と共有されている状態情報にアクセスできるのは、ドライバーによって提供される*SynchCritSection*ルーチンだけです。

詳細については、「[同期の手法](synchronization-techniques.md)」を参照してください。

 

 





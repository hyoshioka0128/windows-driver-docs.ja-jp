---
title: IRP のキューとデキュー
description: IRP のキューとデキュー
ms.assetid: 736107bf-4790-4562-8785-c37fbbed03d3
keywords:
- Irp WDK カーネルでは、キュー
- キューの Irp
- Irp をデキューする.
- WDK のカーネルを処理する複数の I/O 要求
- IRP キュー WDK カーネルの内部
- WDK Irp の同期
- I/O 操作の開始
- I/O WDK カーネルでは、開始操作
- StartIo ルーチン
- キャンセルの安全な IRP キュー WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04ff9062fc46d403ecd8bbcc4db244431b459e52
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378756"
---
# <a name="queuing-and-dequeuing-irps"></a>IRP のキューとデキュー





I/O マネージャーは、マルチタス キング、マルチ スレッド システム内での非同期 I/O をサポートするためにデバイス I/O 要求はそのドライバーが完了すると、特にマルチプロセッサ コンピューターでを処理できるよりも高速取得できます。 その結果、Irp の特定のデバイスにバインドされている必要がありますキューに入れられ、ドライバーでそのデバイスが別の IRP の処理でビジー状態では既にします。

そのため、最下位レベルのドライバーには、次のいずれかが必要です。

-   A [ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio) 、日常的な I/O マネージャーが Irp の I/O 操作を開始するドライバーを呼び出しますがキューに登録するシステム提供の IRP キュー (を参照してください[ **IoStartPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartpacket)).

-   内部 IRP のキューおよびデキューのメカニズムは、それよりも高速には Irp を管理するドライバーを使用して満たすことが。 ドライバーは、デバイスのキュー、インタロックされたキュー、またはキャンセルの安全なキューを使用できます。 詳細については、次を参照してください。 [Driver-Managed IRP キュー](driver-managed-irp-queues.md)します。

最下位レベルのデバイス ドライバを満たすことができます、ディスパッチ ルーチンですべての可能な IRP の完了を必要なしのみ*StartIo*ルーチンと Irp のドライバー管理キューがありません。

高度なドライバーがほとんどないが*StartIo*ルーチン。 ほとんどの中間ドライバーでは、どちらも必要がある*StartIo*ルーチンも内部キュー中間のドライバーできます通常そのディスパッチ ルーチンから有効なパラメーター Irp を渡すとはどのような後処理が任意の IRP で必要です。その[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)ルーチン。

以下に示します、一般に、設計の考慮事項を実装するかどうかを決定するためのいくつか、 *StartIo* Irp の内部のドライバー管理キューの有無ルーチン。

### <a name="startio-routines-in-drivers"></a>ドライバーで StartIo ルーチン

コンピューター周辺機器、一度に 1 つだけのデバイスの I/O 操作を処理できる、デバイス ドライバーを実装できます*StartIo*ルーチン。 I/O マネージャーは、これらのドライバーの[ **IoStartPacket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartpacket)と[**います**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartnextpacket)キューおよびデキューを Irp をルーチンとシステム提供の IRP キューです。

詳細については*StartIo*ルーチンを参照してください[StartIo ルーチンを記述](writing-a-startio-routine.md)します。

### <a name="internal-queues-for-irps-in-drivers"></a>Irp がドライバーでの内部キュー

デバイスは、同時実行の 1 つ以上の I/O 操作をサポートできますが、最下位レベルのデバイス ドライバーのでは内部要求キューを設定し、独自 Irp のキューを管理する必要があります。 たとえば、システム シリアル ドライバーは、別のキューの読み取り、書き込み、削除、および全二重シリアル デバイスをサポートしているために、そのデバイスでの操作を待機を保持します。

いくつかの基になるデバイスのドライバーに要求を送信するより高度なドライバーが Irp の内部キューを維持することがありますもできます。 たとえば、ファイル システム ドライバーは、Irp の内部キューをほぼ常にあります。

詳細については、次を参照してください。 [Driver-Managed IRP キュー](driver-managed-irp-queues.md)します。

### <a name="internal-queue-synchronization"></a>内部キューの同期

デバイス専用のスレッドと、通常は Irp の自分のキューを設定 (ほとんどのファイル システム ドライバーを含む) 実行ワーカー スレッドを使用する最上位レベルのドライバーのドライバーです。 キューは Irp を処理するその他のドライバー ルーチンとドライバーのスレッドまたはワーカー スレッドをドライバーが指定したコールバックによって共有されます。

独自のキューの構造を実装するドライバーには、キューへのアクセスが同期されていると、取り消された Irp がキューから削除する必要がありますを確認します。 ドライバーのライターのこのタスクを簡素化するには、は、キャンセルの安全な IRP のキューは、標準的なフレームワーク、IRP のキューを実装する場合に使用することができますを提供します。 参照してください[キャンセル セーフ IRP キュー](cancel-safe-irp-queues.md)詳細についてはします。 これは、IRP のキューを実装するための推奨される方法です。

ドライバーは IRP キューのすべての同期を実装し、ロジックを明示的にキャンセルできます。 たとえば、ドライバーは、インタロックされたキューを使用できます。 ドライバーのディスパッチ ルーチンは、インタロックされたキューおよびドライバーが作成したスレッドに Irp を挿入するか、ドライバーのワーカー スレッドのコールバックを削除して呼び出すことによって、 **ExInterlocked*Xxx*一覧**サポートルーチン。

たとえば、システム フロッピー コント ローラーのドライバーは、インタロックされたキューを使用します。 そのデバイス専用のスレッドが他のデバイス ドライバーのによって行われる Irp の同じ処理を行います*StartIo*ルーチンとその他のデバイス ドライバーのによって行われる同じ Irp の処理の一部を[ *DpcForIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine)ルーチン。

### <a name="internal-queues-with-startio-routines-in-drivers"></a>ドライバーで StartIo ルーチンでキューの内部

独自の内部キューを管理するドライバーを持つことも、 *StartIo*ルーチン必要はありませんが、します。 いずれかがあるほとんどの最下位レベルのデバイス ドライバー、 *StartIo*ルーチンまたは独自の Irp では、両方ではなくキューを管理します。

SCSI ポート ドライバーには、例外、 *StartIo*ルーチンおよび Irp の内部キューを管理します。 I/O マネージャーが Irp をポート ドライバーのキューに入れ*StartIo* SCSI HBA を表すデバイスのドライバーが作成したオブジェクトに関連付けられているデバイスのキューで日常的な。 SCSI ポート ドライバーも設定し、Irp のマシンの場合は、任意 HBA ドリブン SCSI バス上の (SCSI 論理ユニットに対応する) 各ターゲット デバイスにデバイスのキューを管理します。

SCSI ポート ドライバーでは、SCSI バス上の任意のデバイスが特に負荷の高いたびに Irp が SCSI のクラス ドライバー LU 固有のキューから送信を保持するために、補足的なデバイス キューを使用します。 実際には、このドライバーの補足、LU 固有のデバイスのキューは、その HBA の SCSI バス上の各デバイスをできるだけビジー状態で維持しながら、HBA 経由の異種の SCSI デバイスの操作をシリアル化する、SCSI ポート ドライバーを使用します。

 

 





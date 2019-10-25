---
title: IRP のキューとデキュー
description: IRP のキューとデキュー
ms.assetid: 736107bf-4790-4562-8785-c37fbbed03d3
keywords:
- Irp WDK カーネル、キュー
- キューの Irp
- Irp のデキュー
- 複数の i/o 要求による WDK カーネルの処理
- 内部 IRP キュー WDK カーネル
- WDK Irp の同期
- i/o 操作の開始
- I/o WDK カーネル、操作開始
- StartIo ルーチン
- キャンセル-セーフな IRP キュー WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 067b8a95987ec8415117aeca88461dd7143cc7d1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827581"
---
# <a name="queuing-and-dequeuing-irps"></a>IRP のキューとデキュー





I/o マネージャーでは、マルチタスクおよびマルチスレッドシステム内の非同期 i/o がサポートされるため、デバイスへの i/o 要求は、そのドライバーが、特にマルチプロセッサコンピューターでは、そのドライバーによって処理されるようになります。 そのため、特定のデバイスにバインドされている Irp は、デバイスが別の IRP を処理しているときに、ドライバーでキューに入れられる必要があります。

そのため、最下位レベルのドライバーには、次のいずれかが必要です。

-   [*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチン。 i/o マネージャーが irp の i/o 操作を開始するために、システムによって提供される irp キューのキューに登録されています (「 [**iostartpacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartpacket)」を参照してください)。

-   内部の IRP キューとデキューメカニズム。ドライバーは、このメカニズムを使用して、より高速な Irp を管理します。 ドライバーは、デバイスキュー、インタロックしたキュー、またはキャンセルセーフキューを使用できます。 詳細については、「[ドライバーによって管理される IRP キュー](driver-managed-irp-queues.md)」を参照してください。

ディスパッチルーチン内のすべての IRP を満たすことができる最低レベルのデバイスドライバーのみが、Irp に対して*StartIo*ルーチンを使用したり、ドライバーで管理されたキューを使用したりすることはできません。

上位レベルのドライバーには、ほとんどの場合、 *StartIo*ルーチンがありません。 ほとんどの中間ドライバーには、 *StartIo*ルーチンも内部キューもありません。中間ドライバーは、通常、有効なパラメーターを持つ Irp をディスパッチルーチンから渡し、その[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチン内の任意の irp に必要なすべての後処理を実行できます。

ここでは、Irp に対してドライバーで管理された内部キューを使用するかどうかに関係なく、 *StartIo*ルーチンを実装するかどうかを決定するための設計上の考慮事項について、一般的に説明します。

### <a name="startio-routines-in-drivers"></a>ドライバーの StartIo ルーチン

一度に1つのデバイス i/o 操作のみを処理できるコンピューター周辺機器の場合、デバイスドライバーは*StartIo*ルーチンを実装できます。 これらのドライバーについては、i/o マネージャーによって、システムによって提供される IRP キューとの間で Irp をキューにしたりデキューしたりするための[**iostartpacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartpacket)ルーチンと[**iostartnextnextpacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket)ルーチンが用意されています。

*StartIo*ルーチンの詳細については、「 [StartIo ルーチンの記述](writing-a-startio-routine.md)」を参照してください。

### <a name="internal-queues-for-irps-in-drivers"></a>ドライバー内の Irp の内部キュー

デバイスが複数の同時 i/o 操作をサポートできる場合、その最下位レベルのデバイスドライバーで内部要求キューを設定し、Irp の独自のキューを管理する必要があります。 たとえば、システムのシリアルドライバーは、すべての二重シリアルデバイスをサポートするため、デバイスに対する読み取り、書き込み、消去、待機の各操作用に個別のキューを保持します。

いくつかの基になるデバイスドライバーに要求を送信する上位レベルのドライバーも、Irp の内部キューを維持する場合があります。 たとえば、ファイルシステムドライバーには、ほとんどの場合、Irp の内部キューがあります。

詳細については、「[ドライバーによって管理される IRP キュー](driver-managed-irp-queues.md)」を参照してください。

### <a name="internal-queue-synchronization"></a>内部キューの同期

デバイス専用のスレッドを使用するドライバーと、executive ワーカースレッドを使用する最上位レベルのドライバー (ほとんどのファイルシステムドライバーを含む) は、通常、Irp 用に独自のキューを設定します。 キューは、ドライバースレッドまたはドライバーによって提供されるワーカースレッドコールバックと、Irp を処理する他のドライバールーチンによって共有されます。

独自のキュー構造を実装するドライバーは、キューへのアクセスが同期され、キャンセルされた Irp がキューから削除されることを保証する必要があります。 このタスクをドライバー作成者にとって簡単にするために、キャンセルセーフな IRP キューには、IRP キューを実装するときに使用できる標準のフレームワークが用意されています。 詳細については[、「キャンセルセーフな IRP キュー](cancel-safe-irp-queues.md) 」を参照してください。 これは、IRP キューを実装する場合に推奨される方法です。

ドライバーは、すべての IRP キュー同期とキャンセルロジックを明示的に実装することもできます。 たとえば、ドライバーは、インタロックキューを使用できます。 ドライバーのディスパッチルーチンは、ロックされたキューに Irp を挿入し、ドライバーによって作成されたスレッドまたはドライバーのワーカースレッドのコールバックは、 **Exinterlocked ロック*Xxx*リスト**サポートルーチンを呼び出してそれらを削除します。

たとえば、システムのフロッピーコントローラードライバーは、インタロックされたキューを使用します。 デバイス専用スレッドは、他のデバイスドライバーの*StartIo*ルーチンによって実行される irp の処理と、他のデバイスドライバーの[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)ルーチンによって実行される同じ irp の処理を処理します。

### <a name="internal-queues-with-startio-routines-in-drivers"></a>ドライバー内の StartIo ルーチンを使用した内部キュー

独自の内部キューを管理するドライバーも*StartIo*ルーチンを持つことができますが、そうする必要はありません。 最下位レベルのデバイスドライバーには、 *StartIo*ルーチンがあるか、または irp の独自のキューが管理されていますが、両方がありません。

この例外は、 *StartIo*ルーチンがあり、irp の内部キューを管理する SCSI ポートドライバーです。 I/o マネージャーは、SCSI HBA を表すドライバーによって作成されたデバイスオブジェクトに関連付けられているデバイスキューで、ポートドライバーの*StartIo*ルーチンの irp をキューに置いています。 また、SCSI ポートドライバーは、コンピューターの任意の HBA 駆動型 SCSI バス上の各ターゲットデバイス (SCSI 論理ユニットに対応) に対する Irp のデバイスキューを設定し、管理します。

Scsi ポートドライバーは、追加のデバイスキューを使用して、SCSI バス上の任意のデバイスが特にビジー状態になったときに、LU 固有のキューにある SCSI クラスドライバーから送信される Irp を保持します。 実際には、このドライバーの追加の LU 固有のデバイスキューを使用すると、SCSI ポートドライバーは HBA を介して異種 SCSI デバイスの操作をシリアル化しながら、各デバイスを可能な限りビジー状態にすることができます。

 

 





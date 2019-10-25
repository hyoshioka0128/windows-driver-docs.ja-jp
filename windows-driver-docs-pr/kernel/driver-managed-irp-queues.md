---
title: ドライバーで管理される IRP キュー
description: ドライバーで管理される IRP キュー
ms.assetid: b701e4aa-96ba-44af-96a5-b6cecf075bac
keywords:
- デバイスキュー WDK Irp、オブジェクト
- Irp WDK カーネル、キュー
- キューの Irp
- Irp のデキュー
- 内部 IRP キュー WDK カーネル
- キャンセル-セーフな IRP キュー WDK カーネル
- ドライバーで管理される IRP キューの WDK カーネル
- 補足の IRP キュー WDK カーネル
- インタロック IRP キュー WDK カーネル
- デバイスキュー WDK Irp
- デバイスは、デバイスキューに関する WDK Irp をキューに置いて
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2da091e089dcb0bcdf4b6df0fef11bc1f6e1335e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838719"
---
# <a name="driver-managed-irp-queues"></a>ドライバーで管理される IRP キュー





ファイルシステムドライバーを除き、i/o マネージャーは、デバイスキューオブジェクト (キュー Irp 用) を、ドライバーが作成する各デバイスオブジェクトに関連付けます。

ほとんどのデバイスドライバーは、関連付けられているデバイスキューを使用するために i/o マネージャーのサポートルーチンを呼び出します。これは、ターゲットデバイスオブジェクトのデバイス i/o 要求が、ドライバーによって処理されてから完了するまでの時間がかかるたびに、Irp を保持します。 この手法では、Irp はドライバーが提供する[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチンのキューに登録されます。

最適なパフォーマンスを得るために、ほとんどの中間ドライバーは、Irp を低レベルのドライバーに渡すだけで、そのデバイスオブジェクトに関連付けられているデバイスキューを使用することはほとんどありません。

ただし、1つ以上のデバイスキュー、インタロックされたキュー、またはキャンセルセーフキューを明示的に設定することによって、Irp の内部キューを管理するようにドライバーを設計できます。 この方法は、ドライバーが i/o 操作と重複するデバイスを制御する場合に特に便利です。 このようなデバイスでは、1つのキューのみを使用して、同じターゲットデバイスオブジェクトの2つ以上の Irp の同時処理を管理することが困難な場合があります。

内部キューを構築する最も簡単な方法は、キャンセルセーフの IRP queue フレームワークを使用することです。 任意のキューメカニズムをドライバーに実装できます。 その後、 [**IoCsqInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinitialize)を使用して、IRP の挿入と削除を処理するコールバックルーチンのセットを登録し、キューのロックとロック解除を行うことができます。 キャンセルセーフな IRP キューフレームワークには、 [**IoCsqInsertIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinsertirp)、 [**IoCsqRemoveIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqremoveirp)、および[**IoCsqRemoveNextIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqremovenextirp)ルーチンが用意されており、コールバックルーチンを使用して、ドライバーのキューから irp を安全に挿入したり削除したりできます。 また、コールバックルーチンを使用して、取り消されたすべての Irp を安全に削除します。

また、異種物理デバイスのセットについて、デバイスコントローラーのドライバーで Irp の補足キューを設定することもできます。 たとえば、SCSI ポートドライバーは、内部キューのデバイスキューオブジェクトを使用します。 このドライバーには、 *StartIo*ルーチンがあります。また、デバイスキューオブジェクトは、HBA を表すために作成するデバイスオブジェクトに関連付けられているデバイスキューに加えて、補足キューとして設定されます。 SCSI ポートドライバーは、追加のデバイスキューを使用して、HBA で制御される SCSI バス上の特定の論理ユニットにバインドされた Irp を保持します。

システムフロッピーコントローラードライバーは、 *StartIo*ルーチンがなく、インタロックされたキューを使用するドライバーの例です。 このドライバーは、二重にリンクされたインタロックされたキューを設定します。このキューから、ドライバーとそのデバイス専用のスレッドが Irp を挿入および削除します。

カーネルは、デバイスキューオブジェクトの種類を定義します。 Executive サポートコンポーネントには、インタロックされたキューの Irp を挿入または削除するためのルーチンが用意されています。 Windows XP 以降のバージョンの Windows 用ドライバーでは、[キャンセルセーフな irp キュー](cancel-safe-irp-queues.md)を使用して、irp キューを処理できます。

次のセクションでは、デバイスキュー、インタロックされたキュー、およびキャンセルセーフキューを使用する方法について説明します。

[デバイスキューの設定と使用](setting-up-and-using-device-queues.md)

[デバイスキューの管理](managing-device-queues.md)

[インタロックされたキューの設定と使用](setting-up-and-using-interlocked-queues.md)

[ドライバーで作成されたスレッドを使用したインタロックされたキューの管理](managing-interlocked-queues-with-a-driver-created-thread.md)

[キャンセル-セーフな IRP キュー](cancel-safe-irp-queues.md)

 

 





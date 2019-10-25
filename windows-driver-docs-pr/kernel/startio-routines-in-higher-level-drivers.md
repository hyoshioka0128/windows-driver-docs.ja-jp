---
title: 上位レベル ドライバーの StartIo ルーチン
description: 上位レベル ドライバーの StartIo ルーチン
ms.assetid: 8b0e3bef-4a73-4cf8-b71a-6aedf451d648
keywords:
- StartIo ルーチン、上位レベルのドライバー
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a046837efd0651f36525aaa1dd3c34d23cabb6e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838407"
---
# <a name="startio-routines-in-higher-level-drivers"></a>上位レベル ドライバーの StartIo ルーチン





すべての上位レベルのドライバーは、 [*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチンを持つことができます。 ただし、このようなドライバーは、既存の下位レベルのドライバーと相互運用できない可能性があり、パフォーマンス特性が低下する可能性があります。

上位レベルのドライバーの*StartIo*ルーチンには、次のような影響があります。

-   受信した Irp は、ドライバーの*ディスパッチ*Xxx ルーチンから[**iostartpacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartpacket)を呼び出し、 [*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンから[**iostartnextpacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket)を呼び出してキューに入れることができます。これにより、irp が一度に1つずつ処理されるようになります *。StartIo*ルーチン。

-   *StartIo*ルーチンがボトルネックになる可能性があるため、大量の i/o 要求が発生しても、ドライバーの i/o スループットが著しく低下する可能性があります。

-   ドライバーの*StartIo*ルーチンは、IRQL = ディスパッチ\_レベルで各 IRP を使用して[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出します。これにより、すべての下位ドライバーのディスパッチルーチンも、IRQL = dispatch\_レベルで実行されます。 これにより、ドライバーがディスパッチルーチンで呼び出すことができる一連のサポートルーチンが制限されます。 ほとんどのドライバーライターは、ドライバーのディスパッチルーチンが IRQL &lt; ディスパッチ\_レベルで実行されることを想定しているため、上位レベルのドライバーは、既存の下位レベルの多くのドライバーと相互運用できない可能性があります。

-   *StartIo*ルーチンは、システム全体のスループットを削減します。これは、チェーン内のすべての下位レベルのドライバーのディスパッチルーチンが、IRQL = ディスパッチ\_レベルで実行されるためです。

    標準ドライバールーチンを実行する IRQLs の詳細については、「[ハードウェアの優先順位の管理](managing-hardware-priorities.md)」を参照してください。

システムで提供されている上位レベルのドライバーには*StartIo*ルーチンがありません。これは、ドライバー自体、それより上のすべてのドライバー、およびシステム全体に対する IRP 処理が遅くなる可能性があるためです。

上位レベルのドライバーの多くは、ディスパッチルーチンから低レベルのドライバーに Irp を送信し、 *Iocompletion*ルーチンで必要なクリーンアップ処理を実行するだけです。

ただし、上位レベルのドライバーでは、特定の種類の操作を要求する Irp の内部キューを設定したり、SCSI ポートドライバーなどのさまざまな基になるデバイスのセットにバインドされた Irp を保持するように内部キューを設定したりできます。 詳細については、「 [irp のキューとデキュー](queuing-and-dequeuing-irps.md)」を参照してください。

 

 





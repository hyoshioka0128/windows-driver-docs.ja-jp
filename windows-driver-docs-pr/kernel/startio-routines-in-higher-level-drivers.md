---
title: 上位レベル ドライバーの StartIo ルーチン
description: 上位レベル ドライバーの StartIo ルーチン
ms.assetid: 8b0e3bef-4a73-4cf8-b71a-6aedf451d648
keywords:
- StartIo ルーチンより高度なドライバー
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bea19bcbe9d06991ba212fe61b66945dfbc40a04
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382989"
---
# <a name="startio-routines-in-higher-level-drivers"></a>上位レベル ドライバーの StartIo ルーチン





高度なドライバーが持つことができます、 [ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)ルーチン。 ただし、このようなドライバーを使用して、既存の下位レベルのドライバーと相互運用する可能性がありますすることがなく、特徴のパフォーマンスが低下する可能性があります。

A *StartIo*ドライバーでは上位レベルのルーチンに次の効果があります。

-   受信 Irp が呼び出すことによってキューに格納可能[ **IoStartPacket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartpacket)からドライバーの*ディスパッチ*Xxx routine(s) と[**います** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartnextpacket)からその[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine) routine(s)、原因となり、ある Irp の処理を一度に 1 つずつ、 *StartIo*ルーチンです。

-   大量の I/O 要求の期間中に、ドライバーの I/O スループットが著しく遅くなる可能性がありますので、その*StartIo*ルーチンがボトルネックになることができます。

-   ドライバーの*StartIo*ルーチンの呼び出し[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver) IRQL で各 IRP = ディスパッチ\_レベル、それによってすべての下位のドライバーのディスパッチの原因IRQL で実行するためにもルーチン = ディスパッチ\_レベル。 これは、下位のドライバーがディスパッチ ルーチン内で呼び出すことができるサポート ルーチンのセットを制限します。 ほとんどのドライバー作成者には、そのドライバーのディスパッチ ルーチンの IRQL で実行が前提としていますので&lt;ディスパッチ\_レベルより高いレベルのドライバーは、多くの既存の下位のドライバーと相互運用する可能性がありますがします。

-   *StartIo*ルーチンがシステム全体のスループットを削減し、チェーン内のすべての下位のドライバーのディスパッチ ルーチンは IRQL で実行されるため、ディスパッチ =\_レベル。

    標準のドライバーのルーチンを実行する Irql の詳細については、次を参照してください。[を管理するハードウェアの優先順位](managing-hardware-priorities.md)します。

どのシステム提供のより高度なドライバーがない、 *StartIo* IRP がドライバー自体に、上記のすべてのドライバーと、その下と、システム全体の処理が低下するため、ルーチン。

単に最も高度なドライバーは Irp を下位レベルのドライバーに、ディスパッチ ルーチンから送信し、必要なクリーンアップ処理を行う、 *IoCompletion*ルーチン。

ただしより高度なドライバーは、特定の種類、操作の要求または Irp の一連の SCSI ポート ドライバーなどの異種の基になるデバイスのバインドを保持するために内部キューを設定する Irp の内部キューを設定できます。 詳細については、次を参照してください。[キューおよびデキュー Irp](queuing-and-dequeuing-irps.md)します。

 

 





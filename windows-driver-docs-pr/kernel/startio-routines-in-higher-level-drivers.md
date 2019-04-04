---
title: 高度なドライバーの StartIo ルーチン
description: 高度なドライバーの StartIo ルーチン
ms.assetid: 8b0e3bef-4a73-4cf8-b71a-6aedf451d648
keywords:
- StartIo ルーチンより高度なドライバー
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c99d78155f63908c02cda53caa444f887170b535
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528294"
---
# <a name="startio-routines-in-higher-level-drivers"></a>高度なドライバーの StartIo ルーチン





高度なドライバーが持つことができます、 [ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858)ルーチン。 ただし、このようなドライバーを使用して、既存の下位レベルのドライバーと相互運用する可能性がありますすることがなく、特徴のパフォーマンスが低下する可能性があります。

A *StartIo*ドライバーでは上位レベルのルーチンに次の効果があります。

-   受信 Irp が呼び出すことによってキューに格納可能[ **IoStartPacket** ](https://msdn.microsoft.com/library/windows/hardware/ff550370)からドライバーの*ディスパッチ*Xxx routine(s) と[**います** ](https://msdn.microsoft.com/library/windows/hardware/ff550358)からその[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354) routine(s)、原因となり、ある Irp の処理を一度に 1 つずつ、 *StartIo*ルーチンです。

-   大量の I/O 要求の期間中に、ドライバーの I/O スループットが著しく遅くなる可能性がありますので、その*StartIo*ルーチンがボトルネックになることができます。

-   ドライバーの*StartIo*ルーチンの呼び出し[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336) IRQL で各 IRP = ディスパッチ\_レベル、それによってすべての下位のドライバーのディスパッチの原因IRQL で実行するためにもルーチン = ディスパッチ\_レベル。 これは、下位のドライバーがディスパッチ ルーチン内で呼び出すことができるサポート ルーチンのセットを制限します。 ほとんどのドライバー作成者には、そのドライバーのディスパッチ ルーチンの IRQL で実行が前提としていますので&lt;ディスパッチ\_レベルより高いレベルのドライバーは、多くの既存の下位のドライバーと相互運用する可能性がありますがします。

-   *StartIo*ルーチンがシステム全体のスループットを削減し、チェーン内のすべての下位のドライバーのディスパッチ ルーチンは IRQL で実行されるため、ディスパッチ =\_レベル。

    標準のドライバーのルーチンを実行する Irql の詳細については、[を管理するハードウェアの優先順位](managing-hardware-priorities.md)を参照してください。

どのシステム提供のより高度なドライバーがない、 *StartIo* IRP がドライバー自体に、上記のすべてのドライバーと、その下と、システム全体の処理が低下するため、ルーチン。

単に最も高度なドライバーは Irp を下位レベルのドライバーに、ディスパッチ ルーチンから送信し、必要なクリーンアップ処理を行う、 *IoCompletion*ルーチン。

ただしより高度なドライバーは、特定の種類、操作の要求または Irp の一連の SCSI ポート ドライバーなどの異種の基になるデバイスのバインドを保持するために内部キューを設定する Irp の内部キューを設定できます。 詳細については、[キューおよびデキュー Irp](queuing-and-dequeuing-irps.md)を参照してください。

 

 





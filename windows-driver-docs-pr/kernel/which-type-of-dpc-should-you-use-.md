---
title: DPC の種類を使用する必要があります。
description: DPC の種類を使用する必要があります。
ms.assetid: 7a8e6d75-5573-4a94-a895-fa2f70856807
keywords:
- 遅延プロシージャ呼び出しの WDK カーネル
- Dpc WDK カーネル
- DpcForIsr
- CustomDpc
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b1f461e16c0507eb33d83524342bc3132aafb22
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338432"
---
# <a name="which-type-of-dpc-should-you-use"></a>使用すべき DPC の種類





ドライバーの設計によって、次のことができます。

-   1 つ[ *DpcForIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff544079)割り込み駆動のすべての I/O 操作を完了するには

-   1 つまたは複数のセット[ *CustomDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542972)ルーチン。

-   両方を*DpcForIsr*と一連の操作に固有の*CustomDpc*ルーチン

ドライバーが 1 つを持つかどうか*DpcForIsr*ルーチン、一連の*CustomDpc*ルーチン、またはその両方が、基になるデバイスの性質に依存し、一連の I/O 要求がサポートする必要がある必要があります。

ほとんどの最下位レベルのデバイス ドライバーがある、1 つ*DpcForIsr*ルーチンを I/O がそれぞれのデバイスで 1 つまたは複数の操作を必要とする各 IRP の処理を完了します。 1 つを使用して*DpcForIsr*要求を完了するは一度に 1 つの操作をデバイス上の I/O 操作の割り込み駆動は比較的簡単です。 このようなドライバーの ISR を呼び出すだけ[ **IoRequestDpc** ](https://msdn.microsoft.com/library/windows/hardware/ff549657)割り込み駆動の I/O 操作ごとにします。

最下位レベルのいくつかのドライバーが*CustomDpc*ルーチンがデバイスの I/O 操作の割り込み駆動の多様なセットを完了する 1 つ以上の DPC を必要としない限り、します。

1 つを使用して*DpcForIsr*同時操作を実行できるデバイスでの操作、割り込み駆動のオーバー ラップ I/O の完了を慎重に設計でできることが比較的難しいことができます。 他に、またはキューではなく、 *DpcForIsr*、ドライバーによって提供される、操作に固有の一連のキューに配置できます ISR *CustomDpc*ルーチンを呼び出すことによって[ **KeInsertQueueDpc**](https://msdn.microsoft.com/library/windows/hardware/ff552185).

たとえば、デザインの課題のいくつかシリアル ドライバーの記述に関連します。 全二重デバイスのドライバーとしてシリアル ドライバーは Irp をキューには、順序、一対一で対応に依存できない、 *StartIo*ルーチンとマルチタスクでそのデバイスからの割り込みのシーケンスマルチプロセッサ システムです。 さらに、シリアル ドライバーは、バッファー内のデータを削除するには、要求と、以前要求した操作をキャンセルする非同期のユーザーが生成した要求のタイムアウトを処理する必要がありますなどとします。

その結果、シリアル ドライバーは、読み取り用の内部キューの記述、消去、およびユーザー モードの COM ポートのアプリケーションが要求できる操作の待機を維持する可能性があります。 でした参照カウントを維持するか、または、内部キューに Irp の一連のフラグなどの他の追跡メカニズムを使用します。 その ISR を呼び出して**KeInsertQueueDpc**と複数のドライバーに割り当てられた、初期化の DPC オブジェクトのそれぞれに関連付けられているドライバーによって提供される*CustomDpc*ルーチン。

 

 





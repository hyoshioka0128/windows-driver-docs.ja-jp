---
title: 読み取り/書き込みディスパッチ ルーチンの概要
description: 読み取り/書き込みディスパッチ ルーチンの概要
ms.assetid: 2ab1cde7-89e8-449f-b2a0-12aa0762ebf3
keywords:
- DispatchRead ルーチン
- DispatchWrite ルーチン
- DispatchReadWrite ルーチン
- ディスパッチルーチン WDK カーネル、DispatchReadWrite ルーチン
- ディスパッチルーチン WDK カーネル、DispatchWrite ルーチン
- ディスパッチルーチン WDK カーネル、DispatchRead ルーチン
- 読み取り/書き込みディスパッチルーチン WDK カーネル
- IRP_MJ_WRITE i/o 関数コード
- IRP_MJ_READ i/o 関数コード
- データ転送 WDK カーネル、読み取り/書き込みディスパッチルーチン
- データの転送 WDK カーネル、読み取り/書き込みディスパッチルーチン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 087db34294c7d5c9047af976da4af2ac0979cfec
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838401"
---
# <a name="summary-of-readwrite-dispatch-routines"></a>読み取り/書き込みディスパッチ ルーチンの概要





[*DispatchRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)、 [*DispatchWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)、または[*DispatchReadWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンを実装する場合は、次の点に注意してください。

-   複数の階層化されたドライバーのチェーンにおいて、IRP で次に下位レベルのドライバーの i/o スタックの場所を設定する前に、受信した読み取り/書き込み Irp のパラメーターを確認して有効性を確認する必要があります。

-   一般に、中間レベルと最下位レベルのドライバーは、チェーン内の最上位レベルのドライバーに依存して、有効なパラメーターで転送要求を渡すことができます。 ただし、すべてのドライバーは、IRP の i/o スタックの場所にあるパラメーターに対して正常性チェックを実行できます。また、各デバイスドライバーは、デバイスによって設定された制限に違反する可能性がある条件のパラメーターをチェックする必要があります。

-   *DispatchReadWrite*ルーチンがエラーで IRP を完了した場合、i/o スタックの場所の**状態**のメンバーに適切な NTSTATUS の種類の値を設定し、**情報**メンバーを0に設定し、を使用して[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出す必要があります。IO\_の IRP と優先*順位の上昇*は\_インクリメントされません。

-   ドライバーがバッファーされた i/o を使用する場合、転送するデータを格納する構造体を定義することが必要になる場合があります。また、これらの構造体の数を内部でバッファーする必要がある場合もあります。

-   ドライバーが直接 i/o を使用する場合、基になるデバイスが1回の転送操作で処理するのに必要なデータが多すぎる (または、改ページが多すぎる) バッファーに記述さ **&gt;** れているかどうかを確認する必要がある場合があります。 その場合、ドライバーは元の転送要求を、より小さな転送操作のシーケンスに分割する必要があります。

    密接に結合されたクラスドライバーは、基になるポートドライバーの*DispatchReadWrite*ルーチンでこのような要求を分割することがあります。 これを行うには、SCSI クラスドライバー (特に大容量記憶装置用) が必要です。 SCSI ドライバーの要件の詳細については、「[記憶装置ドライバー](https://docs.microsoft.com/windows-hardware/drivers/storage/storage-drivers)」を参照してください。

-   低レベルのデバイスドライバーの*DispatchReadWrite*ルーチンでは、別のドライバールーチンによって、転送用にデバイスを設定するように IRP がデキューされるまで、大規模な転送要求を部分的な転送に分割する必要があります。

-   下位レベルのデバイスドライバーが、独自のルーチンによってさらに処理するために読み取り/書き込みの IRP をキューに置いている場合、IRP をキューに追加する前に[**Iomarkirppending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)を呼び出す必要があります。 また、このような状況では、 *DispatchReadWrite*ルーチンは状態\_保留中のコントロールを返す必要があります。

-   *DispatchReadWrite*ルーチンが irp を下位のドライバーに渡す場合、irp 内の次に小さいドライバーの i/o スタックの場所を設定する必要があります。 上位レベルのドライバーも、 [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)で渡す前に IRP で[*iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを設定するかどうかは、ドライバーの設計とその下にあるレイヤーの設計によって異なります。

    ただし、より高いレベルのドライバーは、Irp やメモリなどのリソースを割り当てる場合は、 [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出す前に[**Ioset補完ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)を呼び出す必要があります。 低レベルのドライバーが要求を完了した後、 *Iocompletion*ルーチンが元の IRP で[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出す前に、その*iocompletion*ルーチンは、ドライバーで割り当てられたリソースを解放する必要があります。

-   上位レベルのドライバーが、基になるリムーバブルメディアデバイスドライバーを含む可能性のある下位のドライバーに対して Irp を割り当てる場合、割り当てドライバーは、割り当てられる各 IRP でスレッドコンテキストを確立する必要があります。

 

 





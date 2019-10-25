---
title: 上位レベル ドライバーの DispatchReadWrite
description: 上位レベル ドライバーの DispatchReadWrite
ms.assetid: d8406115-c62e-4362-8d2c-77d0414c4104
keywords:
- DispatchReadWrite ルーチン
- ディスパッチルーチン WDK カーネル、DispatchReadWrite ルーチン
- 読み取り/書き込みディスパッチルーチン WDK カーネル
- IRP_MJ_WRITE i/o 関数コード
- IRP_MJ_READ i/o 関数コード
- データ転送 WDK カーネル、読み取り/書き込みディスパッチルーチン
- データの転送 WDK カーネル、読み取り/書き込みディスパッチルーチン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ddfd2831410c51da04126f6b91fbd050367ade98
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836839"
---
# <a name="dispatchreadwrite-in-higher-level-drivers"></a>上位レベル ドライバーの DispatchReadWrite





ファイルシステムドライバーを除き、上位レベルのドライバーは、通常、Irp の内部ドライバーキューを持っていません。 このようなドライバーの[*DispatchReadWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンでは、有効なパラメーターを持つ irp を下位のドライバーに渡すことができます。これは、「 [Irp をドライバースタックに渡す](passing-irps-down-the-driver-stack.md)」で説明されているように、 [*iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを設定した後に行うことができます。

ただし、SCSI クラスドライバーの*DispatchReadWrite*ルーチンは、必要に応じて大規模な転送要求を分割してから、主要な関数コード[**irp\_MJ\_READ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)または[**IRP\_MJ\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write) SCSI ポート/ミニポートドライバーのペアに書き込みます。 詳細については、「[ストレージクラスドライバーの SplitTransferRequest ルーチン](https://docs.microsoft.com/windows-hardware/drivers/storage/storage-class-driver-s-splittransferrequest-routine)」を参照してください。

上位レベルのドライバーによって1つ以上の Irp が割り当てられている場合は、 *DispatchReadWrite*ルーチン内の次の下位のドライバーに対して設定されます。一部の部分転送を要求するには、 *DispatchReadWrite*ルーチンでを呼び出す[**必要があります。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)各ドライバーが割り当てられた IRP を使用した Ioset補完ルーチン。 ドライバーは、各部分転送操作で転送されるデータの量を追跡するために*iocompletion*ルーチンを登録して、 *iocompletion*ルーチンがドライバーによって割り当てられたすべての irp を解放し、最終的に元の要求を完了できるようにする必要があります.

基になるドライバーがリムーバブルメディアデバイスを制御する場合は、上位レベルのドライバーによって割り当てられる Irp にスレッドコンテキストが必要です。 スレッドコンテキストを設定するには、割り当てドライバーが**Irp&gt;テール**を設定する必要があります。着信転送 IRP の同じ値から、新しく割り当てられた各 IRP 内のスレッド。 詳細については、「[リムーバブルメディアのサポート](supporting-removable-media.md)」を参照してください。

基になるデバイスドライバーが、エラーが発生した部分的な転送に対して IRP を返した場合、 *Iocompletion*ルーチンは、部分転送要求を再試行するか、返されたエラーと共に、その i/o 状態ブロックを使用して元の irp を完了することができます。高レベルのドライバーによって割り当てられた Irp とメモリ。

上位レベルのドライバーの*DispatchReadWrite*ルーチンが部分転送操作にメモリを割り当て、その割り当てがドライバーの*iocompletion*ルーチン (または基になるデバイスドライバー)*によってアクセスされる場合、DispatchReadWrite*ルーチンは、非ページプールからそのメモリを割り当てる必要があります。

 

 





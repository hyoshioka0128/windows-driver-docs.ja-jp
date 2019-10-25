---
title: DispatchCleanup ルーチン
description: DispatchCleanup ルーチン
ms.assetid: 1ba001b8-92e0-453f-b9f6-6099cedf6439
keywords:
- ディスパッチルーチン WDK カーネル、DispatchCleanup ルーチン
- DispatchCleanup ルーチン
- IRP_MJ_CLEANUP i/o 関数のコード
- リソースの割り当ての解除 (WDK カーネル)
- ハードウェアメモリのマッピング解除
- ユーザーモードメモリのマッピング解除
- ユーザーモードメモリのロック解除
- リソースのクリーンアップ WDK カーネル
- スピンロック WDK カーネル
- クリーンアップディスパッチルーチン WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8217625e32b3d0b19fcd3a7ffe3c243df5b7492
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836893"
---
# <a name="dispatchcleanup-routines"></a>DispatchCleanup ルーチン





ドライバーの[*DispatchCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンは、 [**irp\_MJ\_クリーンアップ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-cleanup)I/o 関数コードの irp を処理します。

ドライバーは、 *DispatchCleanup*ルーチンを使用して、ファイルオブジェクトへのすべてのハンドルが閉じられた後に必要なクリーンアップ操作を実行できます。 *DispatchCleanup*は、最後のハンドルを閉じたプロセスのプロセスコンテキストで呼び出されることに注意してください。このプロセスは、最初にハンドルを開いたプロセスとは異なる場合があります。 (通常、この違いが発生するのは、別のプロセスで**DuplicateHandle**ユーザーモードルーチンを使用してプロセスハンドルが複製されるためです)。元のプロセスコンテキストでクリーンアップを実行する必要があるドライバーは、 [**Pssetcreateprocessnotifyroutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-pssetcreateprocessnotifyroutine)ルーチンを使用してその目的のコールバックルーチンを登録できますが、このようなコールバックはシステムリソースが限られていることに注意してください。

一般に、 *DispatchCleanup*ルーチンでは、ターゲットデバイスオブジェクトのデバイスキュー (またはドライバーの内部キュー内) にあるすべての irp に対して次の操作を実行することで、 **irp\_MJ\_クリーンアップ**要求を処理する必要があります。およびは、ファイルオブジェクトに関連付けられています。

-   [**Iosetcancelroutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcancelroutine)を呼び出して、[*キャンセル*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)ルーチンポインターを**NULL**に設定します。

-   キューに置かれている IRP の i/o スタックの場所に指定されているファイルオブジェクトが、Irp\_MJ の i/o スタックの場所で受信したファイルオブジェクトと一致する場合、ターゲットデバイスオブジェクトのキューにあるすべての IRP をキャンセルし **\_クリーンアップ**要求です。

-   [**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出して IRP を完了し、STATUS\_SUCCESS を返します。

**Irp\_MJ\_クリーンアップ**要求の処理中に、ドライバーは、 [**irp\_MJ\_READ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)または[**irp\_MJ\_WRITE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)などの追加の要求を受け取ることができます。 そのため、リソースの割り当てを解除する必要があるドライバーでは、 *DispatchCleanup*ルーチンの実行を、 [*DispatchRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)や[*DispatchWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)などの他のディスパッチルーチンと同期させる必要があります。

 

 





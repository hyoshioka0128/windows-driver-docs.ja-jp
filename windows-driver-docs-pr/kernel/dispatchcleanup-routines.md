---
title: DispatchCleanup ルーチン
description: DispatchCleanup ルーチン
ms.assetid: 1ba001b8-92e0-453f-b9f6-6099cedf6439
keywords:
- ディスパッチ ルーチンの WDK カーネル、DispatchCleanup ルーチン
- DispatchCleanup ルーチン
- IRP_MJ_CLEANUP I/O 関数のコード
- WDK カーネルのリソースの割り当てを解除
- ハードウェア メモリをマップ解除しています
- ユーザー モード メモリにマップ解除しています
- ユーザー モード メモリにロック解除
- WDK カーネルのリソースのクリーンアップ
- スピン ロック WDK カーネル
- クリーンアップ ディスパッチ ルーチン WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f49d8ad0a9e60e5a551bc1f619ece598cb0ec86d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381733"
---
# <a name="dispatchcleanup-routines"></a>DispatchCleanup ルーチン





ドライバーの[ *DispatchCleanup* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンの Irp の処理、 [ **IRP\_MJ\_クリーンアップ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-cleanup) I/O関数のコードです。

ドライバーを使用できる、 *DispatchCleanup*ルーチンが必要なすべてファイル オブジェクトへのハンドルの閉じられている任意のクリーンアップ操作を実行します。 なお*DispatchCleanup*プロセスのプロセスのコンテキストで呼び出される最後のハンドルを終了する。 このプロセスは、最初に、ハンドルを開いたプロセスから異なる可能性があります。 (別のプロセスを使用するため、この違いが通常発生、 **DuplicateHandle**プロセス ハンドルを複製するルーチンをユーザー モードです)。元のプロセスのコンテキストでクリーンアップを実行する必要がありますドライバーを使用できます、 [ **PsSetCreateProcessNotifyRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-pssetcreateprocessnotifyroutine)コールバック ルーチンを登録するため、このようなことに注意してください確保するためのルーチンコールバックは、限られたシステム リソースです。

一般に、 *DispatchCleanup*ルーチンを処理する必要があります、 **IRP\_MJ\_クリーンアップ**デバイスのキューにあるすべての IRP の次の手順に従って要求 (または、ドライバーの内部キュー Irp の)、対象のデバイス オブジェクトのファイル オブジェクトに関連付けられたとします。

-   呼び出す[ **IoSetCancelRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcancelroutine)を設定する、 [*キャンセル*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel)へのポインターを日常的な**NULL**します。

-   キューに置かれた IRP のドライバーの I/O スタックの場所で指定されたファイル オブジェクトの I/O スタックの場所で受信したファイルのオブジェクトに一致する場合、対象のデバイス オブジェクトのキューになっているすべての IRP をキャンセル、 **IRP\_MJ\_クリーンアップ**要求。

-   呼び出す[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest) 、IRP の完了を状態を返す\_成功します。

処理中に、 **IRP\_MJ\_クリーンアップ**要求と、ドライバーはなど、追加の要求を受信できる[ **IRP\_MJ\_読み取り**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)または[ **IRP\_MJ\_書き込み**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)します。 そのため、リソースの割り当てを解除する必要がありますドライバーでする必要がありますの実行を同期もその*DispatchCleanup*他のルーチンがなどのルーチンをディスパッチ[ *DispatchRead* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)と[ *DispatchWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)します。

 

 





---
title: 完了処理の実行方法
description: 完了処理の実行方法
ms.assetid: 5741c226-9781-4d9a-b6dd-d8ecc17c4c6f
keywords:
- IRP 完了ルーチン WDK ファイルシステム、処理ステージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fcc3d6956d5ea16df7e7bd38dbcf9b8aa19134c9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841220"
---
# <a name="how-completion-processing-is-performed"></a>完了処理の実行方法


## <span id="ddk_how_completion_processing_is_performed_if"></span><span id="DDK_HOW_COMPLETION_PROCESSING_IS_PERFORMED_IF"></span>


完了処理は2段階で実行されます。 最初の段階は、IRQL &lt;= ディスパッチ\_レベルで、任意のスレッドコンテキストで実行されます。 この段階では、次のタスクが実行されます。

-   IRP に登録されている各完了ルーチンは、最も低い IRP スタックの場所から順に呼び出されます。 完了ルーチンが、必要な\_処理\_より多くの状態\_返す場合、完了処理は停止されます。

-   IRP にメモリ記述子リスト (MDL) が含まれている場合、MDL によってマップされた物理ページのロックは解除されます。

-   I/o 完了の2番目のフェーズは、特別なカーネル APC としてターゲット (要求) スレッドのキューに登録されます。

2番目の段階は、i/o 要求を発信したスレッドのコンテキストで実行されます。 これは特殊なカーネル APC として実行されるため、IRQL APC\_レベルで実行されます。 この段階では、次のタスクが実行されます。

-   IRP がバッファリングされた操作を表す場合、 **irp&gt;の AssociatedIrp**の内容が**UserBuffer&gt;** にコピーされます。

-   IRP に MDL が含まれている場合、MDL は解放されます。

-   I/o 要求の発信者が操作の最終状態を確認できるように、 **irp&gt;IoStatus**の内容が**irp&gt;UserIosb**にコピーされます。

-   イベントが**Irp&gt;UserEvent**に指定されている場合は、シグナルが通知されます。 それ以外の場合、この IRP 用のファイルオブジェクトがある場合、そのイベントはシグナル状態になります。

-   [**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)または[**IoBuildSynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildsynchronousfsdrequest)を呼び出すことによって IRP が作成された場合は、スレッドの保留中の i/o 要求一覧からデキューされます。

-   呼び出し元が要求した場合、ユーザー APC がキューに登録されます。

-   IRP は解放されます。

完了ルーチンが\_処理\_必要な\_の状態を返すために、IRP の完了処理が停止した**場合  、** 同じ Irp で[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出すことによって再開できます。 この場合、最初の段階の処理が再開されます。その後、完了ルーチンがステータスを返したドライバーのすぐ上にあるドライバーの完了ルーチンから、\_処理\_必要な\_が増えます。

 

 

 





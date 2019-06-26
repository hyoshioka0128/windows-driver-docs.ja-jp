---
title: 完了処理の実行方法
description: 完了処理の実行方法
ms.assetid: 5741c226-9781-4d9a-b6dd-d8ecc17c4c6f
keywords:
- IRP の完了ルーチン WDK ファイル システム、処理ステージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e47fa85f64171274e1f63f98c5ebc90e7a62bfbd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365864"
---
# <a name="how-completion-processing-is-performed"></a>完了処理の実行方法


## <span id="ddk_how_completion_processing_is_performed_if"></span><span id="DDK_HOW_COMPLETION_PROCESSING_IS_PERFORMED_IF"></span>


終了処理は、2 つの段階で実行されます。 最初のステージは、IRQL で、任意のスレッド コンテキストで実行&lt;= ディスパッチ\_レベル。 この段階で、次のタスクが実行されます。

-   IRP が登録されている各完了ルーチンは、以降、最下位の IRP スタックの場所でさらに、呼び出されます。 完了ルーチンの状態を返す場合\_詳細\_処理\_必要に応じて、完了処理が停止します。

-   IRP にメモリ記述子のリスト (MDL) が含まれている場合、MDL によってマップされる任意の物理ページはロックされていません。

-   I/O 完了の 2 番目のフェーズは、特別なカーネル APC として (要求) のターゲット スレッドにキューに配置します。

2 番目の段階は、I/O 要求を生成したスレッドのコンテキストで実行されます。 これは特別なカーネル APC として実行され、IRQL APC で実行されるため\_レベル。 この段階で、次のタスクが実行されます。

-   IRP がバッファー内の操作の内容を表すかどうか**Irp -&gt;AssociatedIrp.SystemBuffer**にコピーされます**Irp -&gt;UserBuffer**します。

-   IRP に MDL が含まれている場合、MDL は解放されます。

-   内容**Irp -&gt;IoStatus**にコピーされます**Irp -&gt;UserIosb** I/O 要求の発信元は、操作の最終的な状態を確認できるようにします。

-   イベントがで指定されている場合**Irp の&gt;UserEvent**、シグナル状態になることができます。 それ以外の場合、この IRP のファイル オブジェクトがある場合は、そのイベントがシグナル状態します。

-   IRP が呼び出すことによって作成された場合[ **IoBuildDeviceIoControlRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuilddeviceiocontrolrequest)または[ **IoBuildSynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildsynchronousfsdrequest)、キューから取り出さスレッドの保留中 I/O 要求の一覧。

-   ユーザー APC がキューに 1 つ、呼び出し元が要求された場合。

-   IRP が解放されます。

**注**  完了ルーチンに状態が返されたため完了 IRP の処理は停止\_詳細\_処理\_必要に応じて、再開できるように呼び出すことによって[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest) IRP が同じにします。 最初の段階の処理が再開には、状態が返されましたが完了ルーチンを 1 つのすぐ上のドライバーの完了のルーチンで始まるこのような場合は、\_詳細\_処理\_必要な作業です。

 

 

 





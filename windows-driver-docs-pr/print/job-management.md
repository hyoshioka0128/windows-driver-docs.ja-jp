---
title: ジョブ管理
description: ジョブ管理機能は Windows 8.1 以降のバージョンの Windows で導入され、ジョブキューのライブビューを提供します。
ms.assetid: D1236DD2-D4AD-4615-9036-7EC75D6CADCE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a6454173b26d3dc55480663a5c0df899778d93b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843257"
---
# <a name="job-management"></a>ジョブ管理


ジョブ管理機能は Windows 8.1 以降のバージョンの Windows で導入され、ジョブキューのライブビューを提供します。

この機能を使用すると、クライアントは印刷ジョブをキャンセルすることもできます。 クライアントは、UWP デバイスアプリ内またはプリンター拡張機能から、適切なプログラミングインターフェイスを呼び出すことができます。

## <a name="the-new-interfaces"></a>新しいインターフェイス


次のインターフェイスは、ジョブ管理機能を実装するために Windows 8.1 で導入されました。

[**IPrinterQueue2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterqueue2)

[**Iプリンターキュービュー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterqueueview)

[**IPrinterQueueViewEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterqueueviewevent)

[**IPrintJob**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintjob)

[**IPrintJobCollection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintjobcollection)

## <a name="initiating-a-job-management-session"></a>ジョブ管理セッションを開始しています


ジョブ管理セッションを開始するには、まず、管理するジョブの範囲を指定して要求する必要があります。 このような種類のジョブは "ビュー" と呼ばれ、 [**IPrinterQueue2:: Getプリンター Queueview**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nf-printerextension-iprinterqueue2-getprinterqueueview)メソッドを使用して指定します。

別のジョブセットを監視するようにビューを変更する場合は、 [**Iプリンター queueview:: Set閲覧 wrの**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nf-printerextension-iprinterqueueview-setviewrange)メソッドを使用します。

印刷キューは動的キューであることに注意してください。 したがって、印刷キューの状態が変わるたびにイベントが発生し、 [**IPrinterQueueViewEvent:: OnChanged**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nf-printerextension-iprinterqueueviewevent-onchanged)メソッドによって、要求されたビューの更新されたスナップショットが提供されます。

次C#のコードスニペットは、ジョブ管理セッションを開始するための新しいインターフェイスの使用方法を示しています。

```csharp
void PerformJobManagement(IPrinterQueue2 queue)
{
    //
    // Create a printer queue view and specify the range of
    // print queue positions to be monitored
    //

    PrinterQueueView queueView = queue.GetPrinterQueueView(0, COUNT_JOBS_MONITORED);

    //
    // Add the event handler to the IPrinterQueueView object via the 
    // standard COM event model, the IConnectionPoint mechanism.
    //

    queueView.OnChanged += queueView_OnChanged;


    //
    // When a different range of print jobs needs to be monitored, 
    // reset/update the view.
    //

    queueView.SetViewRange(20, COUNT_JOBS_MONITORED);

}

//
// Create an event handler that is called when
// there is a change in the View
//
void queueView_OnChanged(
    IPrintJobCollection pcollection,
    uint ulviewOffset,
    uint ulviewSize,
    uint ulcountJobsInPrintQueue)
{
    foreach (IPrintJob job in pCollection)
    {
        UIDisplay(job.Name);
        UIDisplay(job.Id);
    }
}
```

UIDisplay は、ユーザーに情報を表示するために開発する機構の汎用名として使用されます。

また、ジョブの列挙は、最初のイベントハンドラーが追加されると開始され、最後のイベントハンドラーが削除されると停止します。

## <a name="related-topics"></a>関連トピック
[**IPrinterQueue2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterqueue2)  
[**Iプリンターキュービュー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterqueueview)  
[**IPrinterQueueViewEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterqueueviewevent)  
[**IPrintJob**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintjob)  
[**IPrintJobCollection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintjobcollection)  




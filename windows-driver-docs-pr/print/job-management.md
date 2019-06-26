---
title: ジョブ管理
description: ジョブ キューのライブ ビューを提供するには、Windows 8.1 および以降のバージョンの Windows で、ジョブの管理機能が導入されました。
ms.assetid: D1236DD2-D4AD-4615-9036-7EC75D6CADCE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17df3c678b8051b4eebbc3aafbf607f93522896c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377526"
---
# <a name="job-management"></a>ジョブ管理


ジョブ キューのライブ ビューを提供するには、Windows 8.1 および以降のバージョンの Windows で、ジョブの管理機能が導入されました。

この機能は、クライアントは印刷ジョブをキャンセルすることもできます。 クライアントは、適切なプログラミング インターフェイスから UWP デバイスのアプリ内、またはプリンターの拡張機能からを呼び出すことができます。

## <a name="the-new-interfaces"></a>新しいインターフェイス


次のインターフェイスが、ジョブの管理機能を実装するために Windows 8.1 で導入されました。

[**IPrinterQueue2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterqueue2)

[**IPrinterQueueView**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterqueueview)

[**IPrinterQueueViewEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterqueueviewevent)

[**IPrintJob**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprintjob)

[**IPrintJobCollection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprintjobcollection)

## <a name="initiating-a-job-management-session"></a>ジョブの管理セッションを開始します。


ジョブの管理セッションを開始するには、最初に指定し、管理するジョブの範囲を要求する必要があります。 このジョブの範囲は"view"と呼ばれ、使用する、 [ **IPrinterQueue2::GetPrinterQueueView** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nf-printerextension-iprinterqueue2-getprinterqueueview)メソッドを指定します。

さまざまな一連のジョブを監視するビューを変更する場合は、使用、 [ **IPrinterQueueView::SetViewRange** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nf-printerextension-iprinterqueueview-setviewrange)を実行するメソッド。

印刷キューは動的なキューであることに注意してください。 イベントが、毎回、印刷キューの変更の状態、および[ **IPrinterQueueViewEvent::OnChanged** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nf-printerextension-iprinterqueueviewevent-onchanged)メソッドが要求されたビューの更新されたスナップショットを提供します。

次C#コード スニペットは、ジョブの管理セッションを開始するため、新しいインターフェイスの使用方法を示します。

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

UIDisplay が使用される汎用的な名前のユーザーに情報を表示するためのメカニズムを開発します。

また、最初のイベント ハンドラーが追加され、最後のイベント ハンドラーが削除されたときに停止しているときにジョブの列挙が開始されるに注意してください。

## <a name="related-topics"></a>関連トピック
[**IPrinterQueue2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterqueue2)  
[**IPrinterQueueView**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterqueueview)  
[**IPrinterQueueViewEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterqueueviewevent)  
[**IPrintJob**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprintjob)  
[**IPrintJobCollection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprintjobcollection)  




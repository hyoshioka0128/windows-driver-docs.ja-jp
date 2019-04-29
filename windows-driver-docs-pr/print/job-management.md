---
title: ジョブ管理
description: ジョブ キューのライブ ビューを提供するには、Windows 8.1 および以降のバージョンの Windows で、ジョブの管理機能が導入されました。
ms.assetid: D1236DD2-D4AD-4615-9036-7EC75D6CADCE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6002e168002c41a4d67ff98b6ba96d3272ead709
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326026"
---
# <a name="job-management"></a>ジョブ管理


ジョブ キューのライブ ビューを提供するには、Windows 8.1 および以降のバージョンの Windows で、ジョブの管理機能が導入されました。

この機能は、クライアントは印刷ジョブをキャンセルすることもできます。 クライアントは、適切なプログラミング インターフェイスから UWP デバイスのアプリ内、またはプリンターの拡張機能からを呼び出すことができます。

## <a name="the-new-interfaces"></a>新しいインターフェイス


次のインターフェイスが、ジョブの管理機能を実装するために Windows 8.1 で導入されました。

[**IPrinterQueue2**](https://msdn.microsoft.com/library/windows/hardware/dn265389)

[**IPrinterQueueView**](https://msdn.microsoft.com/library/windows/hardware/dn265392)

[**IPrinterQueueViewEvent**](https://msdn.microsoft.com/library/windows/hardware/dn265393)

[**IPrintJob**](https://msdn.microsoft.com/library/windows/hardware/dn265396)

[**IPrintJobCollection**](https://msdn.microsoft.com/library/windows/hardware/dn265397)

## <a name="initiating-a-job-management-session"></a>ジョブの管理セッションを開始します。


ジョブの管理セッションを開始するには、最初に指定し、管理するジョブの範囲を要求する必要があります。 このジョブの範囲は"view"と呼ばれ、使用する、 [ **IPrinterQueue2::GetPrinterQueueView** ](https://msdn.microsoft.com/library/windows/hardware/dn265390)メソッドを指定します。

さまざまな一連のジョブを監視するビューを変更する場合は、使用、 [ **IPrinterQueueView::SetViewRange** ](https://msdn.microsoft.com/library/windows/hardware/dn265395)を実行するメソッド。

印刷キューは動的なキューであることに注意してください。 イベントが、毎回、印刷キューの変更の状態、および[ **IPrinterQueueViewEvent::OnChanged** ](https://msdn.microsoft.com/library/windows/hardware/dn265394)メソッドが要求されたビューの更新されたスナップショットを提供します。

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
[**IPrinterQueue2**](https://msdn.microsoft.com/library/windows/hardware/dn265389)  
[**IPrinterQueueView**](https://msdn.microsoft.com/library/windows/hardware/dn265392)  
[**IPrinterQueueViewEvent**](https://msdn.microsoft.com/library/windows/hardware/dn265393)  
[**IPrintJob**](https://msdn.microsoft.com/library/windows/hardware/dn265396)  
[**IPrintJobCollection**](https://msdn.microsoft.com/library/windows/hardware/dn265397)  




---
title: デバイス保守管理
description: デバイスメンテナンス機能は、Windows 8.1 以降のバージョンの Windows で導入されました。
ms.assetid: 310E92A9-F751-4346-9B2D-0578A136AD20
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 855404911961582b36e8dc8b47897917dccfea7b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828946"
---
# <a name="device-maintenance"></a>デバイス保守管理


デバイスメンテナンス機能は、Windows 8.1 以降のバージョンの Windows で導入されました。

この機能では双方向通信 (Bidi) を使用して、UWP デバイスアプリまたはプリンターの拡張機能から印刷サブシステムにデバイスのメンテナンスコマンドを送信できるようにします。 たとえば、印刷デバイスにコマンドを送信して、インクノズルをクリーニングすることができます。

ポートモニターは、ベンダーが提供する Bidi 拡張ファイルと連携して、これらの Bidi 要求をデバイスおよびプロトコル固有のコマンドに変換し、それを印刷デバイスに送信します。 デバイスメンテナンスタスクは、Bidi "Set" クエリを印刷デバイスに送信することによって実行され、デバイスからの Bidi 応答は、操作が成功したか失敗したかを示します。

この機能を実装するために役立つ新しい非同期インターフェイスは、文字列パラメーターとコールバックオブジェクトの形式で XML データを受け取ります。

インターフェイスは非同期であるため、呼び出し元は応答を待つ必要はありません。 Bidi 操作が完了すると、コールバックオブジェクトが呼び出されます。

## <a name="the-new-interfaces"></a>新しいインターフェイス


デバイスメンテナンス機能を実装するために、Windows では次のインターフェイスが導入されています (コードネーム "Blue")。

[**Iプリンター Bidisetrequestcallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterbidisetrequestcallback)

[**IPrinterExtensionAsyncOperation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterextensionasyncoperation)

[**IPrinterQueue2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterqueue2)

## <a name="initiating-a-device-maintenance-session"></a>デバイスメンテナンスセッションを開始しています


デバイスメンテナンスセッションを開始するには、最初にコマンド文字列を XML データとして作成する必要があります。 次に、非同期 Bidi 操作の完了後に呼び出されるコールバックオブジェクトのインスタンスを作成する必要があります。

操作が完了すると、コールバックオブジェクトは Iプリンター Bidisetrequestcallback:: Completed メソッドで呼び出され、操作の HRESULT 値を提供します。 その後、この HRESULT 値を解析して、その他の必要なタスクを実行できます。

次のC#スニペットは、UWP デバイスアプリからデバイスメンテナンスタスクを発行する方法を示しています。

```csharp
//
// Declare a global constant that will be used
// to determine whether method calls were successful
//
const int S_OK = 0;
 
class BidiSendAsyncDemo
{
    //
    // Create a queue object and also
    // create the command string
    //
    void PerformDeviceMaintenance(
        IPrinterQueue2 queue,
        string bidiRequestInXml
        )
    {
        BidiSetResultCallback callBack = new BidiSetResultCallback();

        IPrinterExtensionAsyncOperation asyncOperation =
          queue.SendBidiSetRequestAsync(bidiRequestInXml, callBack);
    }
}

/// <summary>
/// This class represents the callback object
/// </summary>
public class BidiSetResultCallback :
    IPrinterBidiSetRequestCallback
{
    void Completed(
        string bidiResponse,
        int hr
        )
    {
        if (S_OK == hr)
        {
            // parse and interpret 'bidiResponse'
        }
    }
} 
```

デバイスのメンテナンスは、3つのエントリポイントのいずれかを使用してアプリが呼び出された後に UWP デバイスアプリでサポートされます。

## <a name="related-topics"></a>関連トピック
[**Iプリンター Bidisetrequestcallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterbidisetrequestcallback)  
[**IPrinterExtensionAsyncOperation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterextensionasyncoperation)  
[**IPrinterQueue2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterqueue2)  




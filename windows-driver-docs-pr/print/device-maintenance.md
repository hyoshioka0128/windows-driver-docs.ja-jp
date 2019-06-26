---
title: デバイス保守管理
description: デバイスのメンテナンス機能が Windows 8.1 と Windows の以降のバージョンで導入されました。
ms.assetid: 310E92A9-F751-4346-9B2D-0578A136AD20
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 160b9546c117f84d1a4726f8546c89617e426d6e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354925"
---
# <a name="device-maintenance"></a>デバイス保守管理


デバイスのメンテナンス機能が Windows 8.1 と Windows の以降のバージョンで導入されました。

この機能は、UWP デバイスのアプリまたは印刷サブシステムにプリンターの拡張機能内からデバイスのメンテナンス コマンドを送信できるように双方向通信 (Bidi) を使用します。 たとえば、インク ノズルをクリーニングする印刷デバイスにコマンドを送信する可能性があります。

これらの双方向の要求をデバイスとプロトコルに固有のコマンドに変換し、印刷デバイスに送信するベンダーが提供 Bidi 拡張ファイルと連携しますポート モニター。 デバイスのメンテナンス タスクは、印刷デバイスに Bidi"Set"クエリを送信することによって実行され、デバイスからの応答を双方向は、操作が成功したか、失敗したかどうかを示します。

この機能を実装するために役立つ新しい非同期インターフェイスは、文字列パラメーターと、コールバック オブジェクトの形式で XML データを取得します。

インターフェイスは非同期であるため、呼び出し元が応答を待機する必要はありません。 双方向の操作が完了したら、コールバック オブジェクトが呼び出されます。

## <a name="the-new-interfaces"></a>新しいインターフェイス


デバイスのメンテナンス機能を実装するために Windows (コード ネームは"Blue") で、次のインターフェイスが導入されました。

[**IPrinterBidiSetRequestCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterbidisetrequestcallback)

[**IPrinterExtensionAsyncOperation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterextensionasyncoperation)

[**IPrinterQueue2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterqueue2)

## <a name="initiating-a-device-maintenance-session"></a>デバイスのメンテナンス セッションを開始します。


デバイスのメンテナンス セッションを開始するには、まず XML データとして、コマンド文字列を作成する必要があります。 非同期の双方向の操作が完了した後に呼び出されるコールバック オブジェクトのインスタンスを作成する必要があります。

操作が完了した後は、コールバック オブジェクトが IPrinterBidiSetRequestCallback::Completed メソッドで呼び出され、操作の HRESULT 値を提供します。 この HRESULT 値を解析し、その他の必要なタスクを実行します。

次C#スニペットが UWP デバイス アプリからデバイスのメンテナンス タスクを発行する方法について説明します。

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

デバイスのメンテナンスは、次の 3 つのエントリ ポイントのいずれかを使用して、アプリが呼び出された後に、UWP デバイス アプリでサポートされます。

## <a name="related-topics"></a>関連トピック
[**IPrinterBidiSetRequestCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterbidisetrequestcallback)  
[**IPrinterExtensionAsyncOperation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterextensionasyncoperation)  
[**IPrinterQueue2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterqueue2)  




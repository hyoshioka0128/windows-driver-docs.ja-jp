---
title: 印刷フィルターで非同期通知
description: 印刷フィルターで非同期通知
ms.assetid: 52b0790b-4927-4e1b-8ae5-6e2afc7c9df6
keywords:
- モジュール WDK XPSDrv、XPS フィルターを表示します。
- XPS は、WDK XPSDrv をフィルター処理します。
- WDK XPS をフィルター処理します。
- 非同期通知 WDK XPS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 795bdb45d55077d12eedca434223f5cce34c8812
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550416"
---
# <a name="asynchronous-notifications-in-print-filters"></a>印刷フィルターで非同期通知


印刷フィルター パイプラインでは、アプリケーション用の印刷スプーラーでサポートされている非同期の通知に非常に類似した非同期の通知機能があります。 [ **RouterCreatePrintAsyncNotificationChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff562009)印刷スプーラで使用できる関数が印刷フィルターをご利用いただけません。 印刷のフィルターを使用する必要があります、 [IPrintClassObjectFactory](https://msdn.microsoft.com/library/windows/hardware/ff551955) IPrintAsyncNotify オブジェクトを作成するインターフェイス。

このトピックでは、印刷フィルターで非同期通知機能を使用する方法について説明します。

**注**  v4 印刷ドライバー モデルの印刷フィルターから非同期の通知をスローすることはサポートされていません。

 

### <a name="iprintclassobjectfactory"></a>IPrintClassObjectFactory

[IPrintClassObjectFactory](https://msdn.microsoft.com/library/windows/hardware/ff551955)インターフェイス通知インターフェイスへのアクセスを提供します。 次のコード例では、フィルターがプロパティ バッグからこのインターフェイスを取得する方法を示しています。

```cpp
// This interface is defined as a private member variable in the filter class
IPrintClassObjectFactory  *m_pPrintClassFactory;

// The following code goes in the IntializeFilter method of the filter
VARIANT var;
VariantInit(&var);

HRESULT hr = pIPropertyBag->GetProperty(
    XPS_FP_PRINT_CLASS_FACTORY, 
    &var);

if (SUCCEEDED(hr))
{
    hr = V_UNKNOWN(&var)->QueryInterface(
 IID_IPrintClassObjectFactory,
 reinterpret_cast<void **>(&m_pPrintClassFactory));
}
```

### <a name="notification-channel"></a>通知チャンネル

IPrintClassObjectFactory インターフェイスで、フィルターは、一方向またはフィルターのニーズに応じて、双方向の通知チャネルを作成できます。 次のコード例では、前の例から続行し、フィルターが一方向の通知チャネルを確立する方法を示しています。

```cpp
// Create a unidirectional notification channel
IPrintAsyncNotifyChannel  *pIAsyncNotifyChannel;
IPrintAsyncNotify  *pIAsyncNotify;

HRESULT hr = m_pPrintClassFactory->GetPrintClassObject(
 m_bstrPrinter,      // The printer name that was read from the property bag
 IID_IPrintAsyncNotify,
 reinterpret_cast<void**>(&pIAsyncNotify)));

if (SUCCEEDED(hr))
{
    hr = pIAsyncNotify->CreatePrintAsyncNotifyChannel(
 m_jobId,
 const_cast<GUID*>(&MS_ASYNCNOTIFY_UI),
 kPerUser,
 kUniDirectional,
        NULL,
        &pIAsyncNotifyChannel));

   // Etc.
}
```

双方向の通知チャネルを作成するには、前の例の代わりに次のコード例を使用します。

```cpp
// Create a bidirectional notification channel
IPrintAsyncNotifyChannel *pIAsyncNotifyChannel;
IPrintAsyncNotify *pIAsyncNotify;

HRESULT hr = m_pPrintClassFactory->GetPrintClassObject(
 m_bstrPrinterName,   // The printer name that was read from the property bag
 IID_IPrintAsyncNotify,
 reinterpret_cast<void**>(&pIAsyncNotify)));

if (SUCCEEDED(hr))
{
    hr = pIAsyncNotify->CreatePrintAsyncNotifyChannel(
 m_jobId,
 const_cast<GUID*>(& SAMPLE_ASYNCNOTIFY_UI),
 kPerUser,
 kBiDirectional,
 pIAsyncCallback,
        &pIAsyncNotifyChannel));

    // Etc.
}
```

変数、上記のコード例では`pIAsyncCallback`の呼び出し元の実装へのポインター、 [IPrintAsyncNotifyCallback](https://go.microsoft.com/fwlink/p/?linkid=124755)インターフェイス。

場合によってとそれが済んだら、双方向の通知チャネルをリリースする必要があります。 これを行うには、呼び出し、[リリース](https://go.microsoft.com/fwlink/p/?linkid=98433)メソッド[IPrintAsyncNotifyChannel](https://go.microsoft.com/fwlink/p/?linkid=124758)します。 チャネルを解放する場合については、[通知チャネル](notification-channel.md)を参照してください。

### <a name="impersonation-and-notification"></a>権限借用と通知

IPrintAsyncNotify::CreatePrintAsyncNotifyChannel メソッドを呼び出すときに、フィルターは、ユーザー アカウントを借用しませんする必要があります。 印刷スプーラで承認メカニズムは、ローカル サービス アカウントから呼び出されることが必要です。 フィルターは、ジョブを送信したユーザーのアカウントを偽装する必要がある場合、フィルターは、CreatePrintAsyncNotifyChannel を呼び出す前にそれ自体に戻す必要があります。 呼び出しが返された後に、フィルターは、必要に応じて、ユーザー アカウントに戻すことができます。

**注**  ジョブ ID のユーザーの関連付けに基づいてジョブを送信したユーザーに通知呼び出しは、ローカル サービスのコンテキストで行われますが、場合でも kPerUser の通知が送信されます

 

### <a name="adapting-the-wdk-sample-code"></a>WDK サンプル コードを調整

RouterCreatePrintAsyncNotificationChannel 呼び出しを次のコード例に置き換えることにより、印刷フィルターで作業する WDK サンプル コードからの通知のサンプルを適用することができます。

```cpp
IPrintAsyncNotify  *pIAsyncNotify;

HRESULT hr = m_pPrintClassFactory->GetPrintClassObject(
 m_bstrPrinterName,      // get it from the property bag
 IID_IPrintAsyncNotify,
 reinterpret_cast<void**>(&pIAsyncNotify)));

if (SUCCEEDED(hr))
{
    hr = pIAsyncNotify->CreatePrintAsyncNotifyChannel(
 // the same arguments as for 
 // RouterCreatePrintAsyncNotificationChannel
        );

    // Etc.
}
```

 

 





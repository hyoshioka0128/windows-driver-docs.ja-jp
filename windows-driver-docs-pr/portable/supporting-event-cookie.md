---
Description: イベント Cookie のサポート
title: イベント Cookie のサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61ebf90a6099af34ff0c7eca57c2f5fb777f5d64
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380850"
---
# <a name="supporting-event-cookies"></a>イベント Cookie のサポート


WPD アプリケーションまたは指定できます、一意の文字列「クッキー」クライアント情報のいずれかの呼び出し時に、 **IPortableDevice::Open**メソッドまたは**IPortableDeviceService::Open**メソッド。 これらのアプリケーションは、ドライバーを使用して、それぞれのイベント ハンドラーを登録するときに、ドライバーはこの cookie をイベント データを返します。 Cookie を確認するには、アプリケーションは、指定したイベントを処理するかどうかを判断できます。

たとえば、アプリケーション A は、デバイスでオブジェクトを作成し、WPD は受信\_イベント\_オブジェクト\_そのクライアントのイベントの cookie を格納する追加されたイベント。 アプリケーション A は、オブジェクトの作成時に、ビューが更新されたので、デバイスの内容のビューを更新しないを選択できます。 アプリケーション B は、デバイス上の別のオブジェクトを作成、アプリケーション A に与え、WPD\_イベント\_オブジェクト\_を別の cookie (またはない cookie) を持つイベントを追加します。 Cookie を確認するには、アプリケーション A のでかかることが、適切なアクションとデバイスの内容を表示、更新アプリケーション B が新しいオブジェクトを追加します。 WPD イベントは、すべてのアプリケーションにブロードキャストされる、ため、イベントの cookie の値はアプリケーションがデバイスと前の対話中に、トリガーがイベントをフィルター処理時に最も役立ちます。

アプリケーションによっては、cookie には、アプリケーションまたは CLSID、アプリケーションの作成と同時に複数のインスタンスを実行できる場合は、一意識別子の実行可能ファイル名が含まれます。 実際の文字列の内容は、ドライバーには関係ありません。

環境では 2 つありますが、または (Windows エクスプ ローラーは事実上保証 WPD シェル Namespace 拡張機能を使用して 1 つクライアント)、ドライバーと通信するクライアント アプリケーションの詳細イベント cookie のメカニズムをサポートすることをお勧めが。 そうはという WPD プログラミング手法に役立つトラフィックを減らす、クライアント アプリケーション側のイベント処理の効率化、イベントへの応答で、デバイスに。

## <a name="span-idstepstosupporttheeventcookiespanspan-idstepstosupporttheeventcookiespanspan-idstepstosupporttheeventcookiespansteps-to-support-the-event-cookie"></a><span id="Steps_to_Support_the_Event_Cookie"></span><span id="steps_to_support_the_event_cookie"></span><span id="STEPS_TO_SUPPORT_THE_EVENT_COOKIE"></span>イベント クッキーがサポートする手順


次の手順は、WPD をサポートする方法を識別\_クライアント\_イベント\_WPD ドライバー内のクッキー。

1.  WPD のハンドラーを追加\_コマンド\_共通\_保存\_クライアント\_情報コマンド。 WDK から WpdWudfSampleDriver にはでこの例が含まれています、 **WpdBaseDriver::OnSaveClientInfo**メソッド。
2.  **OnSaveClientInfo** WPD 設定されている場合、メソッド\_クライアント\_イベント\_クライアント情報のパラメーターでクッキーが、コンテキスト情報を cookie を保存します。 一部のアプリケーションがこの cookie を送信しないように選択可能性があります、その場合、ドライバーが何かこの手順を行います。
3.  イベントを送信すると、クライアント イベントの cookie を使用できる場合は、イベント パラメーターと共に送信します。 このコードを追加、ドライバーのサンプルで、 **PostWpdEvent**関数。

次のコード例では、WpdWudfSampleDriver ハンドルをステップ前の一覧に 2 つの方法を示します。

```ManagedCPlusPlus
LPWSTR pszEventCookie = NULL; 
hr = pClientInfo->GetStringValue(WPD_CLIENT_EVENT_COOKIE, &pszEventCookie);
if (hr == S_OK && pszEventCookie != NULL){    
// Store the cookie value with the client context    
pContext->EventCookie = pszEventCookie;
}
CoTaskMemFree(pszEventCookie);
```

次のコード例では、WpdWudfSampleDriver ハンドルをステップ、上記の 3 つの方法を示します。

```ManagedCPlusPlus
HRESULT hrEventCookie = GetClientEventCookie(pCommandParams, &pszEventCookie);
if (hrEventCookie == S_OK && pszEventCookie != NULL)
{    
// Add it to the event parameters    
// The application's OnEvent callback will match this with its cookie    
hrEventCookie = pEventParams->SetStringValue(WPD_CLIENT_EVENT_COOKIE, pszEventCookie);
}
CoTaskMemFree(pszEventCookie);
```

次のコード例には、GetClientEventCookie ヘルパー関数の概要が含まれています。 ヘルパー関数では、コンテキスト マップに保存されているクライアントの cookie を検索するコマンド パラメーターで指定されているクライアント情報のコンテキストを使用します。

```ManagedCPlusPlus
ClientContext* pClientContext = NULL;   
// This is a context helper object defined by the sample 
driverhr = pCommandParams->GetStringValue(WPD_PROPERTY_COMMON_CLIENT_INFORMATION_CONTEXT, &pszClientContext);
if (hr == S_OK)
{    
hr = GetClientContext(pCommandParams, pszClientContext, (IUnknown**)&pClientContext);    
if (hr == S_OK && pClientContext != NULL && pClientContext->EventCookie.GetLength() > 0)    
{       
// Allocate the cookie string to return        
*ppszEventCookie = AtlAllocTaskWideString(pClientContext->EventCookie);    
}    
if (pClientContext != NULL)          
pClientContext->Release();    
CoTaskMemFree(pszClientContext);
}
```

 

 





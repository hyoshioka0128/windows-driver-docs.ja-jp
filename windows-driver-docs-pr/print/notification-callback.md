---
title: 通知コールバック
description: 通知コールバック
ms.assetid: cf884097-45a4-4ef3-8ebb-64c006838235
keywords:
- スプーラ通知 WDK print、コールバック
- 印刷スプーラ通知 WDK、コールバック
- 通知コールバックの WDK 印刷スプーラ
- IPrintAsyncNotifyCallback
- コールバック WDK スプーラ通知
ms.date: 06/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: b8a7816c3d179f6cf364d158c0770e2b287f7bb6
ms.sourcegitcommit: d71024c0c782b5c013192d960700802eafc120f7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84507105"
---
# <a name="notification-callback"></a>通知コールバック

通知を受け取る必要があるすべての印刷コンポーネントまたは待機中のアプリケーションは、 [IPrintAsyncNotifyCallback](https://docs.microsoft.com/windows/win32/api/prnasnot/nn-prnasnot-iprintasyncnotifycallback)インターフェイスを公開するオブジェクトを提供する必要があります。 インターフェイスは**IUnknown**から継承されるため、スプーラ通知機構のクライアントは COM オブジェクトまたは C++ オブジェクトを実装できます。

リッスンしているアプリケーションは、通知を受信するために登録するときに、 **IPrintAsyncNotifyCallback**インターフェイスへのポインターを提供する必要があります。 応答に関心があり、双方向チャネルを作成する場合、通知の送信者は**IPrintAsyncNotifyCallback**インターフェイスへのポインターを提供する必要があります。

```cpp
#define INTERFACE IPrintAsyncNotifyCallback
DECLARE_INTERFACE_(IPrintAsyncNotifyCallback, IUnknown)
{
    STDMETHOD(QueryInterface)(
        THIS_
        REFIID riid,
        void** ppvObj
        ) PURE;

    STDMETHOD_(ULONG, AddRef)(
        THIS
        ) PURE;

    STDMETHOD_(ULONG, Release)(
        THIS
        ) PURE;

    STDMETHOD(OnEventNotify)(
         THIS_
 IN IPrintAsyncNotifyChannel*,
         IN IPrintAsyncNotifyDataObject*
         ) PURE;

 STDMETHOD(ChannelClosed)(
         THIS_
         IN IPrintAsyncNotifyChannel*,
         IN IPrintAsyncNotifyDataObject*
         ) PURE;
};
```

チャネルのいずれかのエンドから通知が送信されると、スプーラサービスはチャネルのもう一端で[IPrintAsyncNotifyCallback:: OnEventNotify](https://docs.microsoft.com/windows/win32/api/prnasnot/nf-prnasnot-iprintasyncnotifycallback-oneventnotify)メソッドを呼び出して、通知を配信します。

通知チャネルが1つのエンドで閉じられると、スプーラサービスは、もう一方の端で[IPrintAsyncNotifyCallback:: ChannelClosed](https://docs.microsoft.com/windows/win32/api/prnasnot/nf-prnasnot-iprintasyncnotifycallback-channelclosed)メソッドを呼び出し、チャネルが閉じていることを通知します。 チャネルを閉じる理由は、通知として配信されます。

サーバーまたはリッスンしているアプリケーションのいずれかが停止した場合は、スプーラランダウンコードによってこの状態が検出され、まだ生きているチャネルの "まだ生きている" エンドには、通知リリースメッセージが配信される**IPrintAsyncNotifyCallback:: ChannelClosed**呼び出しによって通知され \_ ます。

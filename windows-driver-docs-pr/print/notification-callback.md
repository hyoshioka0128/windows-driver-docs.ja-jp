---
title: 通知のコールバック
description: 通知のコールバック
ms.assetid: cf884097-45a4-4ef3-8ebb-64c006838235
keywords:
- スプーラ通知 WDK の印刷、コールバック
- 印刷スプーラ通知 WDK、コールバック
- 通知コールバックの WDK 印刷スプーラー
- IPrintAsyncNotifyCallback
- WDK スプーラー通知のコールバック
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45e2a91ba3ad89ffd19c554853cf15ad49c68c46
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530968"
---
# <a name="notification-callback"></a>通知のコールバック





任意の印刷コンポーネントまたは通知を受け取ることに関心がリッスンしているアプリケーションを公開するオブジェクトを提供する必要があります、 [IPrintAsyncNotifyCallback](https://go.microsoft.com/fwlink/p/?linkid=124755)インターフェイス。 インターフェイスを継承**IUnknown**スプーラーの通知メカニズムのクライアントが、COM または C++ オブジェクトのいずれかに実装できるようにします。

リッスンしているアプリケーションへのポインターを提供する必要があります、 **IPrintAsyncNotifyCallback**インターフェイスへの通知を登録するとき。 通知の送信側へのポインターを提供する必要があります、 **IPrintAsyncNotifyCallback**インターフェイスの場合は、応答を求めているし、双方向チャネルを作成します。

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

チャネルの 1 つの端から通知が送信されると、スプーラー サービスを呼び出す、 [IPrintAsyncNotifyCallback::OnEventNotify](https://go.microsoft.com/fwlink/p/?linkid=124757)メソッド、通知を配信するチャネルのもう一方の端にします。

スプーラ サービスを呼び出す一方の end で通知チャネルが閉じられたときに、 [IPrintAsyncNotifyCallback::ChannelClosed](https://go.microsoft.com/fwlink/p/?linkid=124756)メソッド、もう一方の end をチャネルが閉じられたことを発表します。 チャネルを終了する理由は、通知として配信されます。

スプーラ ランダウン コードは、この状態を検出し、チャネルはまだ有効な状態の「アライブ」の末尾に通知されるサーバーまたはリッスンしているアプリケーションが停止した場合、 **IPrintAsyncNotifyCallback::ChannelClosed**でを呼び出すこの通知\_リリース メッセージを配信します。

 

 





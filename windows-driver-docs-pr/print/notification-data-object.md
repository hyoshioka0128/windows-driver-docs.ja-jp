---
title: 通知データ オブジェクト
description: 通知データ オブジェクト
ms.assetid: 6ba8840d-a693-485c-81da-81205e511120
keywords:
- スプーラ通知 WDK print、データオブジェクト
- 印刷スプーラ通知 WDK、データオブジェクト
- 通知データオブジェクト WDK 印刷スプーラ
- IPrintAsyncNotifyDataObject
- データオブジェクト WDK スプーラ通知
ms.date: 06/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: 2b955d6405af507c67e7d255569f01e980b7013f
ms.sourcegitcommit: d71024c0c782b5c013192d960700802eafc120f7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84507109"
---
# <a name="notification-data-object"></a>通知データ オブジェクト

通知データは、 [IPrintAsyncNotifyDataObject](https://docs.microsoft.com/windows/win32/api/prnasnot/nn-prnasnot-iprintasyncnotifydataobject)インターフェイスを公開するオブジェクトとして処理されます。 スプーラ通知パイプのクライアントは、独自のデータスキーマを定義でき、任意のデータ型を前後に送信できます。 ただし、スプーラは、通知データオブジェクトに対して、バイト \* ポインター、データ長、および通知の種類を照会します。 通知の種類は、「[通知の種類](notification-filtering-and-communication-styles.md#notification-types)」で説明されている GUID です。

```cpp
#define INTERFACE IPrintAsyncNotifyDataObject
DECLARE_INTERFACE_(IPrintAsyncNotifyDataObject, IUnknown)
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

    STDMETHOD(AcquireData)(
         THIS_
         OUT BYTE**,
         OUT ULONG*,
         OUT PrintAsyncNotificationType**
         ) PURE;

    STDMETHOD(ReleaseData)(
        THIS
        ) PURE;
};
```

通知の送信者は、 **IPrintAsyncNotifyDataObject**オブジェクトのデータをパックする必要があります。 送信側は[IUnknown](https://docs.microsoft.com/windows/win32/api/unknwn/nn-unknwn-iunknown)インターフェイスを実装する必要があります。

リッスンしているクライアントは、 [IPrintAsyncNotifyDataObject:: AcquireData](https://docs.microsoft.com/windows/win32/api/prnasnot/nf-prnasnot-iprintasyncnotifydataobject-acquiredata)メソッドを呼び出して、通知データへの生のポインター、通知データのサイズ、および通知の種類を取得します。

リッスンしているクライアントがデータを使用して終了したら、 [IPrintAsyncNotifyDataObject:: ReleaseData](https://docs.microsoft.com/windows/win32/api/prnasnot/nf-prnasnot-iprintasyncnotifydataobject-releasedata)メソッドを呼び出す必要があります。 スプーラ通知パイプのクライアントは、 **IPrintAsyncNotifyDataObject:: ReleaseData**メソッドが呼び出される前に**IPrintAsyncNotifyDataObject:: Release**メソッドが呼び出された場合に、オブジェクトが解放されないように、 **IPrintAsyncNotifyDataObject**インターフェイスを実装する必要があります。 **IPrintAsyncNotifyDataObject:: AcquireData**メソッドを呼び出すとオブジェクトの参照カウントがインクリメントされ、 **releasedata**メソッドを呼び出すとオブジェクトの参照カウントがデクリメントされることをお勧めします。

スプーラは、NOTIFICATION RELEASE という名前の特別な通知の種類の GUID を定義し \_ ます。 スプーラまたはリスニングアプリケーションが停止すると、ランダウンコードは[IPrintAsyncNotifyChannel:: CloseChannel](https://docs.microsoft.com/windows/win32/api/prnasnot/nf-prnasnot-iprintasyncnotifychannel-closechannel)メソッドを呼び出すことによって、チャネルの "生きた" 終了を公開します。

この通知に対して**IPrintAsyncNotifyDataObject:: AcquireData**メソッドを呼び出すと、BYTE \* \* パラメーターが**NULL**に設定され、ULONG パラメーターが0に設定され、 \* GUID \* パラメーターが notification RELEASE に設定された状態で返さ \_ れます。

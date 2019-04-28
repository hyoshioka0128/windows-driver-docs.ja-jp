---
title: 通知データ オブジェクト
description: 通知データ オブジェクト
ms.assetid: 6ba8840d-a693-485c-81da-81205e511120
keywords:
- スプーラ通知 WDK 印刷、データ オブジェクト
- 通知は、印刷スプーラの WDK、データ オブジェクト
- 通知のデータ オブジェクトの WDK 印刷スプーラー
- IPrintAsyncNotifyDataObject
- データ オブジェクトの WDK スプーラーの通知
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eea6f5532c4baf19af9d3671658ea1662ab7e6a0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382783"
---
# <a name="notification-data-object"></a>通知データ オブジェクト





通知のデータが公開するオブジェクトとして処理されます、 [IPrintAsyncNotifyDataObject](https://go.microsoft.com/fwlink/p/?linkid=124761)インターフェイス。 スプーラー通知パイプのクライアントは、独自のデータ スキーマを定義でき、任意のデータ型を前後へ送信することができます。 ただし、通知のデータ オブジェクトのバイトのクエリ、スプーラー\*ポインター、データ、および通知の種類の長さ。 」の説明に従って、通知の種類が、GUID、[通知の種類](notification-filtering-and-communication-styles.md#notification-types)します。

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

通知の送信側にデータをパックする必要があります、 **IPrintAsyncNotifyDataObject**オブジェクト。 送信者を実装する必要があります、 [IUnknown](https://go.microsoft.com/fwlink/p/?linkid=124716)インターフェイス。

リッスンしているクライアントが呼び出す、 [IPrintAsyncNotifyDataObject::AcquireData](https://go.microsoft.com/fwlink/p/?linkid=124762)通知データ、通知のデータと通知の種類のサイズに生のポインターを取得します。

リッスンしているクライアントは、完了すると、データが、呼び出す必要があります、 [IPrintAsyncNotifyDataObject::ReleaseData](https://go.microsoft.com/fwlink/p/?linkid=124763)メソッド。 スプーラー通知パイプのクライアントを実装する必要があります、 **IPrintAsyncNotifyDataObject**場合にこのような方法でインターフェイス、 **IPrintAsyncNotifyDataObject::Release**メソッドは前に、**IPrintAsyncNotifyDataObject::ReleaseData**メソッドが呼び出されると、オブジェクトは解放されません。 推奨されますへの呼び出し、 **IPrintAsyncNotifyDataObject::AcquireData**メソッドとオブジェクトの参照カウントをインクリメントする必要がありますを呼び出し、 **ReleaseData**メソッドはデクリメントする必要がありますオブジェクトの参照カウントします。

スプーラが特別な通知の種類の通知をという名前の GUID を定義します\_リリースします。 ランダウンのコードが呼び出すことによって、チャネルの「アライブ」の末尾を発表スプーラーまたはリッスンしているアプリケーションのいずれかが実行されていないときに、 [IPrintAsyncNotifyChannel::CloseChannel](https://go.microsoft.com/fwlink/p/?linkid=124759)メソッド。

呼び出し、 **IPrintAsyncNotifyDataObject::AcquireData**この通知に対するメソッドを返しますバイト\*\*パラメーターに設定**NULL**、ULONG\*パラメーターが 0、および GUID に設定\*パラメーターには、通知設定\_リリースします。

 

 





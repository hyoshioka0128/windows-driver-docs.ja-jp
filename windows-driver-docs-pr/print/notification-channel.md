---
title: 通知チャンネル
description: 通知チャンネル
ms.assetid: 3161342a-0737-4f3b-bb16-32d6949bceea
keywords:
- スプーラ通知 WDK print、channel
- 印刷スプーラ通知 WDK、チャネル
- 通知チャネル WDK 印刷スプーラ
- CreatePrintAsyncNotifyChannel
- チャネル通知 WDK 印刷スプーラ
- データチャネル WDK スプーラ通知
- IPrintAsyncNotifyChannel
ms.date: 06/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: 7402b2c0a0add32e2a57e393d9b260e810a0283d
ms.sourcegitcommit: d71024c0c782b5c013192d960700802eafc120f7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84507107"
---
# <a name="notification-channel"></a>通知チャンネル

このセクションには、 [CreatePrintAsyncNotifyChannel](https://docs.microsoft.com/windows/win32/api/prnasnot/nf-prnasnot-createprintasyncnotifychannel)関数と[IPrintAsyncNotifyChannel](https://docs.microsoft.com/windows/win32/api/prnasnot/nn-prnasnot-iprintasyncnotifychannel)インターフェイスに関する情報が含まれています。

```cpp
HRESULT
 CreatePrintAsyncNotifyChannel(
    IN LPCWSTR,
    IN PrintAsyncNotificationType*,
    IN PrintAsyncNotifyUserFilter,
    IN PrintAsyncNotifyConversationStyle,
    IN IPrintAsyncNotifyCallback*,
 OUT IPrintAsyncNotifyChannel**
    );
```

印刷コンポーネントは、通知チャネルを作成するために**CreatePrintAsyncNotifyChannel**関数を呼び出します。 チャネルは、プリンターごとまたはサーバーごとに指定できます。

印刷コンポーネントは、コンポーネントがスプーラによって読み込まれた場合にのみ、通知チャネルを開くことができます。 呼び出し元がスプーラサービスではなく、アプリケーション内で実行されている場合、winspool. drv はこの機能を無効にします。 たとえば、アプリケーションがレンダリングを実行するためにドライバーを読み込む場合、 **CreatePrintAsyncNotifyChannel**の呼び出しは失敗します。 ただし、ドライバーがスプーラサービスによって読み込まれた場合、同じ呼び出しは成功します。

Spoolss は、ポートモニターがチャネルを開けるように、この機能を提供します。 スプーラ内で実行され、Spoolss にリンクされているコンポーネントは、 **CreatePrintAsyncNotifyChannel**関数を呼び出すことができます。 次の手順では、この関数の呼び出しにおける各入力パラメーターの目的について説明します。 このプロシージャの最初のステップは、この関数の最初のパラメーターに適用され、2番目のステップは2番目のパラメーターに適用されます。

通知チャネルを作成するには、次の項目を指定します。

1. プリンターまたはサーバーの名前。

1. 通知チャネルの種類。 呼び出し元は、このチャネルで送信される通知の種類を指定できます。

1. ユーザーフィルター。 呼び出し元は、通知を受信するユーザー (通知の送信者と同じユーザーまたはすべてのユーザー) を指定できます。

1. メッセージ交換フィルター。 呼び出し元は、これが一方向チャネルと双方向チャネルのどちらであるかを指定する必要があります。 チャネルを一方向としてマークするには、CreatePrintAsyncNotifyChannel の最後のパラメーター (型**IPrintAsyncNotifyChannel** \* \* ) を**NULL**に設定します。 **CreatePrintAsyncNotifyChannel**

1. チャネルのもう一方の端から通知が返されたときに呼び出される**IPrintAsyncNotifyCallback**インターフェイス。 呼び出し元が応答を受信したくない場合は、 **NULL**になることがあります。

**CreatePrintAsyncNotifyChannel**がを返す場合、6番目のパラメーター ( **IPrintAsyncNotifyChannel**型) は、 \* \* **IPrintAsyncNotifyChannel**オブジェクトのアドレスを格納しているメモリ位置を指します。 このオブジェクトは、チャネルを識別し、通知を送信したり、チャネルを閉じたりするために使用されます。

## <a name="iprintasyncnotifychannel-interface"></a>IPrintAsyncNotifyChannel インターフェイス

**IPrintAsyncNotifyChannel**インターフェイスはチャネルを識別し、通知を送信したり、チャネルを閉じたりするために使用されます。 印刷コンポーネントが通知チャネルを作成するために**CreatePrintAsyncNotifyChannel**関数を呼び出すと、スプーラサービスは**IPrintAsyncNotifyChannel**インターフェイスを公開するオブジェクトを提供することによって応答します。

このインターフェイスは、スプーラ通知機構のクライアントが COM オブジェクトまたは C++ オブジェクトを実装できるように、 **IUnknown**インターフェイスから継承されます。 次のコード例のインターフェイス宣言は、この継承を示しています。

```cpp
#define INTERFACE IPrintAsyncNotifyChannel
DECLARE_INTERFACE_(IPrintAsyncNotifyChannel, IUnknown)
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

    STDMETHOD(SendNotification)(
         THIS_
         IN IPrintAsyncNotifyDataObject*
         ) PURE;

    STDMETHOD(CloseChannel)(
         THIS_
         IN IPrintAsyncNotifyDataObject*
         ) PURE;
};
```

通知を送信するために、送信側は[IPrintAsyncNotifyChannel:: SendNotification](https://docs.microsoft.com/windows/win32/api/prnasnot/nf-prnasnot-iprintasyncnotifychannel-sendnotification)メソッドを呼び出します。 送信側は、チャネルを開く印刷コンポーネントのいずれかにすることができます。通知に応答する必要がある場合は、通知またはリッスンしているクライアントを送信します。 このメソッドは、非同期的に動作します。 メソッドが成功コードを返すと、スプーラはリスナーに通知を送信しようとします。 ただし、リスナーが通知を受信する保証はありません。

チャネルを閉じるには、送信側またはリスナーが[IPrintAsyncNotifyChannel:: CloseChannel](https://docs.microsoft.com/windows/win32/api/prnasnot/nf-prnasnot-iprintasyncnotifychannel-closechannel)メソッドを呼び出すことができます。 呼び出し元は、チャネルを閉じる理由を示す通知を渡すことができます。または、 **NULL**ポインターを渡すこともできます。 チャネルを閉じると、キューに置かれたすべての通知が破棄されます。

チャネルオブジェクトに対して[Release](https://docs.microsoft.com/windows/win32/api/unknwn/nf-unknwn-iunknown-release)を呼び出すことは、すべての一般的な COM プログラミングの不変条件に従うわけではないため、注意する必要があります。 次の条件が発生した場合にのみ、 **IPrintAsyncNotifyChannel**で**Release**を呼び出す必要があります。

- [AddRef](https://docs.microsoft.com/windows/win32/api/unknwn/nf-unknwn-iunknown-addref)を明示的に呼び出した場合、 **Release**の呼び出しと照合する必要があります。

- チャネルを一方向として作成した場合は、出力パラメーターとして受け取ったポインターに対して**Release**を1回呼び出す必要があります。 目的の通知を送信し、チャネルを終了したら、 **Release**を呼び出す必要があります。

- チャネルを双方向として作成した場合は、出力パラメーターとして受け取ったポインターに対して**Release**を1回呼び出す必要があります。 次の1つまたは複数の操作を実行する場合にのみ、 **Release**を呼び出す必要があります。

  - 双方向チャネルの**Release**を呼び出す前に、常に**CloseChannel**を呼び出して、成功の結果を受け取る必要があります。 **CloseChannel**の呼び出しが失敗した場合は、チャネルが既に解放されている可能性があるため、 **Release**を呼び出すことはできません。

  - **Channelclosed**イベントの入力中に**Release**を呼び出すことはできません。 この状況を回避するには、エラーチャネルが既に閉じられている状態で失敗した**CloseChannel**への呼び出しを確認し \_ \_ ます。 この場合は、チャネルが既にリリースされているため、 **Release**を呼び出す必要はありません。

  - **Channelclosed**コールバック関数の実行が完了している場合は、チャネルで**CloseChannel**、 **Release**、またはその他のメンバー関数を呼び出すことはできません。 この場合、チャネルは既に解放されているため、それ以降の呼び出しでは未定義の動作が発生する可能性があります。 この制限には、フォアグラウンドスレッドとコールバックオブジェクト間の調整が必要になる場合があります。

  - フォアグラウンドスレッドおよびコールバックオブジェクトが**CloseChannel**と**Release**の呼び出しを調整していることを確認する必要があります。 他のがを呼び出そうとしているか、 **Release**の呼び出しが完了している場合、フォアグラウンドスレッドとコールバックオブジェクトは**CloseChannel**への呼び出しを開始できません。 この制限は、 [**InterlockedCompareExchange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockedcompareexchange)ルーチンを使用して実装できます。 **InterlockedCompareExchange**を使用しない場合は、未定義の動作が発生する可能性があります。

- チャネルにリスナーとして登録した場合は、 **CloseChannel**を呼び出し、 [IPrintAsyncNotifyCallback:: oneventnotify](https://docs.microsoft.com/windows/win32/api/prnasnot/nf-prnasnot-iprintasyncnotifycallback-oneventnotify)コールバック関数で**Release**を呼び出して双方向通信を終了できます。 ただし、 **Channelclosed**コールバックでは**CloseChannel**または**Release**を呼び出さないでください。

これらのいずれかの条件を満たしている場合は、 **Release**を呼び出す必要があります。 これらの条件のいずれかを満たしていない場合は、 **Release**を呼び出すことはできません。

> [!NOTE]
> 上記のいずれかの条件下で**Release**を呼び出すことはできますが、最初に**AddRef**を明示的に呼び出すことは、一般的な COM プログラミングパターンの例外です。 **IPrintAsyncNotifyChannel**は、このような状況では標準的な COM プラクティスとは異なります。

---
title: 通知チャンネル
description: 通知チャンネル
ms.assetid: 3161342a-0737-4f3b-bb16-32d6949bceea
keywords:
- スプーラ通知 WDK の印刷、チャネル
- 印刷スプーラ通知 WDK とチャネル
- 通知チャネルの WDK 印刷スプーラー
- CreatePrintAsyncNotifyChannel
- チャネル通知 WDK の印刷スプーラー
- データ チャネルの WDK スプーラーの通知
- IPrintAsyncNotifyChannel
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d6094c2414aa5648d8dd585274e057a5abcfcce
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385970"
---
# <a name="notification-channel"></a>通知チャンネル





このセクションでは、に関する情報を格納、 [CreatePrintAsyncNotifyChannel](https://go.microsoft.com/fwlink/p/?linkid=124750)関数と[IPrintAsyncNotifyChannel](https://go.microsoft.com/fwlink/p/?linkid=124758)インターフェイス。

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

コンポーネントの呼び出しの印刷、 **CreatePrintAsyncNotifyChannel**通知チャネルを作成する関数。 チャネルは、プリンターごとまたはサーバーごとに指定できます。

印刷のコンポーネントは、コンポーネントが、スプーラーによって読み込まれる場合にのみ、通知チャネルを開くことができます。 Winspool.drv は、アプリケーション内で、スプーラー サービスではなく、呼び出し元が実行されている場合、この機能を無効にします。 呼び出しのレンダリングを実行するドライバーが読み込まれたら、アプリケーション**CreatePrintAsyncNotifyChannel**は失敗します。 ただし、スプーラー サービスによって、ドライバーが読み込まれている場合、同じ呼び出しは成功します。

Spoolss.lib では、この機能を提供するため、ポート モニターは、チャネルを開くことができます。 スプーラー内で実行して、Spoolss.lib にリンクされているコンポーネントを呼び出すことができます、 **CreatePrintAsyncNotifyChannel**関数。 次の手順では、この関数の呼び出しで各入力パラメーターの目的について説明します。 最初の手順の手順では、この関数の最初のパラメーターに適用されます、2 番目のパラメーター、およびなどに 2 番目の手順が適用されます。

通知チャネルを作成するには、次の項目を指定します。

1.  プリンターまたはサーバーの名前。

2.  通知チャネルの種類。 呼び出し元がこのチャネルで送信される通知の種類を指定できます。

3.  ユーザー フィルター。 呼び出し元は、通知送信側と同じユーザーまたはすべてのユーザーか、通知を受信しているユーザーを指定できます。

4.  メッセージ交換を返すフィルター。 呼び出し元は、これは、一方向または双方向チャネルかどうかを指定する必要があります。 一方向として、チャネルをマークするには、最後のパラメーターを設定します (型の**IPrintAsyncNotifyChannel**\*\*) の**CreatePrintAsyncNotifyChannel**に**NULL**.

5.  **IPrintAsyncNotifyCallback**インターフェイス通知は、チャネルのもう一方の端から戻ったときに呼び出されます。 これは、 **NULL**呼び出し元が応答を受信する必要はないです場合。

ときに**CreatePrintAsyncNotifyChannel** 6 番目のパラメーターを返します (型の**IPrintAsyncNotifyChannel**\*\*) のアドレスを格納するメモリ位置を指す**IPrintAsyncNotifyChannel**オブジェクト。 このオブジェクトは、チャネルを識別し、通知を送信して、チャネルを閉じるために使用します。

### <a name="iprintasyncnotifychannel-interface"></a>IPrintAsyncNotifyChannel インターフェイス

**IPrintAsyncNotifyChannel**インターフェイスは、チャネルを識別し、通知を送信して、チャネルを閉じるために使用します。 印刷コンポーネントを呼び出すと、 **CreatePrintAsyncNotifyChannel**を公開するオブジェクトを提供することで通知チャネル、スプーラー サービスが応答を作成する関数、 **IPrintAsyncNotifyChannel**インターフェイス。

このインターフェイスから継承、 **IUnknown**インターフェイスの COM または C++ オブジェクトのいずれか、スプーラーの通知メカニズムのクライアントを実装できるようにします。 次のコード例では、インターフェイス宣言では、この継承を示します。

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

送信者の呼び出し、通知を送信する、 [IPrintAsyncNotifyChannel::SendNotification](https://go.microsoft.com/fwlink/p/?linkid=124760)メソッド。 送信者は、チャネルを開き、通知に応答する必要があるときに、通知またはリッスンしているクライアントを送信するか、印刷コンポーネントを指定できます。 このメソッドは非同期的に動作します。 メソッドは、成功コードを返します、スプーラーはリスナーに通知を送信しようとします。 すべてのリスナーに通知を受け取ることの保証はありません。

チャネルを閉じるには、送信者またはリスナーを呼び出すことができます、 [IPrintAsyncNotifyChannel::CloseChannel](https://go.microsoft.com/fwlink/p/?linkid=124759)メソッド。 呼び出し元のチャネルを終了する理由を示す、通知に渡すことができますまたは渡すことができます、 **NULL**ポインター。 チャネルが閉じられたときにキューに置かれたすべての通知は破棄されます。

呼び出すで注意する必要があります[リリース](https://go.microsoft.com/fwlink/p/?linkid=98433)、チャネル オブジェクトの不変性をプログラミングするすべての一般的な COM に従っていないためです。 呼び出す必要があります**リリース**で**IPrintAsyncNotifyChannel**次の条件が発生した場合にのみ。

-   呼び出した場合[AddRef](https://go.microsoft.com/fwlink/p/?linkid=98432)明示的にへの呼び出しと一致する必要がありますと**リリース**します。

-   かどうか、一方向として、チャネルを作成し、呼び出す必要があります**リリース**出力パラメーターとして受信するポインターを 1 回です。 呼び出す必要があります**リリース**目的の通知を送信し、チャネルを終了した後。

-   双方向チャネルを作成した場合は、呼び出しする必要があります**リリース**出力パラメーターとして受信するポインターを 1 回です。 呼び出す必要があります**リリース**次の 1 つ以上を実行する場合にのみ。
    -   呼び出す前に**リリース**双方向チャネルでは、常に呼び出す必要があります**CloseChannel**と成功の結果を受信します。 呼び出す必要はありません**リリース**場合への呼び出し**CloseChannel**チャネルが既にリリースされているあなたの代わりにあるため、失敗します。
    -   呼び出す必要はありません**リリース**入力するときに、 **ChannelClosed**イベント。 このような状況を避けるためには、確認の呼び出しを**CloseChannel**チャネルのエラーで失敗したが\_ALREADY\_終了します。 呼び出す必要はありません**リリース**ここでは、あなたの代わりに、チャネルは既に解放されているためです。
    -   呼び出す必要はありません**CloseChannel**、**リリース**、または場合に、チャネルで、他のメンバー関数、 **ChannelClosed**コールバック関数の実行が終了します。 ここでは、チャネルが既にリリースされているため、呼び出しが未定義の動作を引き起こすこと可能性があります。 この制限は、フォア グラウンド スレッドとコールバック オブジェクト間の調整を必要があります。
    -   フォア グラウンド スレッドとコールバック オブジェクトがへの呼び出しを調整することを確認する必要があります**CloseChannel**と**リリース**します。 呼び出しを始めることはできません、フォア グラウンド スレッドと、コールバック オブジェクト**CloseChannel**を呼び出すには、呼び出し元が完了した他のか**リリース**します。 使用して、この制限を実装することができます、 [ **InterlockedCompareExchange** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-interlockedcompareexchange)ルーチン。 使用しない場合**InterlockedCompareExchange**、未定義の動作が発生する可能性があります。
-   チャネルのリスナーとして登録した場合は、呼び出す**CloseChannel**を呼び出して**リリース**で、 [IPrintAsyncNotifyCallback::OnEventNotify](https://go.microsoft.com/fwlink/p/?linkid=124757)コールバック双方向通信を終了する関数。 ただし、呼び出す必要はありません**CloseChannel**または**リリース**で、 **ChannelClosed**コールバック。

これらの条件のいずれかを満たしている場合を呼び出す必要があります**リリース**します。 これらの条件のいずれかを満たしていない場合は、呼び出す必要はありません**リリース**します。

**注**  呼び出す**リリース**、上記の条件が、最初は、呼び出すことのいずれか**AddRef** 、明示的には、一般的な COM 例外プログラミング パターン。 **IPrintAsyncNotifyChannel**このような状況で標準的な COM の手法とは異なります。

 

 

 





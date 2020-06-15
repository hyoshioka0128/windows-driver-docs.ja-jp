---
title: 登録して通知を受け取る
description: 登録して通知を受け取る
ms.assetid: 2442c204-c9d8-49fa-93ae-02623d08119c
keywords:
- スプーラ通知 WDK 印刷, 受信の登録
- 印刷スプーラの通知 WDK, 受信の登録
- スプーラ通知の受信
- スプーラ通知の登録
- RegisterForPrintAsyncNotifications
- UnRegisterForPrintAsyncNotifications
- スプーラ通知の登録を解除しています
ms.date: 06/12/2020
ms.localizationpriority: medium
ms.openlocfilehash: f2137c8ba609cc7d772afb90d4dbe68c5901bb5d
ms.sourcegitcommit: 8a3cb2a87ce9751059bca8145a55b8cc39c34de9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2020
ms.locfileid: "84756166"
---
# <a name="registering-to-receive-notifications"></a>登録して通知を受信する

リッスンしているクライアントは、 [RegisterForPrintAsyncNotifications](https://docs.microsoft.com/windows/win32/api/prnasnot/nf-prnasnot-registerforprintasyncnotifications)メソッドを呼び出して、通知の受信に登録します。 リッスンしているクライアントは、アプリケーションにすることも、スプーラ内で実行することもできます。 Winspool. drv が読み込まれる場所に関係なく、この機能を公開します。

Spoolss は、ポートモニターが通知に登録できるように、この機能を公開します。 スプーラ内で実行され、Spoolss にリンクするコンポーネントは、 **RegisterForPrintAsyncNotifications**を呼び出すことができます。 次の手順では、この関数の呼び出しで渡す必要がある情報について詳しく説明します。 プロシージャの最初のステップは最初のパラメーターに適用され、2番目のステップは2番目のパラメーターに適用されます。

```cpp
HRESULT
 RegisterForPrintAsyncNotifications(
    IN LPCWSTR,
    IN PrintAsyncNotificationType*,
    IN PrintAsyncNotifyUserFilter,
    IN PrintAsyncNotifyConversationStyle,
    IN IPrintAsyncNotifyCallback*,
    OUT HANDLE*
    );
```

通知を登録するには、次のように指定します。

1. ローカル/リモートプリンターまたはサーバー名。

1. リスナーが関心のある通知の種類。

1. ユーザーフィルター。通知の受信者と同じユーザー、またはすべてのユーザーを対象に、クライアントが通知を受け取るユーザーを示します。

1. メッセージ交換のスタイルフィルター。 クライアントは、一方向または双方向の通信を指定できます。

1. 通知がチャネルのもう一方の端から戻るときに呼び出される[IPrintAsyncNotifyCallback](https://docs.microsoft.com/windows/win32/api/prnasnot/nn-prnasnot-iprintasyncnotifycallback)インターフェイス。 このパラメーターを**NULL**にすることはできません。

この関数が戻るとき、6番目のパラメーター (型ハンドル \* ) が登録ハンドルを指しています。 登録ハンドルは、クライアントが受信する不透明な構造体です。 登録は、登録呼び出しを行うスレッドのユーザー id に関連付けられています。 スプーラーは、クライアントセッションのフィルターに加えて、チャネルのセッションフィルターとクライアントの登録セッションに基づいて、リッスンしているクライアントをフィルター処理します。

リッスンしているクライアントが通知を受信しなくなることをスプーラに通知するには、クライアントが[UnRegisterForPrintAsyncNotifications](https://docs.microsoft.com/windows/win32/api/prnasnot/nf-prnasnot-unregisterforprintasyncnotifications)を呼び出すときにこのハンドルを使用する必要があります。 一方向の通信では、サーバー側で保留中の通知がすべて破棄されます。 双方向通信では、オープンな双方向チャネルがある場合、通信は閉じられるまで続行されます。

```cpp
HRESULT
 UnRegisterForPrintAsyncNotifications(
    IN HANDLE
    );
```

---
title: 登録して通知を受け取る
description: 登録して通知を受け取る
ms.assetid: 2442c204-c9d8-49fa-93ae-02623d08119c
keywords:
- スプーラの通知を受信登録、WDK の印刷
- 印刷スプーラの通知を受信登録 WDK
- スプーラの通知の受信
- スプーラの通知を登録します。
- RegisterForPrintAsyncNotifications
- UnRegisterForPrintAsyncNotifications
- スプーラの通知の登録を解除
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98b168fd0117921d70f043e25039663628f4d3da
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382593"
---
# <a name="registering-to-receive-notifications"></a>登録して通知を受け取る





クライアント呼び出しをリッスンしている、 [RegisterForPrintAsyncNotifications](https://go.microsoft.com/fwlink/p/?linkid=124752)通知を受信するために登録します。 リッスンしているクライアントは、アプリケーションは、またはスプーラの内部で実行できます。 Winspool.drv では、それが読み込まれた場所に関係なく、この機能を公開します。

Spoolss.lib は、ポート モニターは、通知を登録できるように、この機能を公開します。 スプーラー内で実行されるコンポーネントとそのリンクを Spoolss.lib を呼び出すことができます**RegisterForPrintAsyncNotifications**します。 次の手順では、この関数の呼び出しで渡す必要がある情報について説明します。 プロシージャの最初の手順は、最初のパラメーターに適用されます、2 番目のパラメーター、およびなどに 2 番目の手順が適用されます。

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

**通知に登録するには、次のように指定します。**

1.  ローカル/リモート プリンターまたはサーバー名。

2.  通知リスナーが興味の型。

3.  通知送信側と同じユーザーまたはすべてのユーザーは、クライアントがいずれかの通知を受信する必要になるユーザーを示すユーザー フィルター。

4.  メッセージ交換のスタイルを返すフィルター。 クライアントは、どちらかを指定できる一方向または双方向通信します。

5.  [IPrintAsyncNotifyCallback](https://go.microsoft.com/fwlink/p/?linkid=124755)通知チャネルのもう一方の端から制御が戻るときに呼び出されるインターフェイス。 このパラメーターにすることはできません**NULL**します。

ときにこの関数を返す 6 番目のパラメーター (型ハンドルの\*) 登録ハンドルを指します。 登録ハンドルは、クライアントが受信するための非透過構造体です。 登録は、登録の呼び出しを行っているスレッドのユーザー id に関連付けられます。 スプーラは、待機中のクライアント チャネルのセッションのフィルターと、クライアント セッションのフィルターだけでなく、クライアントの登録セッションに基づいてフィルター処理します。

リッスンしているクライアントに通知を受け取るされなくを呼び出すときに、クライアントはこのハンドルを使用する必要があります、スプーラーに通知する[UnRegisterForPrintAsyncNotifications](https://go.microsoft.com/fwlink/p/?linkid=124754)します。 一方向の通信のサーバー側で、保留中の通知が破棄します。 双方向の通信を開いて双方向のチャネルがある場合すると、通信は閉じられるまでを継続します。

```cpp
HRESULT
 UnRegisterForPrintAsyncNotifications(
    IN HANDLE
    );
```









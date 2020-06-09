---
title: 通知のフィルター処理と通信スタイル
description: 通知のフィルター処理と通信スタイル
ms.assetid: 66d019c2-0760-440d-acc4-85a7c073929a
keywords:
- スプーラ通知 WDK 印刷、フィルター処理
- 印刷スプーラ通知 WDK、フィルター処理
- 通知フィルターの WDK 印刷スプーラ
- WDK スプーラ通知のフィルター処理
- CreatePrintAsyncNotifyChannel
- RegisterForPrintAsyncNotifications
- 通知データ型 WDK 印刷スプーラ
- データ型 WDK スプーラ通知
- 通信 WDK スプーラ通知
- すべてのリスナー通知 WDK 印刷スプーラ
- ユーザーごとのリスナーフィルター WDK スプーラ通知
ms.date: 06/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: 363037f2992d3ed7a6733be32543e3c29c36e2ac
ms.sourcegitcommit: d71024c0c782b5c013192d960700802eafc120f7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84507103"
---
# <a name="notification-filtering-and-communication-styles"></a>通知のフィルター処理と通信スタイル

このセクションでは、スプーラープロセスと、プリントプロセッサ、ドライバー、モニターなどの印刷コンポーネントとの間のインターフェイスについて説明します。

## <a name="notification-filtering"></a>通知のフィルター処理

PrintAsyncNotifyUserFilter 列挙型は、2つの状況で使用されます。 これらの最初の部分では、スプーラ内で実行されている印刷コンポーネントが、 [CreatePrintAsyncNotifyChannel](https://docs.microsoft.com/windows/win32/api/prnasnot/nf-prnasnot-createprintasyncnotifychannel)関数を呼び出して通知チャネルを作成します。 呼び出し元は、PrintAsyncNotifyUserFilter 列挙型の1つの列挙子を渡して、通知の受信を許可されているリッスンクライアントを指定します。 2番目の状況では、リッスンしているクライアントは、 [RegisterForPrintAsyncNotifications](https://docs.microsoft.com/windows/win32/api/prnasnot/nf-prnasnot-registerforprintasyncnotifications)関数を呼び出して通知を登録します。 呼び出し元は、受信する必要のある通知を示すために、PrintAsyncNotifyUserFilter 列挙子のいずれかを渡します。

```cpp
typedef enum
{
  kPerUser,
  kAllUsers
} PrintAsyncNotifyUserFilter;
```

次の図では、 **CreatePrintAsyncNotifyChannel**関数の呼び出しで**kPerUser**列挙子が使用されています。 その結果、登録を行ったユーザーと同じユーザーアカウントで実行されているリスナーだけが、通知を受け取ることができます。

![ユーザーごとのリスナーフィルターを示す図](images/notifyfilt1.gif)

次の図では、 **CreatePrintAsyncNotifyChannel**関数の呼び出しで**kallusers**列挙子が使用されています。 その結果、プリンターまたはサーバーに関心のあるすべてのリスナーが通知を受信できるようになります。 この関数の呼び出しでは、管理者のみが**Kallusers**設定を使用できることに注意してください。

![すべてのリスナーへの通知を示す図](images/notifyfilt2.gif)

次の図は、ユーザー1とユーザー2の両方が**RegisterForPrintAsyncNotifications**関数を呼び出して通知を登録し、呼び出しで**kPerUser**列挙子を渡す状況を示しています。 送信された3つの通知のうち、リスナーユーザー1は、セッション0またはセッション1でユーザー1から通知を受信します。 リスナーユーザー2は、セッション2のユーザー2から通知を受信します。

![通知のユーザーごとのフィルター処理を示す図](images/notifyfilt3.gif)

前の図に示されているリッスンしているクライアントが**RegisterForPrintAsyncNotifications**を呼び出しましたが、今回は呼び出しで**kallusers**列挙子を渡すと、すべてのセッションのすべてのリスナーが3つの通知を受け取りました。 この関数の呼び出しでは、管理者のみが**Kallusers**列挙子を使用できることに注意してください。

## <a name="administrators"></a>管理者

管理者は、 \_ \_ 指定された印刷オブジェクトに対するプリンターアクセスの管理権限を持つユーザーです。 管理者は、すべてのユーザーに通知を送信し、すべてのユーザーから通知を受け取ることができます。 通知フィルターは引き続き適用されることに注意してください。

次の図では、Joe は**kPerUser**を使用してチャネルで通知を送信します。 この列挙子に基づいてチャネルをフィルター処理する場合、通知はユーザー 1 (セッション 1) に属しているセッションにのみ送信されます。 ただし、通知はセッション2にも送信されます。これは、管理者がリッスンし、この種類の通知をリッスンしているためです。 通知の種類が同じではないため、セッション3の管理者が通知を受信していないことに注意してください。

![ユーザーごとのフィルターと通知の種類のフィルター処理を示す図](images/notifyfilt4.gif)

## <a name="specifying-the-type-of-communication"></a>通信の種類の指定

通信の種類を指定することによって、印刷コンポーネントは、リスナークライアントからの応答が必要かどうかを示します。また、通知が複数のクライアントから返送された場合にスプーラが処理する方法も示します。

```cpp
typedef enum
{
  kBidirectional = 1,
  kUnidirectional,
} PrintAsyncNotifyConversationStyle
```

通信には、一方向と双方向の2種類があります。 一方向の通信では、リッスンしているクライアントがスプーラの通知に応答しません。 この場合、リッスンしているクライアントは、 **NULL**の[IPrintAsyncNotifyChannel](https://docs.microsoft.com/windows/win32/api/prnasnot/nn-prnasnot-iprintasyncnotifychannel)インターフェイスポインターを受け取るため、通知を送信できません。 双方向通信では、クライアントは通知を受信したときに応答を送信し、印刷コンポーネントのダイアログを使用します。 これは UI 通知ケースです。

複数のセッションが UI 通知に値するコメントを受け取る状況。 この場合、スプーラはチャネルを開き、フィルターに一致するすべてのリスナーに対して、最初の通知を送信するように通知します。 最初のリスナーが応答すると、スプーラーは他のチャネルを閉じ、ダイアログは最初のクライアントで続行されます。

登録されたリッスンクライアントが応答する前に管理者 (など) がログオンした場合、管理者は、リッスンしているクライアントと同じ UI 通知を受け取ります。

(たとえば、管理者が) 最初のユーザーが応答を送信すると、スプーラは接続を他のクライアントに "終了" としてマークします。 他のリッスンしているクライアントが最終的に応答すると、"チャネルが閉じられました" というメッセージを受信します。

## <a name="notification-types"></a>通知の種類

通知の種類は、スプーラがリスナークライアントをフィルター処理するために受け入れて使用する GUID です。 (ヘッダーファイル Prnasnot. h の PrintAsyncNotificationType type 定義を参照してください)。スプーラ非同期通知メカニズムのすべてのクライアントは、独自の通知の種類を定義できます。 スプーラーは、送信される通知の種類の意味を認識していませんが、通知の種類に基づいてリスナークライアントをフィルター処理します。

各通知には、通知データ型が関連付けられている必要があります。 この型は、通知データスキーマを識別します。

Notification データ型に加えて、チャネルに関連付けられている型 (通知チャネルの種類) があります。 通知の送信者とリッスンしているクライアントは、さまざまな目的で通知チャネルの種類を使用します。

チャネルの送信側では、印刷コンポーネントがチャネルを開くときに、そのチャネルを介して送信する通知の種類を指定できます。 そのチャネルを通過するすべての通知は、通知チャネルの種類と同じ種類である必要があります。

送信者は、常に種類を通知に関連付ける必要があります。これにより、スプーラが適切なリッスンクライアントに送信する方法を認識できるようになります。 リッスンしているクライアントは、独自のスキーマに従ってデータを検証する必要があります。 このスキーマは、通知の種類によって識別されます。

チャネルのリスナー側では、リッスンしているクライアントは、登録時に特定の通知データ型を指定することによって、1種類の通知を受信するように要求できます。

スプーラは、サービスまたはアプリケーションが停止したクライアントをリッスンするために使用される特別な通知の種類を定義します。

```cpp
const GUID NOTIFICATION_RELEASE;
```

リッスンしているクライアントは、 [IPrintAsyncNotifyCallback:: ChannelClosed](https://docs.microsoft.com/windows/win32/api/prnasnot/nf-prnasnot-iprintasyncnotifycallback-channelclosed)メソッドが呼び出されたときにのみ、この種類のメッセージを受信できます。

## <a name="notification-registration-handle"></a>通知登録ハンドル

クライアントが通知を登録すると、サーバー側のスプーラは、セキュリティコンテキストなど、アプリケーションに関する情報を含む内部テーブルを保持します。 通知登録ハンドルは、クライアントが受信する不透明な構造体です。

クライアントは、このハンドルを使用することによってのみ、通知を受信するための登録を解除できます。

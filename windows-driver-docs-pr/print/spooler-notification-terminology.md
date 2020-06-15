---
title: スプーラー通知の用語集
description: スプーラー通知の用語集
ms.assetid: 7d4888b1-cb5f-4095-9e1b-c330c04e4971
keywords:
- スプーラ通知 WDK print、用語集
- 印刷スプーラの通知 WDK、用語集
ms.date: 06/12/2020
ms.localizationpriority: medium
ms.openlocfilehash: 043f619262c8fa2aff9cf2b0caea5562ecd2eb07
ms.sourcegitcommit: 8a3cb2a87ce9751059bca8145a55b8cc39c34de9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2020
ms.locfileid: "84756164"
---
# <a name="spooler-notification-terminology"></a>スプーラの通知に関する用語

非同期スプーラの通知については、次の用語が使用されます。

| 期間 | 説明 |
|--|--|
| **コールバックインターフェイス** | リッスンしているクライアントは、通知を登録するときに、 [IPrintAsyncNotifyCallback](https://docs.microsoft.com/windows/win32/api/prnasnot/nn-prnasnot-iprintasyncnotifycallback)インターフェイスへのポインターを提供する必要があります。 このインターフェイスのメソッドは、通知が到着するか、チャネルが閉じられたときにコールバックされます。 |
| **クライアントをリッスンする** | 印刷通知を受信するように登録されたアプリケーションまたはスプーラ内部コンポーネント。 これは、以前にスプーラ通知パイプのクライアントと呼ばれていたものとは異なります。 スプーラ通知パイプのクライアントは、どのコンポーネントが通知の種類とスキーマを定義しているかを示します。 |
| **通知 (notification)** | 印刷コンポーネントとリッスンしているクライアントの間の通知チャネルを介して送信されるデータ。 |
| **通知チャネル** | 論理コンポーネント。 これは、 **IPrintAsyncNotifyCallback**インターフェイスポインターによって表されます。 印刷コンポーネントは、通知を送信する必要があるときに通知チャネルを作成します。 リッスンしているクライアントは、データを印刷コンポーネントに返信するときに、通知チャネルを使用します。 |
| **通知登録ハンドル** | リッスンしているクライアントが通知を受信するために登録するときに、サービスによって作成されるハンドル。 リッスンしているクライアントは、このハンドルを使用して通知の登録を解除できます。 |
| **印刷コンポーネント** | Spoolsv.exe によって読み込まれるコンポーネント (印刷プロセッサ、ドライバー、モニターなど)。 |
| **service** | サービス自体 (Spoolsv.exe) の一部として、またはクライアント側 (Winspool. drv) の一部としてスプーラによって実装される機能。 |

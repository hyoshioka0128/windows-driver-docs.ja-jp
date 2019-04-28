---
title: スプーラー通知の用語集
description: スプーラー通知の用語集
ms.assetid: 7d4888b1-cb5f-4095-9e1b-c330c04e4971
keywords:
- スプーラ通知 WDK の印刷、用語集
- 印刷スプーラ通知 WDK、用語集
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6c9f5a261b823b162460533b45e73645c64d449
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382125"
---
# <a name="spooler-notification-terminology"></a>スプーラー通知の用語集





Asnychronous スプーラー通知の説明で、次の用語が使用されます。

<a href="" id="callback-interface"></a>コールバック インターフェイス  
ポインターを提供する必要がありますの通知をリッスンしているクライアントが登録する場合、 [IPrintAsyncNotifyCallback](https://go.microsoft.com/fwlink/p/?linkid=124755)インターフェイス、このドキュメントの後半で説明します。 このインターフェイスのメソッドは、通知が到着したときに、または、チャネルが閉じられたときに呼び出されます。

<a href="" id="listening-clients-"></a>待機中のクライアント   
アプリケーションまたは印刷の通知を受信する登録されているスプーラー内部コンポーネントのいずれかを指します。 これは、何が以前と呼ばれるスプーラー通知パイプのクライアントと異なります。 スプーラ通知パイプのクライアントとはどのようなコンポーネントは、通知の種類とスキーマを定義します。

<a href="" id="notification"></a>通知  
データは、印刷コンポーネントと待機中のクライアント間の通知チャネルを介して送信されます。

<a href="" id="notification-channel-"></a>通知チャネル   
論理コンポーネントです。 によって表されます、 **IPrintAsyncNotifyCallback**インターフェイス ポインターをこのドキュメントの後半で説明します。

印刷コンポーネントは、通知を送信する必要があるときに、通知チャネルを作成します。 リッスンしているクライアントは、印刷のコンポーネントをバックアップするデータを送信するときに、通知チャネルを使用します。

<a href="" id="notification-registration-handle"></a>通知登録ハンドル  
通知を受け取るサービスがリッスンしているクライアントで作成されたハンドルを登録します。 リッスンしているクライアントは、このハンドルを使用して、通知の登録を解除します。

<a href="" id="printing-component"></a>印刷コンポーネント  
ドライバーをアンロード Spoolsv.exe、プリント プロセッサなどのコンポーネントを参照し、監視します。

<a href="" id="service"></a>サービス  
サービス自体 (Spoolsv.exe) の一部として、またはクライアント側 (Winspool.drv) の一部として、スプーラーによって実装される機能を指します。

 

 





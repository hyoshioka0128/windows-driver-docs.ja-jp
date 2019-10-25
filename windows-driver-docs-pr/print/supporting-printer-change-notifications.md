---
title: プリンター変更通知のサポート
description: プリンター変更通知のサポート
ms.assetid: e75c6f89-9cef-4900-af89-edf1f7f786c7
keywords:
- 印刷プロバイダー WDK、プリンター変更通知
- ネットワーク印刷プロバイダー WDK、プリンターの変更通知
- 通知 WDK プリンター
- プリンター変更通知 WDK
- イベント WDK プリンター
- 印刷キュー WDK、プリンター変更通知
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0fffb3726a62b847da4320b06416715eb3065fcb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838787"
---
# <a name="supporting-printer-change-notifications"></a>プリンター変更通知のサポート





アプリケーションは、スプーラの**FindFirstPrinterChangeNotification**、 **FindNextPrinterChangeNotification**、および**FindClosePrinterChangeNotification**を呼び出すことによって、印刷キューイベントの発生の通知を要求できます。関数。これらの機能については、Microsoft Windows SDK のドキュメントを参照してください。 部分的な印刷プロバイダーでサポートされている印刷キューのイベント通知をアプリケーションの作成者が要求する場合は、次のようにプロバイダーのイベント通知をサポートする必要があります。

-   [**FindFirstPrinterChangeNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winspool/nf-winspool-findfirstprinterchangenotification)関数を指定します。

    スプーラはこの関数を呼び出して、印刷プロバイダーに次の情報を提供します。

    -   アプリケーションが通知を要求したプリンターイベントの種類を示すフラグのセット。
    -   通知が要求されている印刷キューを示すハンドル。
    -   イベントの発生時にアプリケーションから提供されるように要求された情報の種類の一覧。

    関数は、変更が発生したかどうかを判断するためにプロバイダーをポーリングする必要があるかどうかを示すフラグ値を返す必要があります。 (非ポーリングプロバイダーは、変更が発生するたびにクライアントにシグナルを送信します。 ポーリングが必要なプロバイダーは、変更が発生したときにクライアントにシグナルを送信しません。 代わりに、スプーラーは、変更が発生したかどうかにかかわらず、クライアントに一定の間隔で通知します。

    (プロバイダーレベルでは、この関数の引数は Win32 レベルとは異なることに注意してください)。

-   **FindFirstPrinterChangeNotification**を呼び出したときにアプリケーションが指定したすべての印刷キューイベントを追跡します。

    (アプリケーションが要求できる通知の種類の一覧、およびイベントの説明に使用できる情報の種類の一覧については、Windows SDK のドキュメントの Win32 **FindFirstPrinterChangeNotification**の説明を参照してください。プロシージャ. アプリケーションが通知を要求する可能性のあるイベントの種類には、印刷ジョブやフォームの追加や削除があります。 アプリケーションが要求する情報の種類には、ジョブまたはフォームパラメーターがあります。

    ポーリングされていない印刷プロバイダーは、変更が発生したときに[**PartialReplyPrinterChangeNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-partialreplyprinterchangenotification)または[**ReplyPrinterChangeNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-replyprinterchangenotification)を呼び出して、変更を説明する情報をスプーラに提供する必要があります。 **ReplyPrinterChangeNotification**関数は、スプーラによってアプリケーションが通知されるため、ある時点で呼び出す必要がありますが、 **PartialReplyPrinterChangeNotification**関数では呼び出されません。 アプリケーションが**ReplyPrinterChangeNotification**からシグナルを受信すると、 **FindNextPrinterChangeNotification**を呼び出すことになります。 後者の関数は、スプーラーが以前に印刷プロバイダーから受け取ったイベント情報をアプリケーションに提供します。

    ポーリングされた印刷プロバイダーは、単に変更を追跡する必要があります。 スプーラは、アプリケーションに一定の間隔で通知します。 アプリケーションは、シグナルを受信すると、スプーラの**FindNextPrinterChangeNotification**関数を呼び出すことが想定されます。 ポーリングプロバイダーの場合、この関数はプロバイダーの**RefreshPrinterChangeNotification**関数を呼び出します。

-   [**RefreshPrinterChangeNotification**](https://docs.microsoft.com/previous-versions/ff561930(v=vs.85))関数を指定します。

    この関数は、指定された印刷キューのすべての監視対象の印刷キューオプションの現在の状態を返す必要があります。 この機能は、Windows SDK のドキュメントで説明されているように、アプリケーションがプリンターを使用して**FindNextPrinterChangeNotification**を呼び出し、\_オプション\_更新フラグが設定されている場合に、この関数を呼び出し\_ます。 (アプリケーションは、以前に**FindNextPrinterChangeNotification**を呼び出したときにプリンター\_\_情報の構造を返し、\_情報を通知\_破棄フラグが設定されていることを知らせる\_、このフラグを設定することが想定されています)。ポーリングと非ポーリングの両方のプロバイダーが**RefreshPrinterChangeNotification**をサポートしている必要があります。

-   (Windows SDK のドキュメントで説明されている) **FindClosePrinterChangeNotification**関数を指定します。

 

 





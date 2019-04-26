---
title: プリンター変更通知のサポート
description: プリンター変更通知のサポート
ms.assetid: e75c6f89-9cef-4900-af89-edf1f7f786c7
keywords:
- プロバイダー WDK、変更通知のプリンターを印刷します。
- ネットワーク印刷プロバイダー WDK、プリンターの変更通知
- 通知の WDK プリンター
- プリンターの変更通知 WDK
- イベントの WDK プリンター
- 印刷キュー WDK、プリンターの変更通知
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd69e755e959b38879d8b19a14f916d3f934dd41
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354782"
---
# <a name="supporting-printer-change-notifications"></a>プリンター変更通知のサポート





アプリケーションが、スプーラーを呼び出すことによって印刷キューのイベントの発生の通知を要求できる**FindFirstPrinterChangeNotification**、 **FindNextPrinterChangeNotification**、および**FindClosePrinterChangeNotification** Microsoft Windows SDK ドキュメントに記載されているすべての関数。 アプリケーションの作成者は、部分的な印刷プロバイダーでサポートされている印刷キューのイベント通知を要求する場合は、次のように、プロバイダーでイベント通知をサポートする必要があります。

-   提供、 [ **FindFirstPrinterChangeNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff548837)関数。

    スプーラは、次の情報を使用して印刷プロバイダーを指定するには、この関数を呼び出します。

    -   アプリケーションが通知を要求がプリンター イベントの種類を示すフラグのセット。
    -   通知が要求されている印刷キューへのハンドル。
    -   情報の種類の一覧、アプリケーションが要求したは、イベントが発生したときに指定します。

    関数は、変更が発生したかどうかに、プロバイダーをポーリングするかどうかを示すフラグの値を返す必要があります。 (Nonpolled プロバイダーにシグナルを送る、クライアントが変更されたとき。 ポーリングする必要があります、プロバイダーの変更が発生した場合、信号をクライアントに送信しません。 スプーラが一定の間隔でクライアントを通知する代わりに、かどうかの変更があるかどうかが発生しました)。

    (プロバイダー レベルでは、この機能が付いている別の引数よりも Win32 レベルに注意してください)。

-   呼び出されたときに、アプリケーションが指定されているすべての印刷キュー イベントの追跡**FindFirstPrinterChangeNotification**します。

    (アプリケーションが要求、およびイベントを表すために使用できる情報の種類の一覧は、win32、Windows SDK ドキュメントの説明を参照してください通知の種類の一覧については**FindFirstPrinterChangeNotification。** 関数。 アプリケーションが通知を要求がイベントの種類には、印刷ジョブやフォーム追加または削除が含まれます。 アプリケーション要求情報の種類は、ジョブまたはフォーム パラメーターです)

    ポーリングされません印刷のプロバイダーを呼び出す必要があります[ **PartialReplyPrinterChangeNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff559739)または[ **ReplyPrinterChangeNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff561959)変更が発生する場合、変更を説明する情報を含む、スプーラーを指定します。 **ReplyPrinterChangeNotification**関数である必要があります、スプーラーをアプリケーションに通知するので、ある時点で呼び出されると、while、 **PartialReplyPrinterChangeNotification**関数じゃない。 アプリケーションがからの信号を受信すると**ReplyPrinterChangeNotification**、呼び出しが届いていない**FindNextPrinterChangeNotification**します。 この後者の関数は、スプーラーは印刷プロバイダーからまだ受信イベント情報を使用してアプリケーションを提供します。

    ポーリングされるプロバイダーが印刷する必要がありますだけの変更を追跡します。 スプーラは、一定の間隔でアプリケーションを通知します。 スプーラの呼び出しが届いていないアプリケーションは、信号を受信するときに**FindNextPrinterChangeNotification**関数。 ポーリングされたプロバイダーは、この関数の呼び出し、プロバイダーの**RefreshPrinterChangeNotification**関数。

-   提供、 [ **RefreshPrinterChangeNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff561930)関数。

    この関数は、指定した印刷キューのすべての監視対象の印刷キュー オプションの現在の状態を返す必要があります。 スプーラがアプリケーションを呼び出すときに、この関数を呼び出す**FindNextPrinterChangeNotification** 、プリンターに\_通知\_オプション\_Windows SDK で説明されているため、更新フラグを設定ドキュメントです。 (以前の呼び出しの場合は、このフラグを設定することになっているアプリケーション**FindNextPrinterChangeNotification**プリンターを返します\_通知\_、プリンターに情報の構造体\_通知\_情報\_破棄済みフラグを設定します)。ポーリングと nonpolled の両方のプロバイダーをサポートする必要があります**RefreshPrinterChangeNotification**します。

-   提供、 **FindClosePrinterChangeNotification**関数 (Windows SDK のドキュメントで説明)。

 

 





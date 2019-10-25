---
title: ハードウェア プロファイル変更の通知登録
description: ハードウェア プロファイル変更の通知登録
ms.assetid: 3aaa09f7-ac63-4b56-917a-74cf344f6dd3
keywords:
- 通知 WDK PnP, ハードウェアプロファイルの変更
- ハードウェアプロファイルの変更通知の WDK PnP
- Eventカテゴリのハードウェアプロファイルの通知
- プロファイル変更通知の WDK PnP
- ハードウェアプロファイルの変更通知を登録しています
- コンピューターハードウェアプロファイルの変更通知の WDK PnP
- IoRegisterPlugPlayNotification
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e52082e4a23e7b91ffdb78d8bdee048e5419268d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838463"
---
# <a name="registering-for-hardware-profile-change-notification"></a>ハードウェア プロファイル変更の通知登録





ドライバーは、 [**IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)を呼び出すことによって、ハードウェアプロファイルの変更の通知を登録します。

次の情報は、ハードウェアプロファイルの変更通知にこのルーチンを呼び出した場合に適用されます。

-   Eventcategory**の** *eventcategory*を指定します。

-   *Eventカテゴリデータ*は**NULL**である必要があります。

-   PnP マネージャーがコールバックルーチンに渡すドライバー定義の*コンテキスト*を指定します (該当する場合)。

ドライバーは、 **IoRegisterPlugPlayNotification**によって返された*notificationentry*を使用して[**IoUnregisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iounregisterplugplaynotification)を呼び出すことによって、通知登録を削除します。

 

 





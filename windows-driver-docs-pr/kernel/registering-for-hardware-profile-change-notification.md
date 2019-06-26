---
title: ハードウェア プロファイル変更の通知登録
description: ハードウェア プロファイル変更の通知登録
ms.assetid: 3aaa09f7-ac63-4b56-917a-74cf344f6dd3
keywords:
- 通知 WDK PnP、ハードウェア プロファイルの変更
- ハードウェア プロファイルの変更通知 PnP WDK
- EventCategoryHardwareProfileChange 通知
- プロファイルの変更通知 PnP WDK
- ハードウェア プロファイルの変更通知を登録します。
- マシンのハードウェア プロファイルの変更通知 PnP WDK
- IoRegisterPlugPlayNotification
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42a9cdf287197f4676f4d0461a685fa80c13645a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373462"
---
# <a name="registering-for-hardware-profile-change-notification"></a>ハードウェア プロファイル変更の通知登録





ドライバーでは、呼び出すことでハードウェア プロファイルの変更の通知を登録します。 [ **IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterplugplaynotification)します。

次の情報は、ハードウェア プロファイルの変更通知のこのルーチンの呼び出しに適用されます。

-   指定、*によって*の**EventCategoryHardwareProfileChange**します。

-   *EventCategoryData*あります**NULL**します。

-   ドライバーの定義を指定*コンテキスト*、必要に応じて、PnP マネージャーは、コールバック ルーチンに渡されます。

ドライバーを呼び出して通知の登録を削除する[ **IoUnregisterPlugPlayNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iounregisterplugplaynotification)で、 *NotificationEntry*によって返される**IoRegisterPlugPlayNotification**します。

 

 





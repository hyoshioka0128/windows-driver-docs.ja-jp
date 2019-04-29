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
ms.openlocfilehash: 11ad18adc1ac01f59c8aaa6ec9f30eed7d503624
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338445"
---
# <a name="registering-for-hardware-profile-change-notification"></a>ハードウェア プロファイル変更の通知登録





ドライバーでは、呼び出すことでハードウェア プロファイルの変更の通知を登録します。 [ **IoRegisterPlugPlayNotification**](https://msdn.microsoft.com/library/windows/hardware/ff549526)します。

次の情報は、ハードウェア プロファイルの変更通知のこのルーチンの呼び出しに適用されます。

-   指定、*によって*の**EventCategoryHardwareProfileChange**します。

-   *EventCategoryData*あります**NULL**します。

-   ドライバーの定義を指定*コンテキスト*、必要に応じて、PnP マネージャーは、コールバック ルーチンに渡されます。

ドライバーを呼び出して通知の登録を削除する[ **IoUnregisterPlugPlayNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff550398)で、 *NotificationEntry*によって返される**IoRegisterPlugPlayNotification**します。

 

 





---
title: 通知の送信
description: 通知の送信
ms.assetid: 55e0f41c-e042-4170-bedd-160b6c457365
keywords:
- 通知 WDK ネイティブ 802.11 IHV Extensions DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0f5b6d471ddb1d371e654b1af25676898e7f147
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841958"
---
# <a name="sending-notifications"></a>通知の送信




 

IHV Extensions DLL は、 [**Dot11ExtSendNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_notification)関数を呼び出して、通知に登録されているサービスまたはアプリケーションに通知を送信します。 通知を受信するには、サービスまたはアプリケーションが**WlanRegisterNotification**関数を呼び出すことによって、Auto CONFIGURATION MANAGER (ACM) に登録する必要があります。 この関数の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

[**Dot11ExtSendNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_notification)関数の呼び出しを通じて通知を受信するには、サービスまたはアプリケーションが、source 値が L2\_NOTIFICATION\_SOURCE\_WLAN\_IHV の通知に登録する必要が**あり  ます**。

 

[**Dot11ExtSendNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_notification)を呼び出すと、IHV 拡張 DLL は[**L2\_通知\_データ**](https://docs.microsoft.com/windows/desktop/api/l2cmn/ns-l2cmn-_l2_notification_data)構造体へのポインターを*pnotificationdata*パラメーターに渡します。 L2\_NOTIFICATION\_データは、通知の種類を定義し、IHV 拡張 DLL への通知に関する追加データを提供できます。

 

 






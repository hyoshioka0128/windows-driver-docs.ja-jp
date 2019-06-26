---
title: 通知の送信
description: 通知の送信
ms.assetid: 55e0f41c-e042-4170-bedd-160b6c457365
keywords:
- WDK ネイティブ 802.11 IHV 拡張 DLL の通知
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfc21e7ac954406c4c7fd470ab5933ac3f2bc1da
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386837"
---
# <a name="sending-notifications"></a>通知の送信




 

IHV 拡張 DLL の呼び出し、 [ **Dot11ExtSendNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_send_notification)関数、サービスや通知に登録されているアプリケーションに通知を送信します。 通知を受信するためにサービスまたはアプリケーション登録する必要があります自動構成マネージャー (ACM) を呼び出すことによって、 **WlanRegisterNotification**関数。 この関数の詳細については、Microsoft Windows SDK のマニュアルを参照してください。

**注**  L2 の元の値を使用した通知のサービスまたはアプリケーションを登録する必要があります\_通知\_ソース\_WLAN\_IHV 経由で通知を受信するには呼び出し、 [ **Dot11ExtSendNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_send_notification)関数。

 

呼び出すときに[ **Dot11ExtSendNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_send_notification)、IHV 拡張機能の DLL へのポインターを渡す、 [ **L2\_通知\_データ**](https://docs.microsoft.com/windows/desktop/api/l2cmn/ns-l2cmn-_l2_notification_data)構造体を*pNotificationData*パラメーター。 L2\_通知\_データは、通知の種類を定義および IHV 拡張機能の DLL への通知に関する追加データを提供できます。

 

 






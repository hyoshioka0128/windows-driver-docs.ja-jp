---
title: Bluetooth プロファイル ドライバーでの SCO 接続の受け入れ
description: Bluetooth プロファイル ドライバーでの SCO 接続の受け入れ
ms.assetid: 9736f113-26fb-4e2f-9a58-9874a11f8347
keywords:
- 同期接続指向の WDK Bluetooth
- SCO プロファイル ドライバー WDK Bluetooth
- SCO の着信接続要求の WDK Bluetooth
- リモート接続通知 WDK Bluetooth
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97c38df284bd3cafea4618bf7d9f957068d222e3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364672"
---
# <a name="accepting-sco-connections-in-a-bluetooth-profile-driver"></a>Bluetooth プロファイル ドライバーでの SCO 接続の受け入れ


SCO プロファイル ドライバーには、リモート デバイスから Synchronous Connection-Oriented (SCO) 接続の要求に応答する自体を登録できます。 たとえば、コードレス テレフォニー プロファイル (CTP) デバイスの SCO プロファイル ドライバーを受け入れるか、要求を拒否して、CTP デバイスから受信 SCO 接続要求に応答します。 サーバー プロファイルのドライバーが要求を受け入れる場合、サーバー プロファイルのドライバーは、デバイスからの入力に応答し、Bluetooth ドライバー スタックには、その入力を渡します。

Server プロファイルのドライバーでは、リモートの Bluetooth デバイスからの受信の SCO 接続要求を受け入れる次の手順を実行する必要があります。

**リモート デバイスから SCO 接続要求を受信するには**

1.  プロファイルのドライバーが[をビルドし、送信](building-and-sending-a-brb.md)、 [ **BRB\_SCO\_登録\_サーバー** ](https://docs.microsoft.com/previous-versions/ff536628(v=vs.85)) の登録を要求する[ *SCO コールバック関数*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/nc-bthddi-pfnsco_indication_callback) Bluetooth ドライバー スタック、スタックが SCO 接続要求のプロファイルのドライバーに通知できます。

2.  Bluetooth ドライバー スタックは受信 SCO 接続要求を受信リモート デバイスから、呼び出し、 [ *SCO コールバック関数*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/nc-bthddi-pfnsco_indication_callback)プロファイル ドライバーによって以前に登録します。 Bluetooth ドライバー スタックは、値を渡します**ScoIndicationRemoteConnect**を*Indication*コールバック関数のパラメーター。

3.  受信接続要求に応答して、プロファイルのドライバーをビルドを送信してください、 [ **BRB\_SCO\_オープン\_チャネル\_応答**](https://docs.microsoft.com/previous-versions/ff536627(v=vs.85))要求。 値に基づいて、**応答**のメンバー、 [  **\_BRB\_SCO\_オープン\_チャネル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_sco_open_channel)構造体この要求で渡されると、サーバー プロファイルのドライバーを受け入れるか、接続要求を拒否します。

4.  Bluetooth ドライバー スタックが呼び出すことができますし、サーバー プロファイルのドライバーが接続を受け入れる場合、 [ *SCO コールバック関数*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/nc-bthddi-pfnsco_indication_callback)で指定されている、**コールバック**のメンバー、[  **\_BRB\_SCO\_オープン\_チャネル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_sco_open_channel) SCO 接続への変更のサーバーのプロファイルのドライバーに通知する構造体。

プロファイル ドライバーが接続要求を受け入れた後、新しく確立された SCO 接続経由でデータを送受信するその他の BRBs を使用できます。

SCO 接続のリモート デバイスの通知の受信を停止すると、プロファイルのドライバーが[をビルドし、送信](building-and-sending-a-brb.md)、 [ **BRB\_SCO\_登録解除\_サーバー** ](https://docs.microsoft.com/previous-versions/ff536630(v=vs.85))プロファイル ドライバーが処理するときに、サーバーの登録を解除する要求[ **IRP\_MN\_削除\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)プラグ アンド プレイでは、通知を削除します。

通知とコールバック関数の詳細については、次を参照してください。 [Bluetooth イベント通知のサポート](supporting-bluetooth-event-notifications.md)します。

 

 






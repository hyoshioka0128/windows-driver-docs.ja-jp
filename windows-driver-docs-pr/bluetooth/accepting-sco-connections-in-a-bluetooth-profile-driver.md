---
title: Bluetooth プロファイル ドライバーでの SCO 接続の受け入れ
description: Bluetooth プロファイル ドライバーでの SCO 接続の受け入れ
ms.assetid: 9736f113-26fb-4e2f-9a58-9874a11f8347
keywords:
- 同期接続指向 WDK Bluetooth
- SCO プロファイルドライバー WDK Bluetooth
- 受信 SCO 接続要求 WDK Bluetooth
- リモート接続の通知 WDK Bluetooth
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8433b71dee982cab1d93a8f56ea9e0469776e7b9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833899"
---
# <a name="accepting-sco-connections-in-a-bluetooth-profile-driver"></a>Bluetooth プロファイル ドライバーでの SCO 接続の受け入れ


SCO プロファイルドライバーは、リモートデバイスからの受信同期接続指向 (SCO) 接続要求に応答するように自身を登録できます。 たとえば、コードレステレフォニープロファイル (CTP) デバイスの SCO プロファイルドライバーは、要求を受け入れるか拒否するかを、CTP デバイスからの入力 SCO 接続要求に応答します。 サーバープロファイルドライバーが要求を受け入れる場合、サーバープロファイルドライバーは、デバイスからの入力に応答し、その入力を Bluetooth ドライバースタックに渡します。

サーバープロファイルドライバーは、次の手順を実行して、リモート Bluetooth デバイスからの入力 SCO 接続要求を受け入れる必要があります。

**リモートデバイスからの受信 SCO 接続要求を受信するには**

1.  プロファイルドライバーは、 [**Brb\_sco\_** ](https://docs.microsoft.com/previous-versions/ff536628(v=vs.85))を[作成して送信](building-and-sending-a-brb.md)する必要があります。\_サーバー要求を登録して、 [*Sco コールバック関数*](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnsco_indication_callback)を Bluetooth ドライバースタックに登録し、スタックが受信 sco のプロファイルドライバーに通知できるようにします。接続要求。

2.  Bluetooth ドライバースタックは、リモートデバイスから受信 SCO 接続要求を受信すると、プロファイルドライバーによって以前に登録された[*Sco コールバック関数*](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnsco_indication_callback)を呼び出します。 Bluetooth ドライバースタックは、コールバック関数の表示*パラメーターに* **ScoIndicationRemoteConnect**値を渡します。

3.  着信接続要求に応答するには、プロファイルドライバーが[**Brb\_SCO\_オープン\_チャネル\_応答**](https://docs.microsoft.com/previous-versions/ff536627(v=vs.85))要求を作成して送信する必要があります。 この要求で渡された[ **\_BRB\_SCO\_オープン\_チャネル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_open_channel)構造の**応答**メンバーの値に基づいて、サーバープロファイルドライバーは接続要求を受け入れたり拒否したりします。

4.  サーバープロファイルドライバーが接続を受け入れると、Bluetooth ドライバースタックは、 [ **\_BRB\_sco\_オープン\_チャネル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_open_channel)構造の**コールバック**メンバーで指定されている[*sco コールバック関数*](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnsco_indication_callback)を呼び出すことができます。SCO 接続に対する変更をサーバープロファイルドライバーに通知する。

プロファイルドライバーは接続要求を受け入れると、他の BRBs を使用して、新しく確立された SCO 接続でデータを送受信できます。

リモートデバイスの SCO 接続試行の通知を受信しないようにするには、プロファイルドライバーで[**Brb\_SCO**](https://docs.microsoft.com/previous-versions/ff536630(v=vs.85))を[構築して送信](building-and-sending-a-brb.md)する必要があります。これにより、プロファイルドライバーが[**IRP\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)を処理し\_\_デバイスを削除しプラグアンドプレイ通知を削除するときにサーバーの登録を解除\_\_ます。

通知とコールバック関数の詳細については、「 [Bluetooth イベント通知のサポート](supporting-bluetooth-event-notifications.md)」を参照してください。

 

 






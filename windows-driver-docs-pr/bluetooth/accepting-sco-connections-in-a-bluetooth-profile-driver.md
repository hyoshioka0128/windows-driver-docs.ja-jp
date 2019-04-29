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
ms.openlocfilehash: 8637ca3f86556e94a1cc8b047abc01fdc9e5f925
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328345"
---
# <a name="accepting-sco-connections-in-a-bluetooth-profile-driver"></a>Bluetooth プロファイル ドライバーでの SCO 接続の受け入れ


SCO プロファイル ドライバーには、リモート デバイスから Synchronous Connection-Oriented (SCO) 接続の要求に応答する自体を登録できます。 たとえば、コードレス テレフォニー プロファイル (CTP) デバイスの SCO プロファイル ドライバーを受け入れるか、要求を拒否して、CTP デバイスから受信 SCO 接続要求に応答します。 サーバー プロファイルのドライバーが要求を受け入れる場合、サーバー プロファイルのドライバーは、デバイスからの入力に応答し、Bluetooth ドライバー スタックには、その入力を渡します。

Server プロファイルのドライバーでは、リモートの Bluetooth デバイスからの受信の SCO 接続要求を受け入れる次の手順を実行する必要があります。

**リモート デバイスから SCO 接続要求を受信するには**

1.  プロファイルのドライバーが[をビルドし、送信](building-and-sending-a-brb.md)、 [ **BRB\_SCO\_登録\_サーバー** ](https://msdn.microsoft.com/library/windows/hardware/ff536628) の登録を要求する[ *SCO コールバック関数*](https://msdn.microsoft.com/library/windows/hardware/ff536772) Bluetooth ドライバー スタック、スタックが SCO 接続要求のプロファイルのドライバーに通知できます。

2.  Bluetooth ドライバー スタックは受信 SCO 接続要求を受信リモート デバイスから、呼び出し、 [ *SCO コールバック関数*](https://msdn.microsoft.com/library/windows/hardware/ff536772)プロファイル ドライバーによって以前に登録します。 Bluetooth ドライバー スタックは、値を渡します**ScoIndicationRemoteConnect**を*Indication*コールバック関数のパラメーター。

3.  受信接続要求に応答して、プロファイルのドライバーをビルドを送信してください、 [ **BRB\_SCO\_オープン\_チャネル\_応答**](https://msdn.microsoft.com/library/windows/hardware/ff536627)要求。 値に基づいて、**応答**のメンバー、 [  **\_BRB\_SCO\_オープン\_チャネル**](https://msdn.microsoft.com/library/windows/hardware/ff536870)構造体この要求で渡されると、サーバー プロファイルのドライバーを受け入れるか、接続要求を拒否します。

4.  Bluetooth ドライバー スタックが呼び出すことができますし、サーバー プロファイルのドライバーが接続を受け入れる場合、 [ *SCO コールバック関数*](https://msdn.microsoft.com/library/windows/hardware/ff536772)で指定されている、**コールバック**のメンバー、[  **\_BRB\_SCO\_オープン\_チャネル**](https://msdn.microsoft.com/library/windows/hardware/ff536870) SCO 接続への変更のサーバーのプロファイルのドライバーに通知する構造体。

プロファイル ドライバーが接続要求を受け入れた後、新しく確立された SCO 接続経由でデータを送受信するその他の BRBs を使用できます。

SCO 接続のリモート デバイスの通知の受信を停止すると、プロファイルのドライバーが[をビルドし、送信](building-and-sending-a-brb.md)、 [ **BRB\_SCO\_登録解除\_サーバー** ](https://msdn.microsoft.com/library/windows/hardware/ff536630)プロファイル ドライバーが処理するときに、サーバーの登録を解除する要求[ **IRP\_MN\_削除\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551738)プラグ アンド プレイでは、通知を削除します。

通知とコールバック関数の詳細については、次を参照してください。 [Bluetooth イベント通知のサポート](supporting-bluetooth-event-notifications.md)します。

 

 






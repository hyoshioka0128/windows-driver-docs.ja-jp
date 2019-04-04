---
title: ドライバーで Bluetooth プロファイル L2CAP 接続の受け入れ
description: ドライバーで Bluetooth プロファイル L2CAP 接続の受け入れ
ms.assetid: 26a8238d-717a-438f-84d0-047ce9618928
keywords:
- L2CAP プロファイル ドライバー WDK Bluetooth
- 論理リンク コント ローラーとプロトコルの適応 WDK Bluetooth
- 着信 L2CAP 接続要求が WDK Bluetooth
- WDK の Bluetooth の接続
- リモート接続通知 WDK Bluetooth
- WDK の Bluetooth の通知
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 358c02116c2bbae1a35a543e0ef8a9f35fe816b9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553122"
---
# <a name="accepting-l2cap-connections-in-a-bluetooth-profile-driver"></a>ドライバーで Bluetooth プロファイル L2CAP 接続の受け入れ


L2CAP サーバー プロファイル ドライバーは、リモート デバイスからの受信の論理リンク コントロールと適応プロトコル (L2CAP) 接続要求に応答します。 たとえば、PDA の L2CAP サーバー プロファイル ドライバーに PDA から受信接続要求に応答。

**L2CAP 接続要求を受信するには**

1.  **着信 L2CAP 接続要求を受信する*任意*特定 PSM 用のリモート デバイス**、プロファイルのドライバーはまず必要があります[をビルドし、送信](building-and-sending-a-brb.md)、 [ **BRB\_L2CA\_登録\_SERVER** ](https://msdn.microsoft.com/library/windows/hardware/ff536618)要求を指定する**NULL**で、 **BtAddress**メンバーと 0 で、**Psm**の要求のメンバー \_BRB\_L2CA\_登録\_サーバー構造体。 プロファイルのドライバーを登録する必要がありますも、 [ *L2CAP コールバック関数*](https://msdn.microsoft.com/library/windows/hardware/ff536755) Bluetooth ドライバー スタックに送信するときに、 **BRB\_L2CA\_レジスタ\_SERVER**要求。 これにより、Bluetooth ドライバー スタック L2CAP 接続要求のプロファイルのドライバーに通知します。

    次に、プロファイルのドライバーが必要があります[をビルドし、送信](building-and-sending-a-brb.md)、 [ **BRB\_登録\_PSM** ](https://msdn.microsoft.com/library/windows/hardware/ff536621) Bluetooth ドライバー スタックはそのまま使用するための要求要求によって登録された PSM から接続します。 Bluetooth ドライバー スタックが不明 (未登録) があるすべての接続要求を拒否する場合は、接続要求。 PSMs の詳細については、次を参照してください。、 [  **\_BRB\_PSM** ](https://msdn.microsoft.com/library/windows/hardware/ff536865)構造体。

2.  **着信 L2CAP 接続要求を受信する、*特定*リモート デバイス/PSM ペア**、プロファイルのドライバーにする必要があります[をビルドし、送信](building-and-sending-a-brb.md)、 [ **BRB\_L2CA\_登録\_SERVER** ](https://msdn.microsoft.com/library/windows/hardware/ff536618)でリモート デバイスのアドレスを指定する要求、 **BtAddress**メンバー、および PSM、 **Psm**要求のメンバーに付属の\_BRB\_L2CA\_登録\_サーバー構造体。 プロファイルのドライバーを登録する必要がありますも、 [ *L2CAP コールバック関数*](https://msdn.microsoft.com/library/windows/hardware/ff536755) Bluetooth ドライバー スタックに送信するときに、 **BRB\_L2CA\_レジスタ\_SERVER**要求。 これにより、Bluetooth ドライバー スタック L2CAP 接続要求のプロファイルのドライバーに通知します。

3.  プロファイルのドライバーを発行する必要があります、 [ **IOCTL\_両方\_SDP\_送信\_レコード**](https://msdn.microsoft.com/library/windows/hardware/ff536693)します。 プロファイルのドライバーは、リモート システムは、SDP を使用して、新しいサービスを検出できるようにプロファイルのドライバーがサポートするサービスを記述した SDP レコードを登録できます。

4.  Bluetooth ドライバー スタックは、リモート デバイスから受信 L2CAP 接続要求を受け取り、Bluetooth ドライバー スタックが呼び出し、 [ *L2CAP コールバック関数*](https://msdn.microsoft.com/library/windows/hardware/ff536755)プロファイルによって以前に登録ドライバー。 Bluetooth ドライバー スタックは、値を渡します**IndicationRemoteConnect**を*Indication*コールバック関数のパラメーター。

5.  受信接続要求に応答して、プロファイルのドライバーがする必要があります[をビルドし、送信](building-and-sending-a-brb.md)、 [ **BRB\_L2CA\_オープン\_チャネル\_応答**](https://msdn.microsoft.com/library/windows/hardware/ff536616)要求。 サーバー プロファイルのドライバーに Bluetooth ドライバー スタックから渡された値を使用して、*パラメーター*リモート デバイスと接続の設定をネゴシエートするコールバック関数のパラメーター。 値に基づいて、**応答**のメンバー、 [  **\_BRB\_L2CA\_オープン\_チャネル**](https://msdn.microsoft.com/library/windows/hardware/ff536860)構造体この要求で渡されると、サーバー プロファイルのドライバーを受け入れるか、接続要求を拒否します。

6.  Bluetooth ドライバー スタックが呼び出すことができますし、サーバー プロファイルのドライバーが接続を受け入れる場合、 [ *L2CAP コールバック関数*](https://msdn.microsoft.com/library/windows/hardware/ff536755)で指定されている、**コールバック**のメンバー、[  **\_BRB\_L2CA\_オープン\_チャネル**](https://msdn.microsoft.com/library/windows/hardware/ff536860)構造体。 Bluetooth ドライバー スタックは、この関数を使用して、L2CAP 接続への変更のサーバーのプロファイルのドライバーに通知します。

**注:**  
-   1 つのプロファイルのドライバーが複数の L2CAP 接続要求の受信に登録できますを構築し、複数の送信の異なるリモート デバイス/PSM ペア**BRB\_L2CA\_登録\_SERVER** PSM のペアと一意のリモート デバイスのアドレスを指定する、複数の L2CAP サーバーを登録する要求、 **BtAddress**と**Psm**要求のメンバー。

-   1 つのプロファイルのドライバーがからの着信 L2CAP 接続要求を受信登録できます*任意*特定の 2.1.X 用のリモート デバイス、複数の異なるリモート デバイス/PSM ペアから L2CAP 接続要求が受信した受信も、任意のリモート デバイスからの特定の 2.1.X L2CAP 接続要求を受信する最初の登録し登録することで特定のリモートから L2CAP 接続要求を受信するデバイス/PSM ペアに登録されている特定の PSM 限り最初の手順がもう一度登録されていません。

-   任意のリモート デバイスから同じ PSM L2CAP 接続要求を受信する複数のプロファイルのドライバーを登録できません。 Bluetooth ドライバー スタックは、任意のリモート デバイスから特定 PSM L2CAP 接続要求を受信する 1 つのプロファイル ドライバーのみを許可します。

 

プロファイル ドライバーが接続要求を受け入れた後、新しく確立された L2CAP 接続経由でデータを送受信するその他の BRBs を使用できます。

リモート デバイス L2CAP 接続試行の通知の受信を停止するプロファイルのドライバーがする必要があります[をビルドし、送信](building-and-sending-a-brb.md)、 [ **BRB\_L2CA\_登録解除\_SERVER** ](https://msdn.microsoft.com/library/windows/hardware/ff536619)プロファイル ドライバーが処理するときに、サーバーの登録を解除する要求[ **IRP\_MN\_削除\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551738)プラグ アンド プレイが通知を削除します。

通知とコールバック関数の詳細については、[Bluetooth イベント通知のサポート](supporting-bluetooth-event-notifications.md)を参照してください。

 

 






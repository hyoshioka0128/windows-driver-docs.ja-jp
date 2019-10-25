---
title: Bluetooth プロファイル ドライバーでの L2CAP 接続の受け入れ
description: Bluetooth プロファイル ドライバーでの L2CAP 接続の受け入れ
ms.assetid: 26a8238d-717a-438f-84d0-047ce9618928
keywords:
- L2CAP プロファイルドライバー WDK Bluetooth
- 論理リンクコントローラーとアダプテーションプロトコル WDK Bluetooth
- 受信 L2CAP 接続要求 WDK Bluetooth
- 接続 WDK Bluetooth
- リモート接続の通知 WDK Bluetooth
- 通知 WDK Bluetooth
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd7a85e4f601a78181d1b11414291df4c4288bfa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833901"
---
# <a name="accepting-l2cap-connections-in-a-bluetooth-profile-driver"></a>Bluetooth プロファイル ドライバーでの L2CAP 接続の受け入れ


L2CAP サーバープロファイルドライバーは、リモートデバイスからの受信論理リンク制御とアダプテーションプロトコル (L2CAP) 接続要求に応答します。 たとえば、PDA の L2CAP server プロファイルドライバーは、PDA からの着信接続要求に応答します。

**受信 L2CAP 接続要求を受信するには**

1.  **特定の PSM のリモートデバイスから着信 L2CAP 接続要求を受信するに**は、まずプロファイルドライバーが\_L2CA を[作成して\_送信し](building-and-sending-a-brb.md)、 [ **\_サーバー**](https://docs.microsoft.com/previous-versions/ff536618(v=vs.85))要求を登録して、NULL を指定する必要があります。要求の \_BRB\_L2CA の**btaddress** **メンバーと**0 にある\_\_サーバー構造に登録します。 また、プロファイルドライバーは、 **Brb\_L2CA**を送信するときに[*L2CAP コールバック関数*](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnbthport_indication_callback)を Bluetooth ドライバースタックに登録し、\_サーバー要求を登録\_必要があります。 これにより、Bluetooth ドライバースタックは、受信 L2CAP 接続要求のプロファイルドライバーに通知できます。

    次に、プロファイルドライバーは、Brb を[ビルドして送信し](building-and-sending-a-brb.md) [ **\_\_PSM**](https://docs.microsoft.com/previous-versions/ff536621(v=vs.85))要求に登録します。これにより、Bluetooth ドライバースタックは、要求によって登録された psm からの接続を受け入れるようになります。 それ以外の場合、Bluetooth ドライバースタックは、不明な (未登録) 接続要求を持つすべての接続要求を拒否します。 PSMs の詳細については、 [ **\_BRB\_PSM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_psm)の構造を参照してください。

2.  ***特定*のリモートデバイス/PSM ペアから着信 L2CAP 接続要求を受信するに**は、プロファイルドライバーが\_L2CA を[作成して\_送信](building-and-sending-a-brb.md)する必要があります。 [ **\_サーバー**](https://docs.microsoft.com/previous-versions/ff536618(v=vs.85))要求を登録し、リモートデバイスを指定して、**btaddress**メンバーのアドレス、および**PSM**メンバーの psm に付随する \_brb\_L2CA\_REGISTER\_サーバー構造に登録します。 また、プロファイルドライバーは、 **Brb\_L2CA**を送信するときに[*L2CAP コールバック関数*](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnbthport_indication_callback)を Bluetooth ドライバースタックに登録し、\_サーバー要求を登録\_必要があります。 これにより、Bluetooth ドライバースタックは、受信 L2CAP 接続要求のプロファイルドライバーに通知できます。

3.  プロファイルドライバーは、 [**IOCTL\_BTH\_SDP\_送信\_レコード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_submit_record)を発行する必要があります。 プロファイルドライバーは、プロファイルドライバーがサポートするサービスを説明する SDP レコードを登録できます。これにより、リモートシステムが SDP を使用して新しいサービスを検出できるようになります。

4.  Bluetooth ドライバースタックは、リモートデバイスから受信 L2CAP 接続要求を受信すると、プロファイルドライバーによって以前に登録された[*L2CAP コールバック関数*](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnbthport_indication_callback)を呼び出します。 Bluetooth ドライバースタックは、コールバック関数の表示*パラメーターに* **IndicationRemoteConnect**値を渡します。

5.  着信接続要求に応答するには、プロファイルドライバーは Brb\_L2CA を[ビルドして送信し](building-and-sending-a-brb.md) [ **\_\_チャネル\_応答**](https://docs.microsoft.com/previous-versions/ff536616(v=vs.85))要求を開く必要があります。 サーバープロファイルドライバーは、コールバック関数の*Parameters*パラメーターにある Bluetooth ドライバースタックから渡された値を使用して、接続設定をリモートデバイスとネゴシエートします。 この要求で渡された[ **\_BRB\_L2CA\_オープン\_チャネル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_open_channel)構造の**応答**メンバーの値に基づいて、サーバープロファイルドライバーは接続要求を受け入れたり拒否したりします。

6.  サーバープロファイルドライバーが接続を受け入れると、Bluetooth ドライバースタックは[ **\_BRB\_L2CA\_OPEN\_CHANNEL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_open_channel)の**コールバック**メンバーで指定されているように、 [*L2CAP callback 関数*](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnbthport_indication_callback)を呼び出すことができます。データ. Bluetooth ドライバースタックは、この関数を使用して、L2CAP 接続に対する変更をサーバープロファイルドライバーに通知します。

**注:**  
-   1つのプロファイルドライバーは、複数の**Brb\_\_\_L2CA**を作成して送信することによって、複数の異なるリモートデバイス/PSM ペアから着信 L2CAP 接続要求を受信するように登録できます。L2CAP サーバー。 **Btaddress**と psm members に一意のリモートデバイスアドレスと psm ペアを**指定します**。

-   1つのプロファイルドライバーは、特定の PSM のリモートデバイス*から着信*L2CAP 接続要求を受信するように登録できます。また、最初に登録して、複数の異なるリモートデバイス/PSM ペアから着信 L2CAP 接続要求を受信することもできます。特定の psm のリモートデバイスから着信 L2CAP 接続要求を受信し、最初の手順で登録されている特定の PSM が特定のリモートデバイス/PSM ペアから受信 L2CAP 接続要求を受信するように登録するには再登録されました。

-   複数のプロファイルドライバーが、同じ PSM のリモートデバイスから着信 L2CAP 接続要求を受信するように登録することはできません。 Bluetooth ドライバースタックでは、特定の PSM のリモートデバイスから着信 L2CAP 接続要求を受信するプロファイルドライバーが1つだけ許可されます。

 

プロファイルドライバーは接続要求を受け入れると、他の BRBs を使用して、新しく確立された L2CAP 接続でデータの送受信を行うことができます。

リモートデバイス L2CAP 接続試行の通知の受信を停止するには、プロファイルドライバが\_サーバーの要求の登録を解除し、プロファイルドライバが処理されたときにサーバーの登録を解除するために、 [**Brb\_\_L2CA**](https://docs.microsoft.com/previous-versions/ff536619(v=vs.85))を[作成して送信](building-and-sending-a-brb.md)する必要があります。[**IRP\_\_\_デバイスの削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)プラグアンドプレイの通知を削除します。

通知とコールバック関数の詳細については、「 [Bluetooth イベント通知のサポート](supporting-bluetooth-event-notifications.md)」を参照してください。

 

 






---
title: パケット データ サービスのハンドオフ
description: パケット データ サービスのハンドオフ
ms.assetid: 33cb68ac-42db-4bb0-8855-a8575e6e6331
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f846c3fd269132c891b4a99592642ddc8fd662a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376427"
---
# <a name="packet-data-service-handoffs"></a>パケット データ サービスのハンドオフ


次の図は、ミニポート ドライバーがパケット サービス GPRS、EDGE、UMTS、HSDPA、TD SCDMA など、さまざまな GSM ベースのテクノロジとの間を移動または EV DO、1 xrtt など、さまざまな CDMA ベースのテクノロジの間で移動ときに従う必要のある手順を示しています。または、EV DO RevA します。 太字のラベルは、OID 識別子またはトランザクションのフロー制御を通常のテキストに表示されるラベル OID 構造内で重要なフラグ。

![ミニポート ドライバーがパケット サービスは、gsm ベースのさまざまなテクノロジの間で移動したときに従う必要のある手順を示す図](images/wwanpacketdataservicehandoff.png)

ハンドオフ プロセスで、IP アドレスを変更しない限り MB サービスを処理するハンドオフ イベント透過的に、既存の接続を中断せずに注意します。 ただし、ミニポート ドライバーする必要がありますも MB サービスについて通知メディアは、IP アドレスが変更された場合のみ、イベントを切断します。

ミニポート ドライバーと管理 MB デバイスは MB サービスおよびその他のオーバーレイする側のアプリケーションに影響を最小限に自動的には、異なるエア インターフェイス間のレイヤー 2 のハンドオフを処理できる必要があります。 可能な唯一の影響は、テクノロジ ハンドオフからなる可能性がある IP アドレスに変更します。 ここでは、ミニポート ドライバーでは、パケットのサービスの変更を MB サービスに報告する前に MB 接続を再確立する必要があります。 DHCP の機能を実装しませんミニポート ドライバーを使用する必要があります、 [IP ヘルパー](ip-helper.md)と関連付けられた[関数](https://docs.microsoft.com/windows-hardware/drivers/network/ip-helper)します。 次の図に示すように DHCP の機能を実装してミニポート ドライバーでは、IP ヘルパー関数を使用する必要はありません。

パケット データ サービスをすぐには、次の手順を使用します。

1.  ミニポート ドライバー送信[ **NDIS\_状態\_WWAN\_パケット\_サービス**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-packet-service) MB サービスにします。

2.  ミニポート ドライバー送信 NDIS\_WWAN\_リンク\_MB サービスの状態。

3.  ミニポート ドライバー送信[ **NDIS\_状態\_WWAN\_パケット\_サービス**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-packet-service) MB サービスにします。

4.  ミニポート ドライバーの呼び出し、 [ **DeleteUnicastIpAddressEntry** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546370(v=vs.85))ヘルパー関数と古い IP アドレス

5.  ミニポート ドライバーの呼び出し、 [ **CreateUnicastIpAddressEntry** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546227(v=vs.85))ヘルパー関数と、新しい IP アドレス

6.  ミニポート ドライバー送信[ **NDIS\_状態\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state) MB サービスにします。

7.  ミニポート ドライバー送信[ **NDIS\_状態\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state) MB サービスにします。

8.  ミニポート ドライバー送信[ **NDIS\_状態\_WWAN\_パケット\_サービス**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-packet-service) MB サービスにします。

 

 






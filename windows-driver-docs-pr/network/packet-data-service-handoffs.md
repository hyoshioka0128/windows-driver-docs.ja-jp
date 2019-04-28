---
title: パケット データ サービスのハンドオフ
description: パケット データ サービスのハンドオフ
ms.assetid: 33cb68ac-42db-4bb0-8855-a8575e6e6331
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 336d0a23441ce5cd7f6983b98661548bc8c90d62
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363666"
---
# <a name="packet-data-service-handoffs"></a>パケット データ サービスのハンドオフ


次の図は、ミニポート ドライバーがパケット サービス GPRS、EDGE、UMTS、HSDPA、TD SCDMA など、さまざまな GSM ベースのテクノロジとの間を移動または EV DO、1 xrtt など、さまざまな CDMA ベースのテクノロジの間で移動ときに従う必要のある手順を示しています。または、EV DO RevA します。 太字のラベルは、OID 識別子またはトランザクションのフロー制御を通常のテキストに表示されるラベル OID 構造内で重要なフラグ。

![ミニポート ドライバーがパケット サービスは、gsm ベースのさまざまなテクノロジの間で移動したときに従う必要のある手順を示す図](images/wwanpacketdataservicehandoff.png)

ハンドオフ プロセスで、IP アドレスを変更しない限り MB サービスを処理するハンドオフ イベント透過的に、既存の接続を中断せずに注意します。 ただし、ミニポート ドライバーする必要がありますも MB サービスについて通知メディアは、IP アドレスが変更された場合のみ、イベントを切断します。

ミニポート ドライバーと管理 MB デバイスは MB サービスおよびその他のオーバーレイする側のアプリケーションに影響を最小限に自動的には、異なるエア インターフェイス間のレイヤー 2 のハンドオフを処理できる必要があります。 可能な唯一の影響は、テクノロジ ハンドオフからなる可能性がある IP アドレスに変更します。 ここでは、ミニポート ドライバーでは、パケットのサービスの変更を MB サービスに報告する前に MB 接続を再確立する必要があります。 DHCP の機能を実装しませんミニポート ドライバーを使用する必要があります、 [IP ヘルパー](ip-helper.md)と関連付けられた[関数](https://msdn.microsoft.com/library/windows/hardware/ff557018)します。 次の図に示すように DHCP の機能を実装してミニポート ドライバーでは、IP ヘルパー関数を使用する必要はありません。

パケット データ サービスをすぐには、次の手順を使用します。

1.  ミニポート ドライバー送信[ **NDIS\_状態\_WWAN\_パケット\_サービス**](https://msdn.microsoft.com/library/windows/hardware/ff567850) MB サービスにします。

2.  ミニポート ドライバー送信 NDIS\_WWAN\_リンク\_MB サービスの状態。

3.  ミニポート ドライバー送信[ **NDIS\_状態\_WWAN\_パケット\_サービス**](https://msdn.microsoft.com/library/windows/hardware/ff567850) MB サービスにします。

4.  ミニポート ドライバーの呼び出し、 [ **DeleteUnicastIpAddressEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff546370)ヘルパー関数と古い IP アドレス

5.  ミニポート ドライバーの呼び出し、 [ **CreateUnicastIpAddressEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff546227)ヘルパー関数と、新しい IP アドレス

6.  ミニポート ドライバー送信[ **NDIS\_状態\_リンク\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567391) MB サービスにします。

7.  ミニポート ドライバー送信[ **NDIS\_状態\_リンク\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567391) MB サービスにします。

8.  ミニポート ドライバー送信[ **NDIS\_状態\_WWAN\_パケット\_サービス**](https://msdn.microsoft.com/library/windows/hardware/ff567850) MB サービスにします。

 

 






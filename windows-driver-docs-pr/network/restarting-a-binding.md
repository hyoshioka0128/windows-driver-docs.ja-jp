---
title: バインドの再起動
description: バインドの再起動
ms.assetid: 5abec927-cb73-4b02-b977-c4f45bd37c42
keywords:
- プロトコルドライバー WDK ネットワーク、バインドの再起動
- NDIS プロトコルドライバー WDK、バインドの再起動
- バインドが WDK ネットワークを再起動します
- バインドの状態 WDK ネットワーク
- プロトコルドライバーのバインドを再開しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0edc77afea74d696c0fe4c03593d585125badd8c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842016"
---
# <a name="restarting-a-binding"></a>バインドの再起動





停止しているバインドを再起動するには、NDIS によって protocol driver a network プラグアンドプレイ (PnP) restart イベント通知が送信されます。 プロトコルドライバーによって再起動通知が受信されると、影響を受けるバインドは再起動状態になります。

再起動通知を送信するために、NDIS はプロトコルドライバーの[*ProtocolNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event)関数を呼び出します。 NDIS が*ProtocolNetPnPEvent*に渡す[**NET\_PNP\_イベント\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event_notification)構造は、 **Netevent**メンバーでは**NetEventRestart**を指定し、 **Buffer**メンバーにはへのポインターが含まれています。[**NDIS\_プロトコル\_\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_protocol_restart_parameters)構造体を再起動します。 Ndis は、ndis\_プロトコルの**RestartAttributes**メンバー内にある[**ndis\_restart\_ATTRIBUTES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_restart_attributes)構造体へのポインターを提供し、\_PARAMETERS 構造体を再起動\_ます。

バインドが一時停止されている間、NDIS はドライバースタックを再構成**することができ  ます**。 新しいスタック構成では、基になるアダプターに対して異なる機能セットをサポートできます。 これらの新機能は、プロトコルドライバーがバインディングで通信する方法に影響を与える可能性があります。

 

プロトコルドライバーは、不要な OID 要求を避けるために、NDIS\_プロトコルの情報を使用して[ **\_パラメーター構造\_再起動**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_protocol_restart_parameters)する必要があります。

再起動状態では、プロトコルドライバーは次のことが可能です。

-   OID 要求を使用して、ドライバースタックを照会します。 たとえば、このドライバーでは、 [OID\_GEN\_receive\_SCALE\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-receive-scale-capabilities)を使用して、receive side scaling のサポートについて調べることができます。

-   必要に応じて、 [**net\_buffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)と[**net\_buffer\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)プールを再割り当てします。

-   基になるフィルターモジュールの一覧を列挙します。

-   OID 要求を使用して、新しいアダプターの機能を明らかにします。

ドライバーは、バインドの送信および受信操作を再開する準備が整うと、実行中の状態になります。

 

 






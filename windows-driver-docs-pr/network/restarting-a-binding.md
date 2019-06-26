---
title: バインドの再起動
description: バインドの再起動
ms.assetid: 5abec927-cb73-4b02-b977-c4f45bd37c42
keywords:
- プロトコル ドライバー WDK ネットワークは、再起動のバインド
- NDIS プロトコル ドライバー WDK、バインドの再起動
- バインディングは、WDK のネットワークを再起動します。
- バインドは、WDK ネットワークを状態します。
- プロトコル ドライバーのバインドを再起動します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc2ccb56fa55421fc27eaec1f6e7fb0b2cf39695
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384707"
---
# <a name="restarting-a-binding"></a>バインドの再起動





一時停止されているバインディングを再起動する NDIS 送信プロトコル ドライバー ネットワーク プラグしプレイ (PnP) イベント通知を再起動します。 プロトコル ドライバーでは、再起動の通知を受け取た後、影響を受けるバインドは再開中状態になります。

NDIS を再起動通知を送信するには、呼び出しのプロトコル ドライバーの[ *ProtocolNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_net_pnp_event)関数。 [ **NET\_PNP\_イベント\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_pnp_event_notification) NDIS からに渡される構造*ProtocolNetPnPEvent* を指定します**NetEventRestart**で、 **NetEvent**メンバーおよび**バッファー**メンバーにはへのポインターが含まれています、 [ **NDIS\_プロトコル\_再起動\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_protocol_restart_parameters)構造体。 NDIS へのポインターを提供する、 [ **NDIS\_再起動\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_restart_attributes)構造体、 **RestartAttributes**の NDISメンバー\_プロトコル\_再起動\_パラメーター構造体。

**注**  NDIS ドライバー スタックの再構成が、バインドが一時停止中にします。 新しいスタック構成は、基になるアダプターに対して、異なる一連の機能をサポートできます。 これらの新機能、バインディング プロトコル ドライバーが通信する方法に影響を与えることができます。

 

プロトコル ドライバーに情報を使用する必要があります、 [ **NDIS\_プロトコル\_再起動\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_protocol_restart_parameters)不要な OID を回避するために構造体を要求します。

再起動の状態にプロトコル ドライバーでは次のことができます。

-   クエリ ドライバー スタックへの要求の OID を使用します。 たとえば、ドライバーについて確認できますサポートの受信側のスケーリングを使用して[OID\_GEN\_受信\_スケール\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-receive-scale-capabilities)します。

-   再割り当て[ **NET\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)と[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)プールのために必要な場合。

-   基になるフィルター モジュールの一覧を列挙します。

-   新しいアダプターの機能を表示するには、OID の要求を使用します。

バインディング、ドライバーの送信を再開およびバインディングの操作を受信する準備が実行中の状態が入力されます。

 

 






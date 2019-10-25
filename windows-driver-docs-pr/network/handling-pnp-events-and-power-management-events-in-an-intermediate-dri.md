---
title: 中間ドライバーでの PnP イベントおよび電源管理イベントの処理
description: 中間ドライバーでの PnP イベントおよび電源管理イベントの処理
ms.assetid: 0b4cf76f-a31d-4cf6-8486-090393404af9
keywords:
- 中間ドライバー WDK ネットワーク、イベント
- NDIS 中間ドライバー WDK、イベント
- WDK ネットワーク、中間ドライバープラグアンドプレイ
- 電源管理 WDK ネットワーク、中間ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 658751fc4ec636c06361601ffe9305e0569a1d1c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842567"
---
# <a name="handling-pnp-events-and-power-management-events-in-an-intermediate-driver"></a>中間ドライバーでの PnP イベントおよび電源管理イベントの処理





中間ドライバーは、プラグアンドプレイ (PnP) イベントと電源管理イベントを処理できる必要があります。 具体的には、次のとおりです。

-   中間ドライバーでは、ndis\_ミニポート\_アダプターの**Attributeflags**メンバーの\_SUSPEND フラグに\_停止\_\_、NDIS\_ミニポート\_属性を設定する必要があり[ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes) [**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)に渡される登録\_ATTRIBUTES 構造体。 詳細については、「を[ミニポートとして初期化する](initializing-virtual-miniports.md)」を参照してください。

-   中間ドライバーの仮想ミニポートは、OID\_PNP\_*Xxx*要求を処理する必要があります。

-   中間ドライバーのプロトコルセクションは、適切な OID\_PNP\_*Xxx*要求を、基になるミニポートドライバーに伝達する必要があります。 中間ドライバーの仮想ミニポートは、基になるミニポートドライバーの応答を、要求を発信したプロトコルドライバーに渡す必要があります。 中間ドライバーは、設計に必要のない要求を渡す必要はありません。 たとえば、負荷分散フェールオーバー (LBFO) アプリケーションと同様に、仮想ミニポートと基になるミニポートアダプターとの間に一対一のリレーションシップが存在しない場合です。

-   中間ドライバーのプロトコル部分では、 [*ProtocolNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event)関数を指定する必要があります。

中間ドライバープロトコルとミニポートイベントハンドラーは、特定の順序では呼び出されません。 中間ドライバーのイベントハンドラーは、それに応じて実装する必要があります。

ここでは、次のトピックについて説明します。

[PnP および電源管理イベントを処理するための中間ドライバーの初期化](initializing-intermediate-drivers-to-handle-pnp-and-power-management-events.md)

[OID\_PNP\_Xxx クエリとセットの処理](handling-oid-pnp-xxx-queries-and-sets.md)

[中間ドライバーでの ProtocolNetPnPEvent ハンドラーの実装](implementing-a-protocolnetpnpevent-handler-in-an-intermediate-driver.md)

[セットの電源要求の処理](handling-a-set-power-request.md)

 

 






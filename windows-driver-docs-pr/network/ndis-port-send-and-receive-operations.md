---
title: NDIS ポートの送信および受信操作
description: NDIS ポートの送信および受信操作
ms.assetid: f9a22b7b-5565-4d56-a9b9-22562b6bf0da
keywords:
- ポート WDK NDIS、送受信操作
- NDIS ポート WDK、送信し、受信操作
- データの送信ポート operations WDK NDIS
- 受信操作 WDK NDIS ポート
- ポート WDK NDIS ターゲットにします。
- ソース ポート WDK NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5b317c8ad1f0e8b6b17e747558185551094763b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354963"
---
# <a name="ndis-port-send-and-receive-operations"></a>NDIS ポートの送信および受信操作





NDIS ドライバーが NDIS ポート operations の受信し、送信を関連付けることができます。ポート番号、 *PortNumber* NDIS のパラメーターを送信し、送信操作のターゲット ポートまたは受信を示す値を発信元ポート、受信機能を識別します。 場合*PortNumber* 0 の場合は、既定のポートを使用します。 設定は常に超える何もする NDIS ドライバーはドライバー スタックでは必要ありません NDIS 処理の既定のポートおよびミニポート ドライバーは、その他のポートの割り当て、ときに、 *PortNumber*パラメーターを 0 にします。 ミニポート ドライバーでのポートの割り当てに関する詳細については、次を参照してください。[割り当て NDIS ポート](allocating-an-ndis-port.md)します。

ミニポート ドライバーでは、ポートを割り当てます場合、ドライバーの関連と、ポートが関連付けられているミニポート アダプターの適切なサブインタ フェース上のデータの送受信に使用できます。 ただし、上にあるドライバーは、すべてのデータを送信する前に、ポートがアクティブながあることを確認する必要があります。 ミニポート ドライバーでは、関連付けられているサブインタ フェースが利用可能になるときに、ポートがアクティブ化します。 ミニポート ドライバーでのポートをアクティブ化についての詳細については、次を参照してください。[ライセンス NDIS ポート](activating-an-ndis-port.md)します。

NDIS を呼び出すと、 [ *ProtocolBindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)プロトコル ドライバー、NDIS の関数で現在アクティブなすべてのポートの一覧を提供する、 **ActivePorts** のメンバー[**NDIS\_バインド\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)構造体、 *BindParameters*パラメーターを指します。 NDIS は、ポートがアクティブ化し、非アクティブ化されたときに、PnP イベントとプロトコル ドライバーにも通知します。 PnP ポートのアクティブ化と非アクティブ化の通知の詳細については、次を参照してください。 [NDIS ポート PnP 通知の処理](handling-ndis-ports-pnp-event-notifications.md)します。 全般的な情報は約送信および受信操作を参照してください。[送信および受信操作](send-and-receive-operations.md)します。

 

 






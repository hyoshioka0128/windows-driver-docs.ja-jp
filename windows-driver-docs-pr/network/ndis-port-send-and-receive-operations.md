---
title: NDIS ポートの送信し、受信操作
description: NDIS ポートの送信し、受信操作
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
ms.openlocfilehash: a3a1cff504824aa5e1796f0dbb196fe41fd05e3a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550009"
---
# <a name="ndis-port-send-and-receive-operations"></a>NDIS ポートの送信し、受信操作





NDIS ドライバーが NDIS ポート operations の受信し、送信を関連付けることができます。ポート番号、 *PortNumber* NDIS のパラメーターを送信し、送信操作のターゲット ポートまたは受信を示す値を発信元ポート、受信機能を識別します。 場合*PortNumber* 0 の場合は、既定のポートを使用します。 設定は常に超える何もする NDIS ドライバーはドライバー スタックでは必要ありません NDIS 処理の既定のポートおよびミニポート ドライバーは、その他のポートの割り当て、ときに、 *PortNumber*パラメーターを 0 にします。 ミニポート ドライバーでのポートの割り当てに関する詳細については、[割り当て NDIS ポート](allocating-an-ndis-port.md)を参照してください。

ミニポート ドライバーでは、ポートを割り当てます場合、ドライバーの関連と、ポートが関連付けられているミニポート アダプターの適切なサブインタ フェース上のデータの送受信に使用できます。 ただし、上にあるドライバーは、すべてのデータを送信する前に、ポートがアクティブながあることを確認する必要があります。 ミニポート ドライバーでは、関連付けられているサブインタ フェースが利用可能になるときに、ポートがアクティブ化します。 ミニポート ドライバーでのポートをアクティブ化についての詳細については、[ライセンス NDIS ポート](activating-an-ndis-port.md)を参照してください。

NDIS を呼び出すと、 [ *ProtocolBindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570220)プロトコル ドライバー、NDIS の関数で現在アクティブなすべてのポートの一覧を提供する、 **ActivePorts** のメンバー[**NDIS\_バインド\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff564832)構造体、 *BindParameters*パラメーターを指します。 NDIS は、ポートがアクティブ化し、非アクティブ化されたときに、PnP イベントとプロトコル ドライバーにも通知します。 PnP ポートのアクティブ化と非アクティブ化の通知の詳細については、[NDIS ポート PnP 通知の処理](handling-ndis-ports-pnp-event-notifications.md)を参照してください。 全般的な情報は約送信および受信操作を参照してください。[送信および受信操作](send-and-receive-operations.md)します。

 

 






---
title: NDIS ポートの送信および受信操作
description: NDIS ポートの送信および受信操作
ms.assetid: f9a22b7b-5565-4d56-a9b9-22562b6bf0da
keywords:
- ポート WDK NDIS、送信および受信操作
- NDIS ポート WDK、送信および受信操作
- 送信操作 WDK NDIS ポート
- 受信操作 WDK NDIS ポート
- ターゲットポート WDK NDIS
- ソースポート WDK NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8dfff928c0a682fbc6b27606c65beab01c0c4009
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826950"
---
# <a name="ndis-port-send-and-receive-operations"></a>NDIS ポートの送信および受信操作





NDIS ドライバーは、送信および受信操作を NDIS ポートに関連付けることができます。NDIS の送信および受信機能*のポート番号パラメーターの*ポート番号によって、送信操作のターゲットポートまたは受信表示の発信元ポートが識別されます。 ポート番号が 0*の場合は*、既定のポートが使用されます。 NDIS で既定のポートが処理され、ミニポートドライバーによって他のポートが割り当てられていない場合、常*にポート番号パラメーターを*0 に設定するだけではなく、ドライバースタック内の ndis ドライバーは必要ありません。 ミニポートドライバーでのポートの割り当ての詳細については、「 [NDIS ポートの割り当て](allocating-an-ndis-port.md)」を参照してください。

ミニポートドライバーによってポートが割り当てられている場合は、そのポートを使用して、関連するミニポートアダプターの適切なサブインタフェースでデータを送受信できます。 ただし、その後のドライバーでは、データを送信する前にポートがアクティブであることを確認する必要があります。 ミニポートドライバーは、関連するサブポートが使用可能になったときにポートをアクティブにします。 ミニポートドライバーでポートをアクティブ化する方法の詳細については、「 [NDIS ポートのアクティブ化](activating-an-ndis-port.md)」を参照してください。

NDIS がプロトコルドライバーの[*Protocolbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)関数を呼び出すと、ndis は、 [**NDIS\_\_BIND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)の**activeports**メンバー内の現在アクティブなすべてのポートの一覧を提供します *。BindParameters*パラメーターはを指します。 また、ポートがアクティブ化され、非アクティブ化されると、プロトコルドライバーに PnP イベントが通知されます。 PnP ポートのアクティブ化と非アクティブ化の通知の詳細については、「 [NDIS ポートの Pnp 通知の処理](handling-ndis-ports-pnp-event-notifications.md)」を参照してください。 送信操作と受信操作の一般的な情報については、「[送信および受信操作](send-and-receive-operations.md)」を参照してください。

 

 






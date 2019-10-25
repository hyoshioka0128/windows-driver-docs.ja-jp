---
title: NDIS ポートのアクティブ化
description: NDIS ポートのアクティブ化
ms.assetid: 0f3bfda2-8faa-4a92-a76b-0c0c361bd667
keywords:
- ポート WDK NDIS、アクティブ化
- NDIS ポート WDK、アクティブ化
- NDIS ポートのアクティブ化
- ポートの状態 WDK NDIS
- アクティブ化 PnP イベント WDK NDIS ポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5044fed00c74a9961187ace2fbdc4ed97737916
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835393"
---
# <a name="activating-an-ndis-port"></a>NDIS ポートのアクティブ化





ミニポートドライバーが NDIS ポートを正常に割り当てた後、NDIS 関数でポート番号を使用する前に、ドライバーはポートをアクティブにする必要があります。 ポートをアクティブ化するために、ミニポートドライバーはポートライセンス認証プラグアンドプレイ (PnP) イベントを NDIS に送信します。 ポートアクティブ化 PnP イベントを送信するために、ミニポートドライバーは、 [**NdisMNetPnPEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismnetpnpevent)関数の呼び出しで**NetEventPortActivation** PnP イベントコードを使用します。

ポートをアクティブにするには、ミニポートドライバーで、 **NdisMNetPnPEvent**の*NetPnPEvent*パラメーターが次のように、 [**NET\_PNP\_イベント\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event_notification)構造体のメンバーをに設定する必要があります。

<a href="" id="portnumber"></a>**PortNumber**  
イベント通知の送信元ポート。 ポート番号は**NetPnPEvent**メンバーが指定する構造体の**バッファー**メンバーで指定されるため、このメンバーを0に設定します。

<a href="" id="netpnpevent"></a>**NetPnPEvent**  
ポートのアクティブ化イベントを記述する[**NET\_PNP\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event)構造。 この構造体のメンバーを次のように設定します。

<a href="" id="netevent"></a>**NetEvent**  
イベントを説明するイベントコード。 このメンバーを**NetEventPortActivation**に設定します。

<a href="" id="buffer"></a>**格納**  
[**NDIS\_ポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port)構造体のリンクリストへのポインター。 NDIS\_ポート構造体の**次**のメンバーは、一覧の次の NDIS\_ポート構造を指します。

<a href="" id="bufferlength"></a>**BufferLength**  
**Buffer**に指定されているバイト数。 **Bufferlength**を、NDIS\_ポート構造体のサイズに設定します。

<a href="" id="other-members"></a>その他のメンバー  
NET\_PNP\_イベントの残りのメンバーを**NULL**に設定します。

ミニポートドライバーは、 [**NDIS\_ポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port)構造のリンクリストで、状態が非アクティブからアクティブに変更されたポートを一覧表示します。 ただし、ミニポートアダプターの既定のポートが**NetEventPortActivation** PnP イベントのターゲットである場合、既定のポートは一覧の唯一のポートである必要があります。

ミニポートドライバーが、ポートのアクティブ化を NDIS に通知する場合 (およびこの通知呼び出しが返される前に)、ミニポートドライバーは、ポートに関連付けられている送信要求と OID 要求を処理する準備ができている必要があります。 ミニポートドライバーは、 [**NdisMNetPnPEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismnetpnpevent)の呼び出しが返されるまで、新しくアクティブ化されたポートのポート番号を状態で使用したり、通知を受信したりすることはできません。

NDIS は、既定のポートがアクティブになるまで、アクティブ化されたポートについての情報を通知しません。 NDIS がプロトコルドライバーの[*Protocolbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)関数を呼び出すと、ndis は、 [**NDIS\_\_BIND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)の**activeports**メンバー内の現在アクティブなすべてのポートの一覧を提供します *。BindParameters*パラメーターはを指します。 ミニポートドライバーによって新しいポートがアクティブになると、NDIS は**NetEventPortActivation** PnP イベントを使用して、ミニポートドライバーにバインドされているすべてのプロトコルドライバーに通知します。 プロトコルドライバーでこれらのポートのアクティブ化イベントを処理する方法の詳細については、「[ポートのアクティブ化 PnP イベントの処理](handling-the-port-activation-pnp-event.md)」を参照してください。

ミニポートドライバーが NDIS ポートを割り当てる前に、ドライバーは[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)関数を呼び出して、 [**NDIS\_ミニポート\_アダプター\_登録\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)の登録属性を設定する必要があります。データ. ミニポートドライバーは、既定のポートのアクティブ化を制御できます。そのためには、 **NdisMSetMiniportAttributes**を呼び出すときに、NDIS\_ミニポート\_コントロール\_既定の\_ポート属性フラグを設定します。 ミニポートドライバーが既定のポートをアクティブ化することを前提としている場合、NDIS は、ポートのアクティブ化 PnP イベントを使用して既定のポートをアクティブにするまで、ミニポートアダプターとそれ以降のドライバーの間のバインドを開始しません。

NDIS\_ポート構造のリンクリストによって指定されるすべてのポートは、割り当て済みの状態である必要があります。 ミニポートドライバーは、既にアクティブになっているポートのアクティブ化を試みることはできません。ドライバーがアクティブなポートをアクティブ化しようとすると、NDIS ツリーはポートのアクティブ化エラーとして状況を報告します。

NDIS が一覧のポートのアクティブ化に失敗した場合は、 [**NdisMNetPnPEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismnetpnpevent)への呼び出しに失敗し、一覧のどのポートもアクティブ化されていない状態に変わります。 一部のポートが存在しないために NDIS がポートのアクティブ化に失敗した場合、 **NdisMNetPnPEvent**は NDIS\_STATUS\_無効な\_ポートの戻り値を返します。 一部のポートが割り当て済みの状態でないために NDIS がポートのアクティブ化に失敗した場合、 **NdisMNetPnPEvent**は NDIS\_STATUS\_無効な\_ポート\_状態の戻り値を返します。

ポートが正常にアクティブ化されると、ポートはアクティブ化された状態になります。 ミニポートドライバーは、アクティブ化された状態のポートの受信データとステータスを示すことができます。

NDIS は、既定のポートの認証状態を、 [**ndis\_ミニポート\_INIT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_init_parameters)構造体の**Defaultportauthstates**メンバーにある[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数に渡します。 ミニポートドライバーによって既定のポートが制御される場合、ミニポートドライバーによって既定のポートがアクティブになると、既定の認証設定を使用して既定のポートをアクティブにすることができます。 既定の認証設定を使用するには、ndis\_PORT\_CHAR\_使用して、 [**ndis\_ポート\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_characteristics)の構造の**FLAGS**メンバーで既定\_認証\_設定フラグ\_使用します。 ミニポートドライバーでは、NDIS\_PORT\_CHAR\_使用して、割り当てとアクティブ化を行うポートに\_既定\_認証\_設定フラグを使用できます。 アクティベーションの場合、NDIS は、新しくアクティブ化されたポートに既定の認証状態を割り当て、 **NetEventPortActivation**イベントの[**NdisMNetPnPEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismnetpnpevent)に渡される認証状態を無視します。

既定のポートの制御とポートの割り当ての詳細については、「 [NDIS ポートの割り当て](allocating-an-ndis-port.md)」を参照してください。

 

 






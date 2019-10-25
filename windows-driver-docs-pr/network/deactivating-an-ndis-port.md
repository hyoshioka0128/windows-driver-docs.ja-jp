---
title: NDIS ポートの非アクティブ化
description: NDIS ポートの非アクティブ化
ms.assetid: 2a5d288f-b6ea-4b63-91a3-44155aae8064
keywords:
- ポート WDK NDIS、非アクティブ化
- NDIS ポート WDK、非アクティブ化
- NDIS ポート WDK NDIS の非アクティブ化
- PnP イベントの非アクティブ化 WDK の NDIS ポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73c0df73910ad0432900f31f45acc0019320a313
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834955"
---
# <a name="deactivating-an-ndis-port"></a>NDIS ポートの非アクティブ化





NDIS ポートを非アクティブ化するために、ミニポートドライバーはポートの非アクティブ化プラグアンドプレイ (PnP) イベントを NDIS に送信します。 ミニポートドライバーによってポートが正常にアクティブ化された後、ドライバーはポートを解放する前にポートを非アクティブ化する必要があります。 また、ドライバーは、アプリケーション固有の理由によりポートを非アクティブにする場合があります。 ポートは非アクティブ化した後で再アクティブ化できますが、ポートが解放されている場合は再アクティブ化できません。

ポートの非アクティブ化の PnP イベントを送信するために、ミニポートドライバーは、 [**NdisMNetPnPEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismnetpnpevent)関数の呼び出しで**NetEventPortDeactivation** PnP イベントコードを使用します。 ポートを非アクティブ化するには、 **NdisMNetPnPEvent**の*NetPnPEvent*パラメーターで次のように、 [**NET\_PNP\_イベント\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event_notification)構造のメンバーを設定する必要があります。

<a href="" id="portnumber"></a>**PortNumber**  
イベント通知の送信元ポート。 ポート番号は**NetPnPEvent**メンバーが指定する構造体の**バッファー**メンバーで指定されるため、このメンバーを0に設定します。

<a href="" id="netpnpevent"></a>**NetPnPEvent**  
ポートの非アクティブ化イベントを記述する[**NET\_PNP\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event)構造。 この構造体のメンバーを次のように設定します。

<a href="" id="netevent"></a>**NetEvent**  
イベントを説明するイベントコード。 このメンバーを**NetEventPortDeactivation**に設定します。

<a href="" id="buffer"></a>**格納**  
NUMBER 型の要素\_の NDIS\_ポートの配列へのポインター。 配列には、ミニポートドライバーが非アクティブ化しているすべてのポートのポート番号が含まれています。

<a href="" id="bufferlength"></a>**BufferLength**  
**Buffer**に指定されているバイト数。 **Bufferlength**を、**バッファー**が指す配列のサイズに設定します。 配列内の要素の数を取得するには、 **Bufferlength**の値を、NDIS\_PORT\_number データ型のサイズに除算します。

<a href="" id="other-members"></a>その他のメンバー  
NET\_PNP\_イベントの残りのメンバーを**NULL**に設定します。

ミニポートドライバーは、非アクティブ化するポートの一覧を含む配列を提供できます。 ただし、ミニポートアダプターの既定のポートが**NetEventPortDeactivation** PnP イベントのターゲットである場合、既定のポートは、配列で指定されている唯一のポートである必要があります。

ミニポートドライバーは、いつでもアクティブなポートを非アクティブにすることができます。 ただし、ミニポートドライバーがポートを非アクティブ化する前に、そのポートに関連付けられている未処理のステータスの表示や受信通知がないことを確認する必要があります。 ポートの非アクティブ化の PnP イベントはミニポートドライバーによって送信されますが、非アクティブ化されたポートに関連付けられている状態や受信の通知を開始することはできません。

また、ポートを再アクティブ化することもできます。 NDIS ポートのアクティブ化の詳細については、「 [Ndis ポートのアクティブ化](activating-an-ndis-port.md)」を参照してください。

ミニポートドライバーによってポートが非アクティブになると、NDIS は**NetEventPortDeactivation** PnP イベントを使用して、ミニポートドライバーにバインドされているすべてのプロトコルドライバーに通知します。 この PnP イベントは、割り当て済みの状態に変更されたポートを一覧表示し、既に非アクティブ化されているポートは含まれません。 プロトコルドライバーでポートの非アクティブ化イベントを処理する方法の詳細については、「[ポートの非アクティブ化の PnP イベントの処理](handling-the-port-deactivation-pnp-event.md)」を参照してください。

ミニポートドライバーが NDIS ポートを割り当てる前に、ドライバーは[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)関数を呼び出して、 [**NDIS\_ミニポート\_アダプター\_登録\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)の登録属性を設定する必要があります。データ. ミニポートドライバーは、既定のポートのアクティブ化を制御できます。そのためには、 **NdisMSetMiniportAttributes**を呼び出すときに、NDIS\_ミニポート\_コントロール\_既定の\_ポート属性フラグを設定します。 ミニポートドライバーが既定のポートをアクティブ化することを前提としていて、ミニポートドライバーが既定のポートをアクティブ化した場合は、既定のポートを非アクティブ化してから、ミニ[*Porthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)関数から戻る必要があります。

NDIS\_PORT\_NUMBER 要素の配列によって指定されるすべてのポートは、アクティブ化された状態である必要があります。 ミニポートドライバーは、既に非アクティブ化されているポートの非アクティブ化を試みることはできません。

NDIS がポート配列内のポートの非アクティブ化に失敗した場合、ポート配列内のポートはいずれも状態を変更しません。 指定されたポートの一部が存在しないために非アクティブ化が失敗した場合、 [**NdisMNetPnPEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismnetpnpevent)関数は NDIS\_STATUS\_無効な\_ポートの戻り値を返します。 一部のポートがアクティブ化されていない状態であるために非アクティブ化が失敗した場合、 **NdisMNetPnPEvent**は NDIS\_STATUS\_無効な\_ポート\_状態の戻り値を返します。

**NdisMNetPnPEvent**への呼び出しによってが返されるまで、ポートは非アクティブ化されず、ミニポートドライバーは OID 要求を処理し、そのポートに関連付けられている要求を送信できる必要があります。

ミニポートドライバーが既定のポートを非アクティブにすると、NDIS は、それ以降のプロトコルドライバーとミニポートアダプター間のすべてのバインドを閉じます。 ミニポートドライバが既定のポートを非アクティブ化しようとし、既定のポートが既に非アクティブ化されている場合、 [**NdisMNetPnPEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismnetpnpevent)は失敗し、NDIS\_STATUS\_無効\_ポート\_状態の戻り値が返されます。 ミニポートドライバが既定のポートを非アクティブ化しようとしたときに、既定のポートが NDIS\_PORT\_NUMBER 要素の配列に指定されている唯一のポートではない場合、 **NdisMNetPnPEvent**は失敗し、ndis\_の状態が返され\_\_ポートの戻り値が無効です。 ミニポートドライバーによって**バッファー**メンバーが**NULL**または**bufferlength**メンバーにゼロに設定されている場合、ndis は**NdisMNetPnPEvent**呼び出しに失敗し、ndis\_STATUS\_無効な\_パラメーターの戻り値を返します。

ポートが正常に非アクティブ化されると、ポートは [割り当て済み] 状態になります。 ミニポートドライバーは、割り当てられた状態のポートの受信データまたは状態を示すことはできません。

 

 






---
title: 仮想接続の違い
description: 仮想接続の違い
ms.assetid: 6e705f31-eec7-4b9c-a46f-ff7641d224c2
keywords:
- 仮想接続 WDK いる CoNDIS、マネージャーを呼び出すと MCM のドライバー
- シグナリングの VCs WDK いる CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b613b84fc7355297d9e91bb7c946a6c6c34a0c2a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381378"
---
# <a name="differences-in-virtual-connections"></a>仮想接続の違い





コール マネージャーを使用して*VCs のシグナリング*とスイッチなどのネットワーク エンティティの間のシグナリング メッセージを送受信します。 コール マネージャーのシグナリング VCs は、NDIS に表示されます。 コール マネージャーは、作成、アクティブ化、非アクティブ化、および NDIS への呼び出しですべての VCs を削除する必要があります。 ただし、MCM ドライバーのシグナリングの VCs は、NDIS を不透明なは。 MCM ドライバーはいない作成、アクティブ化、非アクティブ化、および削除 NDIS への呼び出しの VCs をシグナル通知。 代わりに、MCM、ドライバーはこのような操作を内部的に実行します。 MCM、ドライバーは、クライアントのデータ送信または受信に使用される VCs で操作を実行する NDIS を呼び出す必要があります。 NDIS する必要がありますの追跡クライアント VCs ためにです。

MCM のドライバーがコール マネージャーとミニポート ドライバーの両方であるため、特定の接続指向の機能は冗長です。 具体的には、 [ **MiniportCoCreateVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_create_vc)と[ **MiniportCoDeleteVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_delete_vc)が冗長になると、MCM ドライバーで提供されないためです。 VC 操作は、によって処理されます。

-   MCM ドライバーの[ **ProtocolCoCreateVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_co_create_vc)と[ **ProtocolCoDeleteVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_co_delete_vc)関数の作成または削除のクライアントが要求したときに、VC します。

-   [**NdisMCmCreateVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmcreatevc)と[ **NdisMCmDeleteVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmdeletevc) MCM ドライバーが作成または VC を削除します。

-   [**NdisMCmActivateVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmactivatevc)と[ **NdisCmDeactivateVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscmdeactivatevc) MCM ドライバーがアクティブにまたは VC を非アクティブ化します。

MCM にドライバーを指定する必要があります、 [ **MiniportCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_oid_request)クライアントでの照会や設定は、ミニポート ドライバー情報を使用するための関数と[ **MiniportCoSendNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_send_net_buffer_lists)クライアントから送信操作を処理する関数。

 

 






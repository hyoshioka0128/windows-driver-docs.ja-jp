---
title: 仮想接続の違い
description: 仮想接続の違い
ms.assetid: 6e705f31-eec7-4b9c-a46f-ff7641d224c2
keywords:
- 仮想接続 WDK、MCM ドライバー、および呼び出しマネージャー
- シグナリングの WDK の場合
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d51954b60ca7770db4e0088150cb0df717884c4e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834891"
---
# <a name="differences-in-virtual-connections"></a>仮想接続の違い





呼び出しマネージャーは、*シグナリング VCs*を使用して、ネットワークエンティティ (スイッチなど) との間でシグナリングメッセージを送受信します。 呼び出しマネージャーのシグナリング VCs は、NDIS から参照できます。 呼び出しマネージャーは、NDIS の呼び出しを使用して、すべての VCs を作成、アクティブ化、非アクティブ化、および削除する必要があります。 ただし、MCM ドライバーのシグナリング VCs は、NDIS に対して非透過的です。 MCM ドライバーでは、NDIS への呼び出しによるシグナリング VCs の作成、アクティブ化、非アクティブ化、削除は行われません。 代わりに、MCM ドライバーは内部でこのような操作を実行します。 MCM ドライバーは、クライアントデータの送受信に使用される VCs に対して操作を実行するために、NDIS を呼び出す必要があります。 これは、NDIS がクライアント VCs を追跡する必要があるためです。

MCM ドライバーは呼び出しマネージャーとミニポートドライバーの両方であるため、特定の接続指向関数は冗長です。 具体的には、 [**MiniportCoCreateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_create_vc)と[**MiniportCoDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_delete_vc)は冗長であるため、mcm ドライバーでは提供されません。 VC 操作は次の方法で処理されます。

-   MCM ドライバーの[**ProtocolCoCreateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_create_vc)と[**ProtocolCoDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_delete_vc)は、クライアントが VC の作成または削除を要求したときに機能します。

-   [**NdisMCmCreateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmcreatevc)と[**NdisMCmDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdeletevc)は、MCM ドライバーが VC を作成または削除するときに行います。

-   [**NdisMCmActivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmactivatevc)と[**NdisCmDeactivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdeactivatevc)は、MCM ドライバーが VC をアクティブまたは非アクティブにしたときに有効になります。

MCM ドライバーは、クライアントがミニポートドライバー情報を照会または設定するときに使用する[**MiniportCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)関数と、クライアントからの送信操作を処理するための[**Miniportcosendnetbufferlists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_send_net_buffer_lists)関数を提供する必要があります。

 

 






---
title: 仮想接続のコンテキスト
description: 仮想接続のコンテキスト
ms.assetid: 9b318f9d-70f4-41b5-acab-5a193f7d2ab4
keywords:
- 仮想接続 WDK ネットワーク、コンテキスト
- ネットワークの VCs WDK、コンテキスト
- コンテキスト WDK 仮想接続
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5da8eeff07fec2e74931944c90f440ab7124f94
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377010"
---
# <a name="virtual-connection-context"></a>仮想接続のコンテキスト





呼び出しを行う前に、接続指向のクライアントは、仮想接続 (VC) するパケット送信したり、受信したを設定する接続指向のミニポート ドライバーを要求します。 同様に、接続指向のクライアントに着信する前に、コール マネージャーまたは統合のミニポート ドライバーを呼び出すマネージャー (MCM) ドライバーを要求するミニポート着信通話の VC を設定します。

VC では、接続指向の 2 つのエンティティ間の論理接続です。 接続指向の転送および受信は、特定の VC で常に発生します。

接続指向のミニポート ドライバーでは、ミニポート ドライバーに割り当てられたコンテキストの領域を設定する各 VC に関する状態情報を保持します。 この VC あたりのコンテキストでは、ミニポート ドライバーによって保持され、NDIS してプロトコル ドライバーに対して非透過的です。 その[ **MiniportCoCreateVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_create_vc)関数では、NDIS、および NDIS に VC コンテキストの領域を識別するハンドルを渡します接続指向のミニポート ドライバー パスを*NdisVcHandle*ですミニポート ドライバーに、適切な接続指向のクライアントおよびコール マネージャーまたはコール マネージャー (MCM) の統合のミニポート ドライバーには、作成した VC を一意に識別します。

データを送信または VC で受信したことができます、前に、VC をアクティブにする必要があります。 コール マネージャーは、呼び出すことによって、VC のアクティブ化を開始**Ndis (M) CmActivateVc**を有効にする VC の特性を含む呼び出しのパラメーターを渡すとします。 NDIS ミニポート ドライバーの呼び出しでは、この呼び出しに応答して、 [ **MiniportCoActivateVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_activate_vc)関数で、VC をアクティブにします。

コール マネージャーに呼び出すことによって、VC できます非アクティブ化後の呼び出しが完了するか、VC、それ以外の場合は必要ありません、 [ **Ndis (M) CmDeactivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscmdeactivatevc)、それが原因でを呼び出す、ミニポート ドライバーの NDIS [ **MiniportCoDeactivateVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_deactivate_vc)関数。 接続指向クライアントまたはコール マネージャーは、呼び出すことによって、VC の削除を開始できる[ **NdisCoDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscodeletevc)、それが原因でを呼び出す、ミニポート ドライバーの NDIS [ **MiniportCoDeleteVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_delete_vc)関数。

Vc のミニポート ドライバー操作の詳細については、次を参照してください。 [VCs に対する操作](operations-on-vcs.md)します。

 

 






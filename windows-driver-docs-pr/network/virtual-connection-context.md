---
title: 仮想接続のコンテキスト
description: 仮想接続のコンテキスト
ms.assetid: 9b318f9d-70f4-41b5-acab-5a193f7d2ab4
keywords:
- 仮想接続 WDK ネットワーク, コンテキスト
- VCs WDK ネットワーク, コンテキスト
- コンテキスト WDK 仮想接続
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 179fac4ba2452ca5ab68187b5c0efe07a036b7db
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842958"
---
# <a name="virtual-connection-context"></a>仮想接続のコンテキスト





接続指向のクライアントは、呼び出しを行う前に、接続指向のミニポートドライバーに対して、パケットを送受信できる仮想接続 (VC) を設定するように要求します。 同様に、接続指向クライアントへの着信呼び出しを示す前に、コールマネージャーまたは統合されたミニポート呼び出しマネージャー (MCM) ドライバーが、受信した呼び出し用に VC を設定するようにミニポートドライバーに要求します。

VC は、2つの接続指向エンティティ間の論理接続です。 接続指向の送信と受信は常に特定の VC で行われます。

接続指向のミニポートドライバーは、設定されている各 VC について、ミニポートドライバーで割り当てられたコンテキスト領域に状態情報を保持します。 この VC ごとのコンテキストはミニポートドライバーによって保持され、NDIS およびプロトコルドライバーに対して非透過的です。 [**MiniportCoCreateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_create_vc)関数では、接続指向のミニポートドライバーが VC コンテキスト領域へのハンドルを ndis に渡し、ndis は作成された vc を一意に識別する*NdisVcHandle*をミニポートドライバーに渡し、適切な接続指向クライアント、および呼び出しマネージャーまたは統合ミニポート呼び出しマネージャー (MCM) ドライバー。

VC でデータを送受信する前に、VC をアクティブにする必要があります。 呼び出しマネージャーは、 **Ndis (M) CmActivateVc**を呼び出し、アクティブ化する vc の特性を含む呼び出しパラメーターを渡すことによって、vc のアクティブ化を開始します。 この呼び出しに応答して、NDIS は、VC をアクティブにするミニポートドライバーの[**MiniportCoActivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_activate_vc)関数を呼び出します。

呼び出しが完了するか、VC が不要であれば、呼び出しマネージャーは[**ndis (M) CmDeactivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdeactivatevc)を呼び出すことで vc を非アクティブ化できます。これにより、ndis はミニポートドライバーの[**MiniportCoDeactivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_deactivate_vc)関数を呼び出します。 接続指向クライアントまたは呼び出しマネージャーは、 [**NdisCoDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscodeletevc)を呼び出すことによって VC の削除を開始できます。これにより、NDIS はミニポートドライバーの[**MiniportCoDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_delete_vc)関数を呼び出します。

VCs でのミニポートドライバーの操作の詳細については、「 [vcs での操作](operations-on-vcs.md)」を参照してください。

 

 






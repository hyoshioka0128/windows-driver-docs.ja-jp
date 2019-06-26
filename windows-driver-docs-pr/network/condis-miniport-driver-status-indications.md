---
title: CoNDIS ミニポート ドライバーの状態表示
description: CoNDIS ミニポート ドライバーの状態表示
ms.assetid: 1f1174ba-8b0a-4d43-96c9-2d92f50a22c4
keywords:
- ミニポート ドライバー WDK ネットワー キング、いる CoNDIS
- NDIS ミニポート ドライバー WDK、いる CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 056a44c41b2a82ab05681e209399e2702d9b9da9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385112"
---
# <a name="condis-miniport-driver-status-indications"></a>CoNDIS ミニポート ドライバーの状態表示





ミニポート ドライバーの呼び出し、 [ **NdisMCoIndicateStatusEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcoindicatestatusex)ミニポート アダプターの状態の変更を報告する関数。 ミニポート ドライバー パス**NdisMCoIndicateStatusEx**へのポインター、 [ **NDIS\_状態\_INDICATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)を含む構造体、状態情報。

状態の表示には、状態と状態の変更の理由の種類を識別する情報が含まれます。

ミニポート ドライバーを設定する必要があります、 **SourceHandle**の NDIS メンバー\_状態\_に渡される NDIS ハンドルを示す値構造体、 *MiniportAdapterHandle*パラメーター、 [ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数。 状態の表示が OID 要求に関連付けられている場合は、ミニポート ドライバーを設定できます、 **DestinationHandle**と**RequestId** NDIS のメンバー\_状態\_INDICATION ようにその NDIS は、特定のプロトコル バインドを状態を示す値を提供できます。 OID 要求の詳細については、次を参照してください。[いる CoNDIS ミニポート ドライバーの OID 要求](condis-miniport-driver-oid-requests.md)します。

 

 






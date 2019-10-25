---
title: ミニポート アダプター状態表示
description: ミニポート アダプター状態表示
ms.assetid: feb5259f-ce9b-40eb-85d2-0064bce692fc
keywords:
- WDK ネットワーク、ミニポートアダプターの状態を示す状態
- ミニポートアダプター WDK ネットワーク、状態のインジケーター
- WDK ネットワークのアダプター、状態のインジケーター
- NdisMIndicateStatusEx
- NDIS_STATUS_INDICATION
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e087d27b44d04b1246d015808407de968b145e2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844244"
---
# <a name="miniport-adapter-status-indications"></a>ミニポート アダプター状態表示





ミニポートドライバーは、 [**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)関数を呼び出して、ミニポートアダプターの状態の変化を報告します。 ミニポートドライバーは、状態情報を格納していることを示す\_**NdisMIndicateStatusEx**の[**状態\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)にポインターを渡します。

状態の表示には、状態の種類と状態の変更の理由を識別するための情報が含まれます。

ミニポートドライバーでは、 **Sourcehandle**メンバーを、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数の*miniportadapterhandle*パラメーターに渡された NDIS ハンドルに設定する必要があります。 ステータス表示が OID 要求に関連付けられている場合、ミニポートドライバーは**Destinationhandle**メンバーと**RequestId**メンバーを設定して、NDIS が特定のプロトコルバインドに状態を示すことができるようにすることができます。

 

 






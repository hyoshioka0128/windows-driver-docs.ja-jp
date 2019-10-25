---
title: CoNDIS ミニポート ドライバーの状態表示
description: CoNDIS ミニポート ドライバーの状態表示
ms.assetid: 1f1174ba-8b0a-4d43-96c9-2d92f50a22c4
keywords:
- ミニポートドライバー WDK ネットワーク、CoNDIS
- NDIS ミニポートドライバー WDK、CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95bfba37c3f77585a3aaa934f084e2be5b74350b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835101"
---
# <a name="condis-miniport-driver-status-indications"></a>CoNDIS ミニポート ドライバーの状態表示





ミニポートドライバーは、 [**NdisMCoIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex)関数を呼び出して、ミニポートアダプターの状態の変化を報告します。 ミニポートドライバーは、状態情報を格納していることを示す\_**NdisMCoIndicateStatusEx**の[**状態\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)にポインターを渡します。

状態の表示には、状態の種類と状態の変更の理由を識別するための情報が含まれます。

ミニポートドライバーでは、ndis\_ステータス\_表示構造体の**Sourcehandle**メンバーを、Ndis が[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数の*miniportadapterhandle*パラメーターに渡すハンドルに設定する必要があります。 状態の表示が OID 要求に関連付けられている場合、ミニポートドライバーでは **、ndis**が特定のについての状態を示すことができるように、ndis\_ステータス\_を示す値を指定できます。プロトコルのバインド。 OID 要求の詳細については、「 [Condis ミニポートドライバー Oid 要求](condis-miniport-driver-oid-requests.md)」を参照してください。

 

 






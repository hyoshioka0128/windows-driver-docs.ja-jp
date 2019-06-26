---
title: ミニポート ドライバーの状態の表示
description: ミニポート ドライバーの状態の表示
ms.assetid: 366caecb-6c4b-42f3-927d-b72db764d6cf
keywords:
- WDK いる CoNDIS のステータス情報
- 接続指向 NDIS WDK、ミニポート ドライバー
- いる CoNDIS WDK ネットワー キング、ミニポート ドライバー
- ミニポート ドライバー WDK ネットワー キング、いる CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d46891ba141bb668b428aac630ffb1346b064c3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380930"
---
# <a name="indicating-miniport-driver-status"></a>ミニポート ドライバーの状態の表示





ミニポート ドライバーでは、ドライバーに関連する状態インジケーターを提供します。 いる CoNDIS 状態を示す値の関数は、コネクションレスの状態を示す値の関数に似ています。

接続指向のミニポート ドライバーを呼び出し、NIC の接続指向の NIC のステータスの変更または特定の VC アクティブの状態の変更を報告する[ **NdisMCoIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcoindicatestatusex)します。 提供されている場合は、ミニポート ドライバーが特定の VC のステータスの変更を報告、 *NdisVcHandle* VC を識別します。

ここでは、次のトピックについて説明します。

[いる CoNDIS ミニポート ドライバーの状態インジケーター](condis-miniport-driver-status-indications.md)

[いる CoNDIS プロトコル ドライバーの処理状態のインジケーター](handling-status-indications-in-a-condis-protocol-driver.md)

 

 






---
title: ミニポート ドライバーの状態の表示
description: ミニポート ドライバーの状態の表示
ms.assetid: 366caecb-6c4b-42f3-927d-b72db764d6cf
keywords:
- 状態情報 WDK CoNDIS
- 接続指向 NDIS WDK、ミニポートドライバー
- CoNDIS WDK ネットワーク、ミニポートドライバー
- ミニポートドライバー WDK ネットワーク、CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96360f129a8debca86625926dd7b47b0a5c61fe8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824685"
---
# <a name="indicating-miniport-driver-status"></a>ミニポート ドライバーの状態の表示





ミニポートドライバーは、状態を示すドライバーを使用します。 CoNDIS ステータス表示関数は、コネクションレスステータス表示関数に似ています。

接続指向の NIC の状態の変化、または NIC でアクティブな特定の VC の状態が変化したことを報告するために、接続指向ミニポートドライバーは[**NdisMCoIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex)を呼び出します。 ミニポートドライバーが特定の VC の状態の変更を報告している場合、その VC を識別する*NdisVcHandle*が提供されます。

ここでは、次のトピックについて説明します。

[CoNDIS ミニポートドライバーの状態のインジケーター](condis-miniport-driver-status-indications.md)

[CoNDIS プロトコルドライバーでのステータスの情報の処理](handling-status-indications-in-a-condis-protocol-driver.md)

 

 






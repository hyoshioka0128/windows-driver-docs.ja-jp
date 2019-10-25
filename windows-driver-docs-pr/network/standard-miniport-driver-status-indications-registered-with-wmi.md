---
title: WMI に登録されている標準ミニポート ドライバー状態表示
description: WMI に登録されている標準ミニポート ドライバー状態表示
ms.assetid: afebd0a2-c811-4534-9320-02b9292ba81b
keywords:
- WDK ネットワーク、WMI の状態を示す状態
- WMI WDK ネットワーク, 状態のインジケーター
- WDK ネットワーク、状態の Windows Management Instrumentation
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7317ad6e7c0d83652245b02fd0cf67eb5bc73361
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841852"
---
# <a name="standard-miniport-driver-status-indications-registered-with-wmi"></a>WMI に登録されている標準ミニポート ドライバー状態表示





NDIS は、 [**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)または[**NdisMCoIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex)関数によってミニポートドライバーによって示される ndis ステータスを示すために、guid を WMI に自動的に登録します。 一般的な状態の表示の一覧については、「[ステータス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)の表示」を参照してください。

Wmi クライアントが NDIS WMI イベントを受信するために WMI に登録すると、NDIS は対応する NDIS 状態の情報を WMI イベントに変換し、イベントに登録されているすべての WMI クライアントにイベントを報告します。

NDIS ドライバーでは、カスタムステータスのインジケーターを生成することもできます。 カスタムステータス表示と WMI の詳細については、「カスタマイズされた[oid と状態](customized-oids-and-status-indications.md)の表示」を参照してください。

 

 






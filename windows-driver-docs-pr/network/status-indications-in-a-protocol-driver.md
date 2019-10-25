---
title: プロトコル ドライバーの状態表示
description: プロトコル ドライバーの状態表示
ms.assetid: 4b0426bb-4311-4251-b9ee-38d081f061e5
keywords:
- プロトコルドライバー (WDK ネットワーク)、状態のインジケーター
- NDIS プロトコルドライバー WDK、状態の示さ
- WDK ネットワークプロトコルドライバーの状態を示す状態
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e97189ff0ab5733b51d7897897dfdca610651bfd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841827"
---
# <a name="status-indications-in-a-protocol-driver"></a>プロトコル ドライバーの状態表示





プロトコルドライバーには、状態を示す2つの異なるインターフェイスがあります。 [**Protocolstatusex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_status_ex)関数を提供するには、より低いエッジを持つ NDIS プロトコルドライバーが必要です。 NDIS は*Protocolstatusex*を呼び出します。基になるコネクションレスなミニポートドライバーが[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)を呼び出して、ハードウェアの状態の変化を報告します。 状態の変更が開始されると、NDIS は*Protocolstatusex*を呼び出します。 コネクションレスプロトコルドライバーでの状態の表示の詳細については、「[プロトコルドライバーでのステータス](handling-status-indications-in-a-protocol-driver.md)表示の処理」を参照してください。

接続指向プロトコルドライバーは、 [**Protocolcostatusex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_status_ex)関数を提供する必要があります。 基になる接続指向ミニポートドライバーが[**NdisMCoIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex)を呼び出して、ハードウェアの状態の変化を報告する場合、NDIS は*Protocolcostatusex*を呼び出します。 状態の変更が開始されると、NDIS は*Protocolcostatusex*を呼び出します。 接続指向プロトコルドライバーの状態の表示の詳細については、「[接続指向の操作](connection-oriented-operations.md)」を参照してください。

表示される状態の一覧については、「[ステータス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)の表示」を参照してください。

 

 






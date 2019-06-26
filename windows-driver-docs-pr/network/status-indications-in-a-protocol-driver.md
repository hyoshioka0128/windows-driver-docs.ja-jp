---
title: プロトコル ドライバーの状態表示
description: プロトコル ドライバーの状態表示
ms.assetid: 4b0426bb-4311-4251-b9ee-38d081f061e5
keywords:
- プロトコル ドライバー WDK ネットワー キング、状態インジケーター
- NDIS プロトコル ドライバー WDK、状態インジケーター
- 状態インジケーターの WDK ネットワー キング、プロトコル ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cae9fc25de2fb70e9313b1037cbae106525f057e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383609"
---
# <a name="status-indications-in-a-protocol-driver"></a>プロトコル ドライバーの状態表示





プロトコル ドライバーに状態インジケーターの 2 つの異なるインターフェイスがあります。 コネクションレスの下端との NDIS プロトコル ドライバーを指定するために必要な[ **ProtocolStatusEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_status_ex)関数。 NDIS 呼び出し*ProtocolStatusEx*基になるコネクションレス ミニポート ドライバーを呼び出すと[ **NdisMIndicateStatusEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex)そのハードウェアの状態の変更を報告します。 NDIS 呼び出し*ProtocolStatusEx*状態の変更を開始するとき。 コネクションレスのプロトコル ドライバーに状態インジケーターの詳細については、次を参照してください。[プロトコル ドライバーに状態インジケーターの処理](handling-status-indications-in-a-protocol-driver.md)します。

接続指向プロトコル ドライバーを指定する必要があります、 [ **ProtocolCoStatusEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_co_status_ex)関数。 NDIS 呼び出し*ProtocolCoStatusEx*を基になる接続指向のミニポート ドライバーを呼び出すと[ **NdisMCoIndicateStatusEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcoindicatestatusex)そのハードウェアの状態の変更を報告するには. NDIS 呼び出し*ProtocolCoStatusEx*状態の変更を開始するとき。 接続指向プロトコル ドライバーに状態インジケーターの詳細については、次を参照してください[Connection-Oriented 操作。](connection-oriented-operations.md)

可能な状態インジケーターの完全な一覧を参照してください。[状態インジケーター](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)します。

 

 






---
title: ハードウェアの状態のレポート
description: ハードウェアの状態のレポート
ms.assetid: d4572c6f-dc09-41c4-af5b-69482b458bef
keywords:
- WMI の WDK ネットワーク、ハードウェアの状態をレポート作成
- ミニポート ドライバー WDK ネットワーク、ハードウェアの状態
- NDIS ミニポート ドライバー WDK、ハードウェアの状態
- ハードウェアの状態の WDK ネットワーク
- WDK の NDIS ミニポートのステータス情報
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3fe22361ebf237630f7f4388471a4798fbb24607
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373262"
---
# <a name="reporting-hardware-status"></a>ハードウェアの状態のレポート





コネクションレスのミニポート ドライバーを呼び出すことによって上位層にハードウェアの状態の変更を示します[ **NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex)します。 接続指向のミニポート ドライバーを呼び出して変更を示し、 [ **NdisMCoIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcoindicatestatusex)します。

**NdisM (Co) IndicateStatusEx**は全般的なステータス コードおよび状態変更の理由をさらに定義するメディアに固有の情報を格納しているバッファーの両方を受け取ります。 NDIS は、プロトコルのドライバーをバインドするには、この状態変更を報告します。 NDIS の解釈またはそれ以外の場合、状態コードをインターセプトはありません。

ミニポート ドライバーでは、このような呼び出しを 1 つまたは複数を行うことができます。 ただし、NDIS の以前のバージョンとは異なり、ミニポート ドライバーは示しませんステータスの送信が完了したこと。 プロトコル ドライバーまたは configuration manager は、状態をログ記録したり、適切な措置を実行します。

[**NdisMCoIndicateStatusEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcoindicatestatusex)は任意の有効な NDIS\_状態\_*Xxx*値。

ミニポート ドライバーでは、プロトコルまたはより高いレベルのドライバーに意味のある状態コードを示す担当します。 プロトコル ドライバーには、状態値は必要ないか、その操作のコンテキストで意味を加えないが無視されます。

ミニポート ドライバーでのコンテキストでの状態を示すことはできません、 [ *MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)、 [ *MiniportInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_isr)、 [ *MiniportHaltEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)、または[ *MiniportShutdownEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_shutdown)関数。

ミニポート ドライバーのハードウェアの状態について、上位レイヤー ドライバーまたは NDIS ミニポート ドライバーを問い合わせもできます。 ときに、 [ *MiniportOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)コネクションレス ミニポート ドライバーの機能または[ **MiniportCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_oid_request)の関数を接続指向のミニポート ドライバー受信 OID\_GEN\_ハードウェア\_NDIS で定義されている適用可能な状態の値のいずれかで応答の状態、\_ハードウェア\_状態. これらの状態値は次のとおりです。

-   **NdisHardwareStatusReady**

-   **NdisHardwareStatusInitializing**

-   **NdisHardwareStatusReset**

-   **NdisHardwareStatusClosing**

-   **NdisHardwareStatusNotReady**

NDIS は NIC がパケットを受け入れる準備ができているかどうかを決定することで NDIS ドライバー--などのレイヤー間での操作を同期できるように、ミニポート ドライバーのクエリを実行できます。

 

 






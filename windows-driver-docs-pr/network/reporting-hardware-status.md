---
title: ハードウェアの状態を報告
description: ハードウェアの状態を報告
ms.assetid: d4572c6f-dc09-41c4-af5b-69482b458bef
keywords:
- WMI の WDK ネットワーク、ハードウェアの状態をレポート作成
- ミニポート ドライバー WDK ネットワーク、ハードウェアの状態
- NDIS ミニポート ドライバー WDK、ハードウェアの状態
- ハードウェアの状態の WDK ネットワーク
- WDK の NDIS ミニポートのステータス情報
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59065d4eee67ca215c43bdb25ae8d446e5247732
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528617"
---
# <a name="reporting-hardware-status"></a>ハードウェアの状態を報告





コネクションレスのミニポート ドライバーを呼び出すことによって上位層にハードウェアの状態の変更を示します[ **NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600)します。 接続指向のミニポート ドライバーを呼び出して変更を示し、 [ **NdisMCoIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563562)します。

**NdisM (Co) IndicateStatusEx**は全般的なステータス コードおよび状態変更の理由をさらに定義するメディアに固有の情報を格納しているバッファーの両方を受け取ります。 NDIS は、プロトコルのドライバーをバインドするには、この状態変更を報告します。 NDIS の解釈またはそれ以外の場合、状態コードをインターセプトはありません。

ミニポート ドライバーでは、このような呼び出しを 1 つまたは複数を行うことができます。 ただし、NDIS の以前のバージョンとは異なり、ミニポート ドライバーは示しませんステータスの送信が完了したこと。 プロトコル ドライバーまたは configuration manager は、状態をログ記録したり、適切な措置を実行します。

[**NdisMCoIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563562)は任意の有効な NDIS\_状態\_*Xxx*値。

ミニポート ドライバーでは、プロトコルまたはより高いレベルのドライバーに意味のある状態コードを示す担当します。 プロトコル ドライバーには、状態値は必要ないか、その操作のコンテキストで意味を加えないが無視されます。

ミニポート ドライバーでのコンテキストでの状態を示すことはできません、 [ *MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389)、 [ *MiniportInterrupt*](https://msdn.microsoft.com/library/windows/hardware/ff559395)、 [ *MiniportHaltEx*](https://msdn.microsoft.com/library/windows/hardware/ff559388)、または[ *MiniportShutdownEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559449)関数。

ミニポート ドライバーのハードウェアの状態について、上位レイヤー ドライバーまたは NDIS ミニポート ドライバーを問い合わせもできます。 ときに、 [ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)コネクションレス ミニポート ドライバーの機能または[ **MiniportCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff559362)の関数を接続指向のミニポート ドライバー受信 OID\_GEN\_ハードウェア\_NDIS で定義されている適用可能な状態の値のいずれかで応答の状態、\_ハードウェア\_状態. これらの状態値は次のとおりです。

-   **NdisHardwareStatusReady**

-   **NdisHardwareStatusInitializing**

-   **NdisHardwareStatusReset**

-   **NdisHardwareStatusClosing**

-   **NdisHardwareStatusNotReady**

NDIS は NIC がパケットを受け入れる準備ができているかどうかを決定することで NDIS ドライバー--などのレイヤー間での操作を同期できるように、ミニポート ドライバーのクエリを実行できます。

 

 






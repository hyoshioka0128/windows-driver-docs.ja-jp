---
title: ハードウェアの状態のレポート
description: ハードウェアの状態のレポート
ms.assetid: d4572c6f-dc09-41c4-af5b-69482b458bef
keywords:
- WMI WDK ネットワーク, レポートハードウェアの状態
- ミニポートドライバー WDK ネットワーク、ハードウェアの状態
- NDIS ミニポートドライバー WDK、ハードウェアの状態
- ハードウェアの状態 WDK ネットワーク
- ステータス情報 WDK NDIS ミニポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9de7c0b72555158244fda52ff4ee0d6c47a5fdd1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842045"
---
# <a name="reporting-hardware-status"></a>ハードウェアの状態のレポート





コネクションレスのミニポートドライバーは、 [**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)を呼び出すことによって、ハードウェアの状態が上位層に変更されたことを示します。 接続指向のミニポートドライバーは、 [**NdisMCoIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex)を呼び出して変更を示します。

**Ndism (Co) IndicateStatusEx**は、一般的な状態コードと、状態の変更の理由をさらに定義するメディア固有の情報を含むバッファーの両方を受け取ります。 NDIS は、この状態の変更をバインドされたプロトコルドライバーに報告します。 NDIS は、状態コードを解釈したり、それ以外の方法でインターセプトしたりすることはありません。

ミニポートドライバーは、1つまたは複数の呼び出しを行うことができます。 ただし、以前のバージョンの NDIS とは異なり、ミニポートドライバーはステータスの送信を完了したことを示していません。 プロトコルドライバーまたは configuration manager では、必要に応じて状態をログに記録するか、修正措置を講じることができます。

[**NdisMCoIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex)は、有効な NDIS\_状態\_*Xxx*値を受け取ります。

ミニポートドライバーは、プロトコルまたは上位レベルのドライバーに対して意味のあるステータスコードを示す役割を担います。 プロトコルドライバーは、関心のない状態値や、操作のコンテキストで意味を持たない状態値を無視します。

ミニポートドライバーは、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)、 [*miniportinterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_isr)、 [*miniporthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)、または[*miniportshutdownex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_shutdown)関数のコンテキストで状態を示すことはできません。

また、ミニポートドライバーは、上位層ドライバーまたはミニポートドライバーのハードウェア状態に関する NDIS によって問い合わせるすることもできます。 コネクションレスミニポートドライバーの[*Miniportoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)関数または接続指向ミニポートドライバーの[**MiniportCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)関数が、OID\_GEN\_ハードウェアの\_の状態を受け取ると、NDIS\_HARDWARE\_STATUS に定義されている該当するステータス値の。 これらの状態の値は次のとおりです。

-   **NdisHardwareStatusReady**

-   **NdisHardwareStatusInitializing**

-   **NdisHardwareStatusReset**

-   **NdisHardwareStatusClosing**

-   **NdisHardwareStatusNotReady**

ミニポートドライバーを照会して、NDIS が NDIS ドライバーのレイヤー間で操作を同期できるようにすることができます。たとえば、NIC がパケットを受け入れる準備ができているかどうかを判断します。

 

 






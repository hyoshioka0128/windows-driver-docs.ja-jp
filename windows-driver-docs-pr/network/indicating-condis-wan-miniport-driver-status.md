---
title: CoNDIS WAN ミニポート ドライバー状態の表示
description: CoNDIS WAN ミニポート ドライバー状態の表示
ms.assetid: c12492d7-e25d-4c80-8f2d-1e89931577ed
keywords:
- CoNDIS WAN ドライバー WDK ネットワーク、状態
- WDK ネットワーク、CoNDIS WAN ミニポートドライバーを示すステータス
- NDIS_STATUS_WAN_CO_LINKPARAMS
- NDIS_STATUS_WAN_CO_FRAGMENT
- WDK CoNDIS WAN を示す
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 495da24443a92f9d70320983f545af027bc4d6cb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824709"
---
# <a name="indicating-condis-wan-miniport-driver-status"></a>CoNDIS WAN ミニポート ドライバー状態の表示





CoNDIS WAN ミニポートドライバーは、 [**NdisMCoIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex)を呼び出して、バインドされたプロトコルドライバーに対する状態の変化を示します。 CoNDIS ミニポートドライバーまたは MCM の状態を示す詳細については、「[ミニポートドライバーのステータスを示す](indicating-miniport-driver-status.md)」を参照してください。

バインドされたプロトコルドライバーは、これらの状態の兆候を無視できます。 ただし、これらの表示を処理すると、通常、プロトコルドライバーとミニポートドライバーのパフォーマンスが向上します。

NDISWAN 中間ドライバーは、状態の兆候を NDIS に転送します。 NDIS は、バインドされたプロトコルドライバーまたは構成マネージャーの[**Protocolcostatusex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_status_ex)関数を呼び出します。 これらのプロトコルドライバーまたは configuration manager は、これらの兆候をログに記録し、必要に応じて修正措置を講じることができます。

CoNDIS WAN ミニポートドライバーの場合、NdisMCoIndicateStatusEx の呼び出しは、すべての[**Condis**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex)ドライバーの場合と同じです。ただし、condis wan ミニポートドライバーは、ミニポートドライバーの NIC にある各仮想接続 (VC) の WAN 固有の状態を示します。 ミニポートドライバーは、明示的な VC ハンドルを使用して**NdisMCoIndicateStatusEx**を呼び出し、この vc を共有するプロトコルドライバーに対するこれらの変更を示します。 ドライバーで **NULL * * * NdisVcHandle*が指定されている場合、状態は NIC の状態の一般的な変更に関連します。

各状態の表示には、次の2つの基本的な情報が表示されます。

-   一般ステータスを指定するステータスコード。 定義されている一般的な状態コードの数には制限があります。この一覧は将来の拡張の対象となります。

-   ステータス情報を格納しているバッファー。 この状態情報は、nic または NIC 上の VC に固有の、CoNDIS WAN ミニポートドライバーに固有です。 たとえば、バッファーには、最近3倍の速度で減少した、x.25 接続の新しい送信速度が含まれている場合があります。

CoNDIS WAN VC 状態のインジケーターは次のとおりです。

-   NDIS\_ステータス\_WAN\_CO\_LINKPARAMS

    CoNDIS は、NIC でアクティブ[](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex)になっている特定の VC のパラメーターが変更されたことを示すために、このドライバーを呼び出します。 この呼び出しでは、ミニポートドライバーは、 *NdisVcHandle*パラメーターの VC にハンドルを渡します。また、*一般ステータス*パラメーターの NDIS\_STATUS\_WAN\_co\_linkparams に、 [**wan\_co へのポインターを渡し\_** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565819(v=vs.85)) *Statusbuffer*パラメーター内の linkparams 構造体。 WAN\_CO\_LINKPARAMS VC の新しいパラメーターについて説明します。

-   NDIS\_ステータス\_WAN\_CO\_フラグメント

    CoNDIS WAN ミニポートドライバーは、VC のエンドポイントから部分的なパケットを受信したことを示すために**NdisMCoIndicateStatusEx**を呼び出します。 この呼び出しでは、ミニポートドライバーは、 *NdisVcHandle*パラメーターの VC にハンドルを渡します。また、*一般ステータス*パラメーターの NDIS\_STATUS\_WAN\_co\_フラグメント、および*Statusbuffer*パラメーター内の[**ndis\_WAN\_co\_fragment**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559030(v=vs.85))構造体へのポインターを渡します。 NDIS\_WAN\_CO\_FRAGMENT は、部分的なパケットが受信された理由を説明します。

    このことが示された後、接続指向クライアントは、VC のもう一方の端にある接続指向クライアントにフレームを送信する必要があります。 これらのフレームは、部分的なパケットの状況の反対側のエンドポイントに通知します。これにより、タイムアウトが発生するまで待機するために、反対側のエンドポイントが必要ないことがわかります。

    NDISWAN は、各 VC のフラグメントの表示数をカウントすることによって、破棄されたパケットを監視します。

 

 






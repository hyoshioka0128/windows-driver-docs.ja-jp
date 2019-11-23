---
title: 中間ドライバーでの設定およびクエリへの応答
description: 中間ドライバーでの設定およびクエリへの応答
ms.assetid: ccc99542-4a36-4bf9-8a19-4e7d385399da
keywords:
- クエリ操作 WDK NDIS 中間
- set 操作 WDK NDIS 中間
- OID 要求の取り消し
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e261dc3851521c62873fb4c38e51ab63fe5974b4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842019"
---
# <a name="responding-to-sets-and-queries-in-an-intermediate-driver"></a>中間ドライバーでの設定およびクエリへの応答





NDIS 中間ドライバーは、前の NDIS ドライバーにバインドされているため、[*ミニ Portoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)関数からクエリやセットを受け取ることもできます。 場合によっては、中間ドライバーは、このような要求を、基になるミニポートドライバーに渡すだけです。 それ以外の場合は、これらのクエリに応答して、上端でエクスポートされるメディアに適切に設定できます。 中間のドライバーは、それを経由する NDIS ドライバーから、基になるミニポートドライバーに送信されるすべての OID\_PNP\_*Xxx*要求を常に通過する必要があることに注意してください。 NDIS 6.0 中間ドライバーは OID 要求も取り消すことができます。

基になるドライバーに要求を転送するために、NDIS 中間ドライバーは[**NdisAllocateCloneOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatecloneoidrequest)を呼び出して、複製された[**ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造を割り当てます。 ドライバーは、要求を送信するために[**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)関数を呼び出します。 要求が完了したら、ドライバーは[**NdisFreeCloneOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreecloneoidrequest)関数を呼び出して、NDIS\_OID\_要求構造体を解放する必要があります。

OID 要求を取り消すには、 [**NdisCancelOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscanceloidrequest)関数を呼び出します。

通常、中間ドライバーが受け取る一般的な Oid は、中間のドライバーが基になるミニポートドライバーに送信するものと同じか類似しています。 中間ドライバーが受け取る中程度固有の Oid は、そのドライバーが必要とするメディアの種類です。

中間ドライバー自体が、基になるミニポートに設定要求を渡すのではなく、OID の設定を処理する場合は、設定する値を検証する必要があります。 中間ドライバーが、設定する値が範囲外であると判断した場合、設定された要求は失敗します。

**注**  中間のドライバーが、基になるミニポートドライバーに転送される tcp ネットワークデータの内容を変更して、tcp オフロード機能をネットワークデータで実行できない場合は、中間ドライバーは、要求を基になるミニポートに渡すのではなく、 [\_TCP\_オフロード\_現在の\_構成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)クエリに応答します。\_\_\_

 

中間ドライバーでのセットおよびクエリへの応答の詳細については、「[ミニポートドライバー情報の取得と設定」および「WMI の NDIS サポート](obtaining-and-setting-miniport-driver-information-and-ndis-support-for.md)」を参照してください。

 

 






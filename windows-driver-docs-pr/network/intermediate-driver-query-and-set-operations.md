---
title: 中間ドライバーのクエリおよび設定操作
description: 中間ドライバーのクエリおよび設定操作
ms.assetid: 68576241-20c1-4df4-ab2e-20ab89e67763
keywords:
- 中間ドライバー WDK ネットワーク、クエリ操作
- NDIS 中間ドライバー WDK、クエリ操作
- 中間ドライバー WDK ネットワーク, 設定操作
- NDIS 中間ドライバー WDK、set 操作
- クエリ操作 WDK NDIS 中間
- set 操作 WDK NDIS 中間
- Oid WDK ネットワーク、中間ドライバーのクエリおよびセット
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8162f7cdda0a3499b87164a932171aface96ae4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844181"
---
# <a name="intermediate-driver-query-and-set-operations"></a>中間ドライバーのクエリおよび設定操作





基になるミニポートアダプターに正常にバインドされ、その仮想ミニポートが初期化されると、中間ドライバーは、基になるミニポートアダプターの動作特性に対してクエリを実行し、独自の内部状態を設定します。 必要に応じて、中間ドライバーも、基になるミニポートアダプターを使用したバインディングの先読みバッファーサイズとして、このようなパラメーターをネゴシエートします。 基になるミニポートアダプターに関連付けられているほとんどの属性は、 [*Protocolbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)関数の*bindparameters*パラメーターで中間ドライバーに渡されます。 中間ドライバーは、可能であれば、OID クエリを発行する代わりに、 *Protocolbindadapterex*に渡される値を使用する必要があります。 ただし、コネクションレスのエッジがある中間ドライバーは、 [**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)を呼び出すことによって OID クエリを発行できます。 接続指向のエッジを持つ中間ドライバーは、 [**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)を呼び出すことによって OID クエリを発行できます。

中間ドライバーは、 [*Miniportoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)関数を介して、上位レベルのドライバーからクエリを受信したり、要求を設定したりすることもできます。 ドライバーは、これらの要求に応答するか、基になるドライバーに渡すことができます。 中間ドライバーがクエリと設定にどのように応答するかは、実装によって異なります。

また、中間ドライバーの動作は、仮想ミニポートおよび基になるミニポートドライバーの電源状態によっても影響を受けること**が  ます**。 クエリおよびセット操作の電源状態の影響の詳細については、「 [Set Power Request の処理](handling-a-set-power-request.md)」を参照してください。

 

「ネットワーク参照」セクションには、汎用、接続指向、メディア固有ではない Oid、中間ドライバー開発者にとって必要なメディア固有の Oid に関する情報が含まれています。

次のトピックでは、中間ドライバーでのクエリとセットの発行と応答に関する追加情報を提供します。

[中間ドライバーからの Set 要求とクエリ要求の発行](issuing-set-and-query-requests-from-an-intermediate-driver.md)

[中間ドライバーでのセットおよびクエリへの応答](responding-to-sets-and-queries-in-an-intermediate-driver.md)

 

 






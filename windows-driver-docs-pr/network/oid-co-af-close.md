---
title: OID_CO_AF_CLOSE
description: このトピックでは、OID_CO_AF_CLOSE オブジェクト識別子 (OID) について説明します。
ms.assetid: 451ab9d5-e118-41c9-8d16-02d75a25a1d4
keywords:
- OID_CO_AF_CLOSE
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: ccb7a8665955f5a8bf265921b57ecff9eeab390c
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916626"
---
# <a name="oid_co_af_close"></a>OID_CO_AF_CLOSE

OID_CO_AF_CLOSE OID は、基になるミニポートドライバーから自身をバインド解除する必要がある呼び出しマネージャーによって送信されます。 コールマネージャーは、ポートをミニポートドライバーからバインド解除する前に、呼び出しマネージャーでアドレスファミリが開かれている各クライアントにこの OID を送信します。 応答として、クライアントは次の操作を行う必要があります。

1. クライアントにアクティブな multipoint 接続がある場合は、各 multipoint VC で1つのパーティだけがアクティブなままになるまで、必要な回数だけ[NdisClDropParty](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscldropparty)を呼び出します。

2. 呼び出しマネージャーで開いたままになっているすべての呼び出しを閉じるには、必要な回数だけ[NdisClCloseCall](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclclosecall)を呼び出します。

3. クライアントが呼び出しマネージャーに登録したすべての Sap の登録を解除するために、必要な回数だけ[NdisClDeregisterSap](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclderegistersap)を呼び出します。

4. [NdisClCloseAddressFamily](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclcloseaddressfamily)を呼び出して、含まれている要求の NdisAfHandle によって参照されているアドレスファミリを閉じ OID_CO_AF_CLOSE

## <a name="requirements"></a>要件

**バージョン**: Windows Vista 以降の**ヘッダー**: Ntddndis (Ndis .h を含む)


---
title: OID_CO_AF_CLOSE
description: このトピックでは、OID_CO_AF_CLOSE オブジェクト識別子 (OID) について説明します。
ms.assetid: 451ab9d5-e118-41c9-8d16-02d75a25a1d4
keywords:
- OID_CO_AF_CLOSE
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: f721fe5a63f4859ded6bf76744a6f3c605569dfa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67357667"
---
# <a name="oidcoafclose"></a>OID_CO_AF_CLOSE

OID_CO_AF_CLOSE OID は、基になるミニポート ドライバーからの自体をバインド解除する必要がありますをコール マネージャーによって送信されます。 自体をバインド解除、ミニポート ドライバーから、前に、コール マネージャーは、この OID をコール マネージャーで開き、アドレス ファミリを持つ各クライアントに送信します。 応答、クライアントは、以下を実行します。

1. クライアントに multipoint のアクティブな接続がある場合は、呼び出す[NdisClDropParty](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscldropparty)として 1 つのパーティのみが、各 multipoint VC のアクティブなままになるまでに必要な回数

2. 呼び出す[NdisClCloseCall](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclclosecall)を閉じる必要な回数呼び出しはすべてまだ開いての呼び出しでマネージャー

3. 呼び出す[NdisClDeregisterSap](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclderegistersap)コール マネージャーで、クライアントが登録されているすべての Sap の登録を解除するために必要なだけ多くの回数

4. 呼び出す[NdisClCloseAddressFamily](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclcloseaddressfamily) OID_CO_AF_CLOSE に含まれている要求で NdisAfHandle によって参照されるアドレス ファミリを閉じる

## <a name="requirements"></a>必要条件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |


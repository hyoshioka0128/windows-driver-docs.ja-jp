---
title: 中間ドライバーのアンロード
description: 中間ドライバーのアンロード
ms.assetid: e3c1dad4-4262-4449-8dcd-2e2f5d6c8e25
keywords:
- NDIS 中間ドライバー WDK、アンロード
- 中間ドライバー WDK ネットワーク、アンロード
- 中間ドライバーのアンロード
- WDK NDIS 中間のインストールまたはアンインストール後にクリーンアップする
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5253108da412b58b7e7bb5c135f8637e8c66a038
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843005"
---
# <a name="unloading-an-intermediate-driver"></a>中間ドライバーのアンロード





NDIS は、 [*Miniportdriverunload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_unload)関数を呼び出して中間ドライバーをアンロードします。 中間ドライバーは、他のミニポートドライバーと同じように、 *Miniportdriverunload*で同じ操作を実行する必要があります。 [**NdisMDeregisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterminiportdriver)関数を呼び出すだけでなく、中間ドライバーも[**NdisDeregisterProtocolDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisderegisterprotocoldriver)を呼び出します。 また、 *Miniportdriverunload*は、任意の必要なクリーンアップ操作 (プロトコルドライバーリソースの割り当て解除など) を実行する必要があります。

中間ドライバーをアンインストールする前にクリーンアップ操作を実行するために、中間ドライバーは[*Protocoluninstall*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_uninstall)関数を登録できます。 たとえば、中間ドライバーの低エッジプロトコルには*Protocoluninstall*関数が必要になる場合があります。 中間ドライバーは、NDIS が*Miniportdriverunload*関数を呼び出す前に、 *protocoluninstall*でそのプロトコルエッジリソースを解放できます。

ミニポート中間ドライバーは、 **NdisMDeregisterMiniportDriver**を2回呼び出します。物理デバイスインターフェイスの場合は1回、仮想デバイスインターフェイスの場合は再びを呼び出します。

 

 






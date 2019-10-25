---
title: CoNDIS ミニポート ドライバー登録
description: CoNDIS ミニポート ドライバー登録
ms.assetid: 2dfd3bdc-b7b1-4491-b05e-2e8e1f5895b8
keywords:
- ミニポートドライバー WDK ネットワーク、CoNDIS
- NDIS ミニポートドライバー WDK、CoNDIS
- ミニポートドライバーの登録
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63dbee2037390337c9beb4cb9ecd6735206e7118
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838192"
---
# <a name="condis-miniport-driver-registration"></a>CoNDIS ミニポート ドライバー登録





CoNDIS ミニポートドライバーは、他のミニポートドライバーと同様に初期化され、追加の CoNDIS entry ポイントも登録する必要があります。 ミニポートドライバーの初期化に関する一般的な情報については、「[ミニポートドライバーの初期化](initializing-a-miniport-driver.md)」を参照してください。

*Miniportxxx*関数の condis エントリポイントを登録するには、 [**Condis**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)関数を[*MiniportSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)関数から呼び出します。 *MiniportSetOptions*では、ミニポートドライバーは、 [**NDIS\_ミニポート\_CO\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_co_characteristics)の構造を初期化し、それを**NdisSetOptionalHandlers**のパラメーター化された*ハンドラー*パラメーターに渡します。

ミニポート呼び出しマネージャー (MCMs) は、 *MiniportSetOptions*で*protocolxxx*関数も登録します。 MCM ドライバーの登録の詳細については、「 [CONMCM の登録](condis-mcm-registration.md)」を参照してください。

オプションのミニポートドライバーサービスの構成の詳細については、「[オプションのミニポートドライバーサービスの構成](configuring-optional-miniport-driver-services.md)」を参照してください。

 

 






---
title: CoNDIS MCM 登録
description: CoNDIS MCM 登録
ms.assetid: 7dfb86c5-e7b6-4b9d-8f29-a6d247500c3e
keywords:
- MCMs WDK ネットワーク, CoNDIS ミニポート呼び出しマネージャーの登録
- ミニポート呼び出しマネージャー WDK ネットワーク, CoNDIS ミニポート呼び出しマネージャーの登録
- ミニポートコールマネージャーを登録しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95bb6c9e2afdac94f6bcf637827399f6b09b7f3d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838189"
---
# <a name="condis-mcm-registration"></a>CoNDIS MCM 登録





Condis ミニポート呼び出しマネージャー (MCMs) は、他のミニポートドライバーと同様に初期化され、追加の CoNDIS entry ポイントも登録する必要があります。 ミニポートドライバーの初期化に関する一般的な情報については、「[ミニポートドライバーの初期化](initializing-a-miniport-driver.md)」を参照してください。

*Miniportxxx*関数と*protocolxxx*関数の condis エントリポイントを登録するには、 [**condis**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)関数を[*MiniportSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)関数から呼び出します。 *MiniportSetOptions*では、mcm によって[**NDIS\_ミニポート\_CO\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_co_characteristics)の構造が初期化され、それが**NdisSetOptionalHandlers**のパラメーター化された*ハンドラー*パラメーターに渡されます。

呼び出しマネージャーのエントリポイントを登録するために、MCMs は、 [**NDIS\_CO\_呼び出し\_マネージャー\_オプションの\_ハンドラー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_co_call_manager_optional_handlers)構造体を初期化し、 **NdisSetOptionalHandlers**のオプションの*ハンドラー*パラメーターに渡します。

オプションのミニポートドライバーサービスの構成の詳細については、「[オプションのミニポートドライバーサービスの構成](configuring-optional-miniport-driver-services.md)」を参照してください。

 

 






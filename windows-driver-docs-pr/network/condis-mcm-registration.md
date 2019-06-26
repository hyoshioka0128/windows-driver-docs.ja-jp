---
title: CoNDIS MCM 登録
description: CoNDIS MCM 登録
ms.assetid: 7dfb86c5-e7b6-4b9d-8f29-a6d247500c3e
keywords:
- MCMs WDK ネットワー キング、いる CoNDIS ミニポート コール マネージャーを登録します。
- ミニポート呼び出すマネージャー WDK ネットワー キング、いる CoNDIS ミニポート呼び出しを登録マネージャー
- ミニポート コール マネージャーを登録します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d989983df77e069d5d65bebdea05717d3d24e98
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379233"
---
# <a name="condis-mcm-registration"></a>CoNDIS MCM 登録





いる CoNDIS ミニポート コール マネージャー (MCMs) は、他のミニポート ドライバーのように初期化しも追加いる CoNDIS エントリ ポイントを登録する必要があります。 ミニポート ドライバーの初期化の詳細については、次を参照してください。[ミニポート ドライバーの初期化](initializing-a-miniport-driver.md)します。

いる CoNDIS エントリ ポイントを登録する*MiniportXxx*関数と*ProtocolXxx*関数、いる CoNDIS MCMs 呼び出し、 [ **NdisSetOptionalHandlers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissetoptionalhandlers)関数を[ *MiniportSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)関数。 *MiniportSetOptions*、MCM を初期化します、 [ **NDIS\_ミニポート\_CO\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_co_characteristics)構造体を渡します*OptionalHandlers*パラメーターの**NdisSetOptionalHandlers**します。

MCMs の初期化呼び出し manager エントリ ポイントを登録する、 [ **NDIS\_CO\_呼び出す\_MANAGER\_(省略可能)\_ハンドラー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_co_call_manager_optional_handlers)構造体し、渡すことで、 *OptionalHandlers*パラメーターの**NdisSetOptionalHandlers**します。

省略可能なミニポート ドライバー サービスを構成する方法の詳細については、次を参照してください。[省略可能なミニポート ドライバー サービスを構成する](configuring-optional-miniport-driver-services.md)します。

 

 






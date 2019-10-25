---
title: CoNDIS コール マネージャー登録
description: CoNDIS コール マネージャー登録
ms.assetid: 63cde3d1-122c-4411-91b6-97e97bdd2df3
keywords:
- 呼び出しマネージャー WDK ネットワーク、CoNDIS
- 登録 (呼び出しマネージャーを)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89af22a9d73619c8379f752cb23deaab4f65ab1b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835145"
---
# <a name="condis-call-manager-registration"></a>CoNDIS コール マネージャー登録





CoNDIS スタンドアロンの呼び出しマネージャーは、他のプロトコルドライバーと同様に初期化し、追加の CoNDIS entry ポイントも登録する必要があります。 プロトコルドライバーの初期化に関する一般的な情報については、「[プロトコルドライバーの初期化](initializing-a-protocol-driver.md)」を参照してください。

*Protocolxxx*関数の condis エントリポイントを登録するには、呼び出し[**マネージャーが**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers) [*ProtocolSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)関数から関数を呼び出します。 *ProtocolSetOptions*では、すべての condis プロトコルドライバーが[ **\_CO\_の特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_protocol_co_characteristics)の構造を初期化し、それを**NdisSetOptionalHandlers**の\_のパラメーターに渡します。

呼び出しマネージャーのエントリポイントを指定するために、プロトコルドライバーは、 [**NDIS\_CO\_呼び出し\_マネージャー\_オプションの\_ハンドラー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_co_call_manager_optional_handlers)構造体を初期化し、のオプションの**ハンドラーパラメーターに渡します。NdisSetOptionalHandlers**。

ミニポート呼び出しマネージャー (MCMs) は、呼び出しマネージャーの*Protocolxxx*関数も登録します。 MCM ドライバーの登録の詳細については、「 [CONMCM の登録](condis-mcm-registration.md)」を参照してください。

オプションのプロトコルドライバーサービスの構成の詳細については、「[オプションのプロトコルドライバーサービスの構成](configuring-optional-protocol-driver-services.md)」を参照してください。

 

 






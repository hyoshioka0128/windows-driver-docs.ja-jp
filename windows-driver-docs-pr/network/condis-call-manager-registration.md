---
title: CoNDIS コール マネージャー登録
description: CoNDIS コール マネージャー登録
ms.assetid: 63cde3d1-122c-4411-91b6-97e97bdd2df3
keywords:
- コール マネージャーの WDK ネットワー キング、いる CoNDIS
- 呼び出しのマネージャーを登録します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a8b7f870cfe66c8cc3d131ed85b072d8240b0ca
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379254"
---
# <a name="condis-call-manager-registration"></a>CoNDIS コール マネージャー登録





スタンドアロンいる CoNDIS などその他のプロトコルのドライバー マネージャー、initialize を呼び出すしも追加いる CoNDIS エントリ ポイントを登録する必要があります。 プロトコル ドライバーの初期化の詳細については、次を参照してください。[プロトコル ドライバーの初期化](initializing-a-protocol-driver.md)します。

いる CoNDIS エントリ ポイントを登録する*ProtocolXxx*関数呼び出しマネージャー呼び出し、 [ **NdisSetOptionalHandlers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissetoptionalhandlers)関数を[ *ProtocolSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)関数。 *ProtocolSetOptions*、いる CoNDIS プロトコルのすべてのドライバーが初期化、 [ **NDIS\_プロトコル\_CO\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_protocol_co_characteristics)構造体し、渡すことで、 *OptionalHandlers*パラメーターの**NdisSetOptionalHandlers**します。

プロトコル ドライバーの初期化をコール マネージャーのエントリ ポイントを指定する、 [ **NDIS\_CO\_呼び出す\_MANAGER\_(省略可能)\_ハンドラー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_co_call_manager_optional_handlers)を構造化し、これで、 *OptionalHandlers*パラメーターの**NdisSetOptionalHandlers**します。

ミニポート マネージャー (MCMs) も登録呼び出し manager 呼び出し*ProtocolXxx*関数。 MCM ドライバーの登録の詳細については、次を参照してください。[いる CoNDIS MCM 登録](condis-mcm-registration.md)します。

省略可能なプロトコル ドライバー サービスを構成する方法の詳細については、次を参照してください。[省略可能なプロトコル ドライバー サービスを構成する](configuring-optional-protocol-driver-services.md)します。

 

 






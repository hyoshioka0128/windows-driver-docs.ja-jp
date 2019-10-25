---
title: CoNDIS クライアント登録
description: CoNDIS クライアント登録
ms.assetid: 335dd117-f6c8-4416-8527-ff64c1a5f3ee
keywords:
- クライアント登録 WDK の場合
- 登録 (エントリポイントを)
- エントリポイント WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 899b880e56b1f87d3a33c18e027e2d2272c44a15
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838193"
---
# <a name="condis-client-registration"></a>CoNDIS クライアント登録





Condis クライアントは他のプロトコルドライバーと同様に初期化され、追加の CoNDIS entry ポイントも登録する必要があります。 プロトコルドライバーの初期化に関する一般的な情報については、「[プロトコルドライバーの初期化](initializing-a-protocol-driver.md)」を参照してください。

*Protocolxxx*関数の condis エントリポイントを登録するには、 [**Condis**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)関数を[*ProtocolSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)関数から呼び出します。 *ProtocolSetOptions*では、すべての condis プロトコルドライバーが[ **\_CO\_の特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_protocol_co_characteristics)の構造を初期化し、それを**NdisSetOptionalHandlers**の\_のパラメーターに渡します。

CoNDIS クライアントのエントリポイントを指定するために、プロトコルドライバーは、 [**NDIS\_CO\_クライアント\_オプションの\_ハンドラー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_co_client_optional_handlers)構造体を初期化し、のオプションの**ハンドラーパラメーターに渡します。NdisSetOptionalHandlers**。

オプションのプロトコルドライバーサービスの構成の詳細については、「[オプションのプロトコルドライバーサービスの構成](configuring-optional-protocol-driver-services.md)」を参照してください。

 

 






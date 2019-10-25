---
title: CoNDIS 登録
description: CoNDIS 登録
ms.assetid: 6db5a4a2-f090-4688-99fa-9d22ca7077ed
keywords:
- CoNDIS WDK ネットワーク、登録
- CoNDIS ドライバーの登録
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7d9d118f8e499ac1dd66b8b669f91bbb905e681
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838187"
---
# <a name="condis-registration"></a>CoNDIS 登録





Condis をサポートするには、NDIS ドライバーでオプションの CoNDIS 関数のエントリポイントを登録する必要があります。 NDIS ドライバーは、 [**NdisSetOptionalHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)関数を呼び出して、オプションのサービスを登録します。

ここでは、次のトピックについて説明します。

[ポートのドライバー登録を切断する](condis-miniport-driver-registration.md)

[クライアント登録の解除](condis-client-registration.md)

[CoNDIS Manager の登録](condis-call-manager-registration.md)

[Conmcm の登録](condis-mcm-registration.md)

 

 






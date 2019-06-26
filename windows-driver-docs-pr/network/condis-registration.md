---
title: CoNDIS 登録
description: CoNDIS 登録
ms.assetid: 6db5a4a2-f090-4688-99fa-9d22ca7077ed
keywords:
- ネットワーク、いる CoNDIS WDK 登録
- 登録している CoNDIS ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c02d91031d87c33fe723027f893af0cd745cfc54
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385099"
---
# <a name="condis-registration"></a>CoNDIS 登録





いる CoNDIS をサポートするには、NDIS ドライバーは、省略可能ないる CoNDIS 関数のエントリ ポイントを登録する必要があります。 NDIS ドライバー呼び出し、 [ **NdisSetOptionalHandlers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissetoptionalhandlers)省略可能なサービスを登録する関数。

ここでは、次のトピックについて説明します。

[いる CoNDIS ミニポート ドライバーの登録](condis-miniport-driver-registration.md)

[いる CoNDIS クライアントの登録](condis-client-registration.md)

[いる CoNDIS 呼び出すマネージャーの登録](condis-call-manager-registration.md)

[いる CoNDIS MCM の登録](condis-mcm-registration.md)

 

 






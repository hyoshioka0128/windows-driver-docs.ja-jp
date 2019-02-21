---
title: いる CoNDIS 登録
description: いる CoNDIS 登録
ms.assetid: 6db5a4a2-f090-4688-99fa-9d22ca7077ed
keywords:
- ネットワーク、いる CoNDIS WDK 登録
- 登録している CoNDIS ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0449cb59335274dac5d1f51000918b27d95be131
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550927"
---
# <a name="condis-registration"></a>いる CoNDIS 登録





いる CoNDIS をサポートするには、NDIS ドライバーは、省略可能ないる CoNDIS 関数のエントリ ポイントを登録する必要があります。 NDIS ドライバー呼び出し、 [ **NdisSetOptionalHandlers** ](https://msdn.microsoft.com/library/windows/hardware/ff564550)省略可能なサービスを登録する関数。

ここでは、次のトピックについて説明します。

[いる CoNDIS ミニポート ドライバーの登録](condis-miniport-driver-registration.md)

[いる CoNDIS クライアントの登録](condis-client-registration.md)

[いる CoNDIS 呼び出すマネージャーの登録](condis-call-manager-registration.md)

[いる CoNDIS MCM の登録](condis-mcm-registration.md)

 

 






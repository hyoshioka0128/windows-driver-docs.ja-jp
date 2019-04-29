---
title: NDIS ドライバーの種類
description: NDIS ドライバーの種類
ms.assetid: ed7bd8b4-75d5-4ecd-beb2-df8ac1ce96b3
keywords:
- ネットワーク ドライバー WDK、NDIS ドライバー
- NDIS WDK では、サポートされているドライバーの種類
ms.date: 11/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: eff0dd928da2288cc50f5ae3af963279885d2a19
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392925"
---
# <a name="ndis-driver-types"></a>NDIS ドライバーの種類

Network Driver Interface Specification (NDIS) ライブラリは、ネットワーク ドライバーからのネットワーク ハードウェアを抽象化します。 NDIS には、複数層のネットワーク ドライバー、それによってネットワーク トランスポートなどの上位レベルのドライバーからハードウェアを管理する下位レベルのドライバーを抽象化の間の標準のインターフェイスも指定します。 NDIS は、状態情報とネットワーク ドライバーは、関数、ハンドル、およびリンケージのパラメーター要素およびその他のシステム値へのポインターを含むパラメーターにも保持されます。

NDIS には、次の主な種類のネットワーク ドライバーがサポートされています。

-   [ミニポート ドライバー](ndis-miniport-drivers2.md)

-   [プロトコル ドライバー](ndis-protocol-drivers2.md)

-   [フィルター ドライバー](ndis-filter-drivers.md)

-   [中間ドライバー](ndis-intermediate-drivers.md)

>[!NOTE]
> これらのトピックでは、NDIS ドライバーの各種類は個別にについて詳しく説明します。 NDIS ドライバー スタックと 4 つすべての NDIS ドライバーの種類間のリレーションシップを示す図の詳細については、次を参照してください。 [NDIS ドライバー スタック](ndis-driver-stack.md)します。
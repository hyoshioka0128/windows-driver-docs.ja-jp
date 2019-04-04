---
title: NDIS 6.30 ドライバーの実装
description: NDIS 6.30 ドライバーの実装
ms.assetid: B1B48ED9-10F1-45F2-AA7C-270B637B5A36
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d34c941d4e2db744e01fc54965591ac0912350e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571485"
---
# <a name="implementing-an-ndis-630-driver"></a>NDIS 6.30 ドライバーの実装


NDIS 6.30、ドライバーがで定義されている要件に従う必要があります[NDIS ドライバー 6.20 が動作を実装する](implementing-an-ndis-6-20-driver.md)します。

さらに、NDIS 6.30 ドライバーは、次の要件に準拠する必要があります。

-   NDIS 6.30 ドライバーは、NDIS に登録する際に、正しい NDIS バージョンを報告する必要があります。

    NDIS のメジャーおよびマイナー NDIS バージョン番号を更新する必要があります\_*Xxx*\_ドライバー\_サポート NDIS 6.30 特性構造体。 **MajorNdisVersion**メンバーを含める必要があります**6**と**MinorNdisVersion**メンバーを含める必要があります**30**します。 この要件は、ミニポート、プロトコル、およびフィルター ドライバーに適用されます。 バージョン情報を更新する必要がありますも、コンパイラでは、[NDIS 6.30 ドライバーをコンパイルする](compiling-an-ndis-6-30-driver.md)を参照してください。

-   NDIS と関連付けたドライバー デバイスとドライバーの機能、NDIS 6.30 に通知するためには、ドライバーは、次の機能の NDIS 6.30 デバイス機能インターフェイスを実装する必要があります。

    -   [仮想化ネットワーク](virtualized-networking-enhancements-in-ndis-6-30.md)

    -   [電源管理](power-management-enhancements-in-ndis-6-30.md)

    -   [NDIS サービスの品質 (QoS)](quality-of-service--qos--support-in-ndis-6-30.md)

-   Windows 8 および Windows Server 2012 オペレーティング システム用の NDIS 6.30 ミニポート ドライバーでは、データ構造の NDIS 6.30 バージョンを使用する必要があります。 詳細については、[NDIS 6.30 データ構造体を使用して](using-ndis-6-30-data-structures.md)を参照してください。

 

 






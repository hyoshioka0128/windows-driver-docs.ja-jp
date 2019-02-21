---
title: WAN いる CoNDIS ほど複雑では
description: WAN いる CoNDIS ほど複雑では
ms.assetid: 750f321a-72c9-4d90-b02e-cbe5177dc2af
keywords:
- いる CoNDIS WAN ドライバー WDK ネットワーク、利点があります。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15d060329cdcc7d3166b6196f7c62cada81f8ea8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550948"
---
# <a name="condis-wan-is-less-complex"></a>WAN いる CoNDIS ほど複雑では





いる CoNDIS は、各接続に関連する論理エンティティに対応するオブジェクトを定義します。 これらのエンティティには、アドレス ファミリ (AFs)、仮想接続 (VCs)、サービス アクセス ポイント (Sap)、およびパーティが含まれます。

いる CoNDIS 環境では、システムは、TAPI の複雑な要件の多くを処理します。 そのため、いる CoNDIS WAN ミニポート ドライバーまたは MCM をする必要はありません、NDIS WAN ミニポート ドライバーと同数の TAPI Oid を処理します。 さらに、いる CoNDIS WAN ミニポート ドライバーまたは MCM は、次の状態インジケーターを処理するためには必要ありません。

-   NDIS\_状態\_TAPI\_を示す値

-   NDIS\_状態\_WAN\_行\_を

-   NDIS\_状態\_WAN\_行\_ダウン

コール マネージャーとミニポート ドライバーの機能の分離では、2 つの簡単なドライバーを実装することができます。 簡略化されたドライバーを維持し、1 つの大規模で複雑なドライバーよりもデバッグが簡単になります。

 

 






---
title: CoNDIS WAN は複雑でない
description: CoNDIS WAN は複雑でない
ms.assetid: 750f321a-72c9-4d90-b02e-cbe5177dc2af
keywords:
- いる CoNDIS WAN ドライバー WDK ネットワーク、利点があります。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15d060329cdcc7d3166b6196f7c62cada81f8ea8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390731"
---
# <a name="condis-wan-is-less-complex"></a>CoNDIS WAN は複雑でない





いる CoNDIS は、各接続に関連する論理エンティティに対応するオブジェクトを定義します。 これらのエンティティには、アドレス ファミリ (AFs)、仮想接続 (VCs)、サービス アクセス ポイント (Sap)、およびパーティが含まれます。

いる CoNDIS 環境では、システムは、TAPI の複雑な要件の多くを処理します。 そのため、いる CoNDIS WAN ミニポート ドライバーまたは MCM をする必要はありません、NDIS WAN ミニポート ドライバーと同数の TAPI Oid を処理します。 さらに、いる CoNDIS WAN ミニポート ドライバーまたは MCM は、次の状態インジケーターを処理するためには必要ありません。

-   NDIS\_状態\_TAPI\_を示す値

-   NDIS\_状態\_WAN\_行\_を

-   NDIS\_状態\_WAN\_行\_ダウン

コール マネージャーとミニポート ドライバーの機能の分離では、2 つの簡単なドライバーを実装することができます。 簡略化されたドライバーを維持し、1 つの大規模で複雑なドライバーよりもデバッグが簡単になります。

 

 






---
title: いる CoNDIS WAN がより柔軟です
description: いる CoNDIS WAN がより柔軟です
ms.assetid: 01f4d5cc-3ecc-4d2f-bc19-67b8d0fda52f
keywords:
- いる CoNDIS WAN ドライバー WDK ネットワーク、利点があります。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f6747502d3fbbcb2df0042f3523addd5fad2d92
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559962"
---
# <a name="condis-wan-is-more-flexible"></a>いる CoNDIS WAN がより柔軟です





いる CoNDIS モデルで (呼び出しの管理とデータ転送) などの主要機能は、独立したコンポーネントまたはサブコンポーネントに区分化します。 この組織では、システムが提供およびサード パーティ製のコンポーネントを使用して、機能をより簡単に更新できます。

いる CoNDIS モデルでは、次の 4 つの種類のドライバーを提供します。

-   接続指向のクライアント ドライバー

-   コール マネージャー

-   接続指向のミニポート ドライバー

-   統合ミニポート コール マネージャー (MCMs)

いる CoNDIS ドライバーの詳細については、次を参照してください。 [Connection-Oriented NDIS](connection-oriented-ndis.md)します。

コール マネージャーとミニポート ドライバー コンポーネントの分離では、コール マネージャーをそのままにしたまま、新しいハードウェアをサポートするために、ミニポート ドライバーを更新することができます。 多くの場合、コール マネージャーには欠陥を修正するだけのアップグレードが必要です。

アーキテクチャのコンポーネントの分離は、MCM で明確に定義されています。 MCM のコール マネージャーのサブコンポーネントが、接続のシグナリングの側面を処理し、いる CoNDIS WAN ミニポート ドライバーのサブコンポーネントは NIC ハードウェアを処理します。

システム提供のコール マネージャーを使用することができます。 場合、システムは、メディアの種類 (と同様、ISDN など) にコール マネージャーを提供しないと、1 つを作成したり、可能性があるサード パーティから取得できます。

Microsoft Windows オペレーティング システムには、PPP いる CoNDIS クライアントが含まれています、いる CoNDIS WAN ミニポート ドライバーは多くのデバイスで利用可能です。 PPP だけでなく他のプロトコルのドライバーをサポートするためにシステムを拡張するクライアントが WAN いる CoNDIS を記述することができます。

いる CoNDIS WAN のモデルでは、PPP データに制限されません。 カスタムの WAN クライアント ドライバーとミニポート ドライバーを処理する、生データのストリーミングまたは独自の暗号化を実装することができます。

 

 






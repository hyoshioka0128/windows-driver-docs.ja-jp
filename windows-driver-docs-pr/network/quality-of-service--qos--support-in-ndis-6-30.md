---
title: NDIS 6.30 のサービスの品質 (QoS) のサポート
description: NDIS 6.30 のサービスの品質 (QoS) のサポート
ms.assetid: B425C05C-0F65-4F94-AECD-0BAD35DA441F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5411b0ee5d87e8b6575023e04d2cc8995bc1478e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578922"
---
# <a name="quality-of-service-qos-support-in-ndis-630"></a>NDIS 6.30 のサービスの品質 (QoS) のサポート


NDIS 6.30 以降では、サービスの品質 (QoS) のサポートを提供します。 ミニポート ドライバーでは、NDIS QoS を使用して、トラフィックの優先順位付けの送信、または*エグレス*パケットに IEEE 802.1 データ センター ブリッジング (DCB) に準拠したネットワーク アダプターを経由します。

IEEE 802.1 データ センター ブリッジング (DCB) は、統一された 802.3 を定義する一連の標準のイーサネット メディア インターフェイス、またはファブリック、ローカル エリア ネットワーク (LAN) および記憶域エリア ネットワーク (SAN) のテクノロジです。 DCB は、データ センター内で同じネットワーク ファブリック経由で LAN、SAN ベースのアプリケーションの共存をサポートする仕様をブリッジ現在 802.1 を拡張します。 DCB には、パケット損失を防止するリンク レベルのポリシーを定義することで Fibre Channel over Ethernet (FCoE)、iSCSI などのテクノロジもサポートしています。

DCB の NDIS QoS のサポートには、ポリシーのセットを指定するトラフィック クラスで構成されるミニポート ドライバーができます。 各ポリシーでは、ネットワーク アダプターが送信パケットの優先順位の高い配信を処理する方法を決定します。

トラフィック クラスごとには、送信パケットに適用される次のポリシーを指定します。

<a href="" id="priority-level-and-flow-control"></a>優先度レベルとフロー制御  
このポリシーは、エグレス トラフィックの IEEE 802.1p の優先度レベルと省略可能なフロー コントロール アルゴリズムを定義します。

<a href="" id="traffic-selection-algorithms--tsas-"></a>トラフィックの選択アルゴリズム (TSAs)  
このポリシーは、ネットワーク アダプターがその送信キューからの配信のエグレス トラフィックがどのように選択する方法を指定します。 たとえば、アダプターでは、IEEE 802.1p の優先度またはトラフィック クラスごとに割り当てられているエグレス帯域幅の割合に基づく送信パケットを選択できます。

DCB の NDIS QoS のサポートの詳細については、次を参照してください。[データ センター ブリッジングの NDIS QoS](ndis-qos-for-data-center-bridging.md)します。

 

 






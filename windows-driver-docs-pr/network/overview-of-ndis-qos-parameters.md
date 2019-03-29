---
title: NDIS QoS パラメーターの概要
description: NDIS QoS パラメーターの概要
ms.assetid: E9321805-2930-410A-81BC-F7978517E89E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bba212964084b2108dcf457ff4504d4529f32519
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578147"
---
# <a name="overview-of-ndis-qos-parameters"></a>NDIS QoS パラメーターの概要


NDIS のサービス品質 (QoS) パラメーターは、ポリシーとのネットワーク アダプターを使用してトラフィック クラスの設定を指定または*エグレス*、パケット配信します。 NDIS QoS パラメーターには、次の設定が含まれます。

-   優先度レベルとフローの設定を制御します。 これらの設定は、送信の IEEE 802.1p の優先度レベルと省略可能なフロー コントロール アルゴリズムを定義または*エグレス*トラフィック。

    詳細については、次を参照してください。[優先度レベルとフロー制御](priority-levels-and-flow-control.md)します。

-   トラフィックの選択アルゴリズム (TSA) 設定します。 これらの設定は、ネットワーク アダプターがその送信キューからのエグレス トラフィックを選択する方法を定義します。 たとえば、アダプターは、TSA の厳密な優先度を使用し、IEEE 802.1p の優先度のみに基づいて送信パケットを選択します。 アダプターは、Enhanced Transmission Selection (ETS)、帯域幅の割り当てに基づくトラフィック クラス間でのエグレス トラフィックに保ちます TSA も使用できます。

    詳細については、次を参照してください。[伝送選択アルゴリズム (TSAs)](transmission-selection-algorithms--tsas-.md)します。

-   トラフィックの分類を EtherType または宛先の TCP ポートなどの分類の条件に一致するデータを含むパケットに IEEE 802.1p の優先度レベルの割り当てを指定します。 詳細については、次を参照してください。 [NDIS QoS トラフィックの分類](ndis-qos-traffic-classifications.md)します。

    **注**  トラフィックの分類は、IEEE 802.1 仕様で「アプリケーションの優先順位」でとも呼ばれます。

     

NDIS QoS では、次の種類のパラメーターを定義します。

<a href="" id="local-ndis-qos-parameters"></a>ローカルの NDIS QoS パラメーター  
ローカルの NDIS QoS パラメーターは、ミニポート ドライバーとそのネットワーク アダプターの主要な QoS 設定を指定します。 これらのパラメーターは、システム レジストリに保存され、次のように、ミニポート ドライバーをローカルに管理します。

-   NDIS オブジェクト識別子 (OID) メソッドの要求を通じて[OID\_QOS\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/hh451835) DCB コンポーネントによって発行されました。 この OID 要求に含まれる、 [ **NDIS\_QOS\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451640)をローカルの NDIS QoS パラメーターを指定します。

    DCB のコンポーネントの詳細については、次を参照してください。[データ センター ブリッジングの NDIS QoS アーキテクチャ](ndis-qos-architecture-for-data-center-bridging.md)します。

-   ネットワーク アダプターの独自のレジストリ設定。 ミニポート ドライバーがこれらの設定を読み取るときにその[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389) NDIS によって呼び出されます。

-   独立系ハードウェア ベンダー (IHV) によって開発された管理アプリケーションを通じてミニポート ドライバーに発行された設定。

ミニポート ドライバーが、ローカルの NDIS QoS パラメーターを取得する方法の詳細については、次を参照してください。 [NDIS QoS パラメーターをローカル設定](setting-local-ndis-qos-parameters.md)します。

<a href="" id="remote-ndis-qos-parameters"></a>リモートの NDIS QoS パラメーター  
リモートの NDIS QoS パラメーターでは、データ リンクの上にネットワーク アダプターが接続されているリモート ピアに構成されているものです。 ミニポート ドライバーは、IEEE 802.1 qaz で指定されている Data Center Bridging Exchange (DCBX) プロトコルを使ってこれらのパラメーターを検出します。 ドラフト標準。

DCBX では、ミニポート ドライバーが 1 つのデータ リンクのピアから受信したリモートの QoS パラメーターの 1 つだけのセットを維持する必要があります。 ミニポート ドライバーは、そのリモートの QoS パラメーターは、最初に、ピアから受信したか、または後で変更時に、NDIS 状態を示す値を発行する必要があります。 たとえば、ドライバーは、そのリモート ピアからさまざまな一連の QoS パラメーターを受け取ったため、そのリモートの NDIS QoS パラメーターを変更可能性があります。 このプロセスの詳細については、次を参照してください。[リモートの NDIS QoS パラメーターを示す変更](indicating-changes-to-the-remote-ndis-qos-parameters.md)します。

ミニポート ドライバーが、リモートの NDIS QoS パラメーターを取得する方法の詳細については、次を参照してください。[リモートの NDIS QoS パラメーターを受け取る](receiving-remote-ndis-qos-parameters.md)します。

<a href="" id="operational-ndis-qos-parameters"></a>運用上の NDIS QoS パラメーター  
運用上の NDIS QoS パラメーターはリモート ピアのリンクのデータ接続経由でトラフィックの優先順位付けのミニポート ドライバーが解決することです。 ミニポート ドライバーは、ローカルまたはリモートの NDIS QoS パラメーターから、運用上の NDIS QoS パラメーターを解決します。

ミニポート ドライバーは、運用上の QoS パラメーターが最初に解決されますか、または後で変更時に NDIS 状態を示す値を発行する必要があります。 たとえば、ドライバーはそのリモート ピアからさまざまな一連の QoS パラメーターを受け取ったため、その運用上の NDIS QoS パラメーターを変更可能性があります。 この状態を示す値を生成する方法の詳細については、次を参照してください。[運用上の NDIS QoS パラメーターを示す変更](indicating-changes-to-the-operational-ndis-qos-parameters.md)します。

ミニポート ドライバーがその運用上の NDIS QoS パラメーターを解決する方法の詳細については、次を参照してください。[運用上の NDIS QoS パラメーターを解決する](resolving-operational-ndis-qos-parameters.md)します。

 

 






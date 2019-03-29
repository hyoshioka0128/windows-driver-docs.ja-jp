---
title: 稼働中の NDIS QoS パラメーターの解決
description: 稼働中の NDIS QoS パラメーターの解決
ms.assetid: F6C486B4-ABD5-413A-9E2D-283D83802C2B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 103d6b3425deaad36e9428ce5c55276acdf8db70
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572729"
---
# <a name="resolving-operational-ndis-qos-parameters"></a>稼働中の NDIS QoS パラメーターの解決


運用上の NDIS サービスの品質 (QoS) パラメーターでは、リモート ピアのリンクのデータ接続経由でトラフィックの優先順位を付け、ミニポート ドライバーを使用しているものです。 ミニポート ドライバーは、次の派生、または*解決*から、次のいずれかの操作の NDIS QoS パラメーター。

-   ミニポート ドライバーをローカルで管理されているローカルの NDIS QoS パラメーター。 ミニポート ドライバーがローカル QoS パラメーターを取得する方法の詳細については、次を参照してください。 [NDIS QoS パラメーターをローカル設定](setting-local-ndis-qos-parameters.md)します。

-   データ リンクをリモート ピアからミニポート ドライバーを受信するリモートの NDIS QoS パラメーター。 ミニポート ドライバーが、リモートの QoS パラメーターを取得する方法の詳細については、次を参照してください。[リモートの NDIS QoS パラメーターを受け取る](receiving-remote-ndis-qos-parameters.md)します。

ローカル、リモート、および運用上の NDIS QoS パラメーターは、次の種類のデータで構成されます。

-   優先度レベルとフローの設定を制御します。 これらの設定は、送信の IEEE 802.1p の優先度レベルと省略可能なフロー コントロール アルゴリズムを定義または*エグレス*トラフィック。

    詳細については、次を参照してください。[優先度レベルとフロー制御](priority-levels-and-flow-control.md)します。

-   トラフィックの選択アルゴリズム (TSA) 設定します。 これらの設定は、ネットワーク アダプターがその送信キューからのエグレス トラフィックを選択する方法を定義します。

    たとえば、アダプターは、TSA の厳密な優先度を使用し、IEEE 802.1p の優先度のみに基づいて送信パケットを選択します。 アダプターは、Enhanced Transmission Selection (ETS)、帯域幅の割り当てに基づくトラフィック クラス間でのエグレス トラフィックに保ちます TSA も使用できます。

    詳細については、次を参照してください。[伝送選択アルゴリズム (TSAs)](transmission-selection-algorithms--tsas-.md)します。

-   トラフィックの分類を EtherType または宛先の TCP ポートなどの分類の条件に一致するデータを含むパケットに IEEE 802.1p の優先度レベルの割り当てを指定します。 詳細については、次を参照してください。 [NDIS QoS トラフィックの分類](ndis-qos-traffic-classifications.md)します。

    **注**  トラフィックの分類は、IEEE 802.1 仕様で「アプリケーションの優先順位」でとも呼ばれます。

     

ミニポート ドライバーでは、次のガイドラインに従って、ローカルまたはリモートの NDIS QoS パラメーターから、操作の設定を解決します。

-   ローカル Data Center Bridging Exchange (DCBX) しようとして状態が有効になっている場合、ミニポート ドライバーは、リモートの QoS パラメーターから、運用の QoS パラメーターを解決する必要があります。

    ミニポート ドライバーがリモートの NDIS QoS パラメーターを処理する方法の詳細については、次を参照してください。[リモートの NDIS QoS パラメーターを受け取る](receiving-remote-ndis-qos-parameters.md)します。

-   ローカルの DCBX しようとして状態が無効になっている場合、ミニポート ドライバーは、ローカルの QoS パラメーターから、運用の QoS パラメーターを解決する必要があります。

    ミニポート ドライバーがローカルの NDIS QoS パラメーターを処理する方法の詳細については、次を参照してください。 [NDIS QoS パラメーターをローカル設定](setting-local-ndis-qos-parameters.md)します。

-   ミニポート ドライバーでは、独立系ハードウェア ベンダー (IHV) で定義されている独自の QoS 設定に基づいて、運用の QoS パラメーターを解決することもできます。 QoS パラメーターまたはローカル ピアが、オペレーティング システムによってリモートで構成されていないこのドライバーにはのみことができます。

-   ミニポート ドライバーは、運用上の QoS パラメーターが最初に解決されますか、または後で変更時に NDIS 状態を示す値を発行する必要があります。 たとえば、ドライバーはそのリモート ピアからさまざまな一連の QoS パラメーターを受け取ったため、その運用上の NDIS QoS パラメーターを変更可能性があります。 この状態を示す値を生成する方法の詳細については、次を参照してください。[運用上の NDIS QoS パラメーターを示す変更](indicating-changes-to-the-operational-ndis-qos-parameters.md)します。

ローカル DCBX の詳細については、状態のような場面を参照してください[DCBX 許容状態のローカル管理](managing-the-local-dcbx-willing-state.md)します。

QoS オペレーションのパラメーターを解決するために使用する方法の詳細については、IEEE 802.1 qaz を参照してくださいドラフト標準。

 

 






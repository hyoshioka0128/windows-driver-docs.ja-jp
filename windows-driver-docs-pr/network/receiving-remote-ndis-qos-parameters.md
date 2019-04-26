---
title: リモート NDIS QoS パラメーターの受け取り
description: リモート NDIS QoS パラメーターの受け取り
ms.assetid: 775FA8D7-ECF7-4F94-8958-C51D74243C3A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 280c19391778b6f92a354fcbca65e8d00c6b6c09
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349428"
---
# <a name="receiving-remote-ndis-qos-parameters"></a>リモート NDIS QoS パラメーターの受け取り


リモートの NDIS サービスの品質 (QoS) パラメーターは、データ リンクの上にネットワーク アダプターが接続されているリモート ピアから受信したものです。 ミニポート ドライバーは、IEEE 802.1 qaz で指定されている Data Center Bridging Exchange (DCBX) プロトコルを使ってこれらのパラメーターを検出します。 ドラフト標準。

ドライバーは、リモートの QoS パラメーターを管理するための次のガイドラインに従う必要があります。

-   ミニポート ドライバーを発行する必要があります、 [ **NDIS\_状態\_QOS\_リモート\_パラメーター\_変更**](https://msdn.microsoft.com/library/windows/hardware/hh439812)状態の表示時にそのリモートの NDIS QoS パラメーターは、最初に、ピアから受信したか、または後で変更します。 この手順の詳細については、次を参照してください。[リモートの NDIS QoS パラメーターを示す変更](indicating-changes-to-the-remote-ndis-qos-parameters.md)します。

-   ミニポート ドライバーでは、ネットワーク アダプターで、ローカル Data Center Bridging Exchange (DCBX) しようとして状態が有効になっている場合にのみ、その運用上の NDIS QoS パラメーターを解決するのには、リモートの NDIS QoS パラメーターを使用できます。 ミニポート ドライバーでは、独立系ハードウェア ベンダー (IHV) で定義されている独自の QoS 設定に基づいて、運用の QoS パラメーターを解決することもできます。

    この手順の詳細については、次を参照してください。[運用上の NDIS QoS パラメーターを解決する](resolving-operational-ndis-qos-parameters.md)します。

    ローカル DCBX の詳細については、状態のような場面を参照してください[DCBX 許容状態のローカル管理](managing-the-local-dcbx-willing-state.md)します。

NDIS QoS パラメーターの詳細については、次を参照してください。 [NDIS QoS パラメーターの概要](overview-of-ndis-qos-parameters.md)します。

 

 






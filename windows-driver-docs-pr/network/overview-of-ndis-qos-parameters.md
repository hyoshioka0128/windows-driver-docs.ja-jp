---
title: NDIS QoS パラメーターの概要
description: NDIS QoS パラメーターの概要
ms.assetid: E9321805-2930-410A-81BC-F7978517E89E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5dd9a4e97ad50a50b689b79a2c93ebb86c354f5e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843739"
---
# <a name="overview-of-ndis-qos-parameters"></a>NDIS QoS パラメーターの概要


NDIS Quality of Service (QoS) パラメーターは、ネットワークアダプターが送信または送信パケット*配信に使用*するトラフィッククラスのポリシーと設定を指定します。 NDIS QoS パラメーターには、次の設定が含まれます。

-   優先度レベルとフロー制御の設定。 これらの設定は、送信*トラフィックまたは*送信トラフィックの IEEE 802.1 p 優先度レベルとオプションのフロー制御アルゴリズムを定義します。

    詳細については、「[優先度レベルとフロー制御](priority-levels-and-flow-control.md)」を参照してください。

-   Traffic selection algorithm (TSA) の設定。 これらの設定は、ネットワークアダプターが送信キューから送信トラフィックを選択する方法を定義します。 たとえば、アダプターは、厳密な優先順位の TSA を使用して、IEEE 802.1 p の優先順位のみに基づいて送信パケットを選択できます。 また、アダプターは、帯域幅の割り当てに基づいてトラフィッククラス間でトラフィックを軽減する、Enhanced 伝送選択 (TSA) を使用することもできます。

    詳細については、「[伝送選択アルゴリズム (TSAs)](transmission-selection-algorithms--tsas-.md)」を参照してください。

-   EtherType や宛先の TCP ポートなど、分類条件に一致するデータを含むパケットに対する IEEE 802.1 p の優先度レベルの割り当てを指定するトラフィック分類。 詳細については、「 [NDIS QoS Traffic 分類](ndis-qos-traffic-classifications.md)」を参照してください。

    **注**  トラフィックの分類は、IEEE 802.1 仕様では "アプリケーションの優先度" とも呼ばれます。

     

NDIS QoS では、次の種類のパラメーターを定義します。

<a href="" id="local-ndis-qos-parameters"></a>ローカル NDIS QoS パラメーター  
ローカル NDIS QoS パラメーターは、ミニポートドライバーとそのネットワークアダプターのコア QoS 設定を指定します。 これらのパラメーターはシステムレジストリに保持され、次の方法でミニポートドライバーにローカルに管理されます。

-   DCB コンポーネントによって発行された[\_QOS\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-parameters)を使用して、NDIS オブジェクト識別子 (oid) メソッドの要求を処理します。 この OID 要求には、ローカル NDIS QoS パラメーターを指定する[**ndis\_QOS\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体が含まれています。

    DCB コンポーネントの詳細については、「[データセンターブリッジングの NDIS QoS アーキテクチャ](ndis-qos-architecture-for-data-center-bridging.md)」を参照してください。

-   ネットワークアダプターの独自のレジストリ設定を使用します。 ミニポートドライバーは、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数が NDIS によって呼び出されたときに、これらの設定を読み取ります。

-   独立系ハードウェアベンダー (IHV) によって開発された管理アプリケーションを使用してミニポートドライバーに発行された設定を使用します。

ミニポートドライバーがローカル NDIS QoS パラメーターを取得する方法の詳細については、「[ローカル Ndis Qos パラメーターの設定](setting-local-ndis-qos-parameters.md)」を参照してください。

<a href="" id="remote-ndis-qos-parameters"></a>リモート NDIS QoS パラメーター  
リモート NDIS QoS パラメーターは、ネットワークアダプターがデータリンク経由で接続されているリモートピアで構成されているものです。 ミニポートドライバーは、IEEE 802.1 Qaz draft standard によって指定されたデータセンターブリッジング (DCBX) プロトコルを使用してこれらのパラメーターを検出します。

DCBX を行うには、ミニポートドライバーが1つのデータリンクピアから受信したリモート QoS パラメーターのセットを1つだけ保持する必要があります。 ミニポートドライバーは、そのリモート QoS パラメーターがピアから受信された場合、または後で変更された場合に、NDIS ステータスを示す値を発行する必要があります。 たとえば、リモートピアから異なる QoS パラメーターのセットを受信したため、ドライバーによってリモート NDIS QoS パラメーターが変更される可能性があります。 このプロセスの詳細については、「[リモート NDIS QoS パラメーターの変更を示す](indicating-changes-to-the-remote-ndis-qos-parameters.md)」を参照してください。

ミニポートドライバーがリモート NDIS QoS パラメーターを取得する方法の詳細については、「[リモート Ndis Qos パラメーターの受信](receiving-remote-ndis-qos-parameters.md)」を参照してください。

<a href="" id="operational-ndis-qos-parameters"></a>運用 NDIS QoS パラメーター  
Operational NDIS QoS パラメーターは、リモートピアへのデータリンク接続を介して、ミニポートドライバーがトラフィックの優先順位付けを解決するものです。 ミニポートドライバーは、ローカルまたはリモートの NDIS QoS パラメーターから、動作している NDIS QoS パラメーターを解決します。

ミニポートドライバーは、動作中の QoS パラメーターが最初に解決されたとき、または後で変更されたときに、NDIS ステータスを示す値を発行する必要があります。 たとえば、ドライバーは、リモートピアから異なる QoS パラメーターのセットを受信したため、動作している NDIS QoS パラメーターを変更する場合があります。 このステータス表示を生成する方法の詳細については、「 [OPERATIONAL NDIS QoS パラメーターの変更を示す](indicating-changes-to-the-operational-ndis-qos-parameters.md)」を参照してください。

ミニポートドライバーが運用 NDIS QoS パラメーターを解決する方法の詳細については、「[運用 Ndis Qos パラメーターの解決](resolving-operational-ndis-qos-parameters.md)」を参照してください。

 

 






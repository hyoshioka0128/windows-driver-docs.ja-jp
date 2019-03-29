---
title: NDIS QoS トラフィック分類
description: NDIS QoS トラフィック分類
ms.assetid: 62D7B69F-A64E-4E3C-9AEA-8C56495E3FF5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4179312c64f862ec8fc7409bb9e63cbc191faf1f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574912"
---
# <a name="ndis-qos-traffic-classifications"></a>NDIS QoS トラフィック分類


NDIS サービスの品質 (QoS) は、送信、分類または*エグレス*パケットのネットワーク アダプターで優先順位の高い配信します。 各トラフィックの分類では、次の項目を指定します。

-   分類を*条件*エグレス パケット データ内のデータのパターンに基づきます。

    NDIS 6.30 以降、分類の条件は、16 ビット値に基づくが、UDP または TCP 宛先ポートなど、メディア アクセス制御 (MAC) EtherType します。

-   分類を*アクション*エグレス パケットを処理するために使用されるトラフィック クラスを定義します。

    NDIS 6.30 以降、分類アクションは、802.1 p の優先度レベルを指定します。

**注**  トラフィックの分類は、IEEE 802.1 仕様で「アプリケーションの優先順位」でとも呼ばれます。

 

NDIS QoS トラフィックの分類は、次の種類のパケットのエグレス トラフィックを意図しています。

-   Fibre Channel over Ethernet (FCoE)、iSCSI のパケットなど、ミニポート ドライバーにオフロードされるトラフィックに基づいてパケット。

-   パケットを管理および RDMA など、ミニポート ドライバーによって適用されている接続に基づきます。

NDIS QoS トラフィックの分類は、オペレーティング システムによって生成された TCP/IP トラフィック用のものではありません、ため、ミニポート ドライバーがパケット インスペクションを実行する必要はありません。 代わりに、分類の条件には、オフロードまたはドライバーによって管理されたパケットの種類が一致すると、単に適用できる分類アクションその型に属しているすべてのパケットに。 たとえば、FCoE オフロードと分類の条件のミニポート ドライバーが有効になっている場合は、iSCSI の TCP ポート番号 (860 または 3260)、ドライバー エグレス iSCSI のすべてのパケットを分類アクションに対して定義された優先順位の優先順位を指定します。

DCB コンポーネント (Msdcb.sys) の OID メソッド要求を通じてトラフィックの分類を指定する[OID\_QOS\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/hh451835)します。 この OID 要求に含まれる、 [ **NDIS\_QOS\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451640)構造体の配列を指定する[ **NDIS\_QOS\_分類\_要素**](https://msdn.microsoft.com/library/windows/hardware/hh451631)構造体。 各構造体には、トラフィックの分類を定義します。

DCB のコンポーネントを指定します、*既定*トラフィックの分類を他の分類の条件と一致しないすべての送信パケットに適用されます。 この場合、ネットワーク アダプターは、これらの送信パケットに既定の分類に関連付けられている IEEE 802.1p の優先度レベルを割り当てます。 既定のトラフィックの分類には、次の属性があります。

-   NDIS の種類のトラフィックの分類の条件が\_QOS\_条件\_既定します。

-   配列で定義されている最初のトラフィックの分類が[ **NDIS\_QOS\_分類\_要素**](https://msdn.microsoft.com/library/windows/hardware/hh451631)構造体。

DCB のコンポーネントの詳細については、次を参照してください。[データ センター ブリッジングの NDIS QoS アーキテクチャ](ndis-qos-architecture-for-data-center-bridging.md)します。

 

 






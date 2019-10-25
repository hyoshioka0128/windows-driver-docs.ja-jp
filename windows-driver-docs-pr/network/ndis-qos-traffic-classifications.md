---
title: NDIS QoS トラフィック分類
description: NDIS QoS トラフィック分類
ms.assetid: 62D7B69F-A64E-4E3C-9AEA-8C56495E3FF5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e73997b4c89156475665ff7efde7215cc00a3a74
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833767"
---
# <a name="ndis-qos-traffic-classifications"></a>NDIS QoS トラフィック分類


NDIS Quality of Service (QoS) は、ネットワークアダプターによる優先順位の高い送信*パケットまたは*送信パケットを分類します。 各トラフィック分類では、次のことを指定します。

-   送信パケットデータ内のデータパターンに基づく分類*条件*。

    NDIS 6.30 以降では、分類条件は、UDP または TCP 宛先ポートやメディアアクセス制御 (MAC) EtherType などの16ビット値に基づいています。

-   送信パケットの処理に使用する traffic クラスを定義する分類*アクション*。

    NDIS 6.30 以降では、分類アクションは 802.1 p 優先度レベルを指定します。

**注**  トラフィックの分類は、IEEE 802.1 仕様では "アプリケーションの優先度" とも呼ばれます。

 

NDIS QoS トラフィック分類は、次の種類の送信パケットトラフィックを対象としています。

-   ミニポートドライバーにオフロードされたトラフィックに基づくパケット (ファイバーチャネル over Ethernet (FCoE) や iSCSI パケットなど)。

-   RDMA などのミニポートドライバーによって管理および適用される接続に基づくパケット。

NDIS QoS トラフィック分類は、オペレーティングシステムによって生成される TCP/IP トラフィックを想定していないため、ミニポートドライバーはパケット検査を実行する必要はありません。 その代わりに、ドライバーによってオフロードまたは管理されているパケットの種類に分類条件が一致する場合は、その種類に属するすべてのパケットに分類アクションを適用するだけで済みます。 たとえば、ミニポートドライバーで FCoE のオフロードが有効になっていて、分類条件で iSCSI TCP ポート番号 (860 または 3260) が指定されている場合、ドライバーは、分類アクションに対して定義された優先度レベルで、すべての送信 iSCSI パケットの優先順位を設定します。

DCB コンポーネント (Msdcb) は、 [oid\_QOS\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-parameters)を使用して、トラフィックの分類を指定します。 この OID 要求には、ndis [ **\_qos\_分類\_要素**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_classification_element)構造の配列を指定する、 [**ndis\_qos\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体が含まれています。 これらの各構造体は、トラフィックの分類を定義します。

DCB コンポーネントは、他の分類条件に一致しないすべての送信パケットに適用される*既定*のトラフィック分類を指定します。 この場合、ネットワークアダプターによって、既定の分類に関連付けられている IEEE 802.1 p の優先度レベルが、これらの送信パケットに割り当てられます。 既定のトラフィック分類には、次の属性があります。

-   これには、種類が NDIS\_QOS\_CONDITION のトラフィック分類条件\_既定値が含まれています。

-   これは、 [**NDIS\_QOS\_分類\_要素**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_classification_element)構造体の配列で定義されている最初のトラフィック分類です。

DCB コンポーネントの詳細については、「[データセンターブリッジングの NDIS QoS アーキテクチャ](ndis-qos-architecture-for-data-center-bridging.md)」を参照してください。

 

 






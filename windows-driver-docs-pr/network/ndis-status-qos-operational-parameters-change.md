---
title: NDIS_STATUS_QOS_OPERATIONAL_PARAMETERS_CHANGE
description: NDIS サービスの品質 (QoS) をサポートしているミニポート ドライバーは、その運用上の NDIS QoS パラメーターは、最初に解決または後で変更されたときに、NDIS_STATUS_QOS_OPERATIONAL_PARAMETERS_CHANGE 状態を示す値を発行します。
ms.assetid: 15D2B139-1AEA-4252-8599-0EA4ED2E3733
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_QOS_OPERATIONAL_PARAMETERS_CHANGE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 1258a6f692f5d4052d69fa615d1230c83dcb0761
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368511"
---
# <a name="ndisstatusqosoperationalparameterschange"></a>NDIS\_状態\_QOS\_運用\_パラメーター\_変更


NDIS サービスの品質 (QoS) の問題をサポートしているミニポート ドライバー、 **NDIS\_状態\_QOS\_運用\_パラメーター\_変更**状態表示ときに、運用上の NDIS QoS パラメーターは、最初に解決または後で変更します。 ミニポート ドライバーでは、QoS パケットの転送を実行するこれらのオペレーションのパラメーターをネットワーク アダプターを構成します。

ミニポート ドライバーはこの状態表示を行うときに、設定、 **StatusBuffer**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)構造体へのポインターを[ **NDIS\_QOS\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体。 ドライバーでは、その運用上の NDIS QoS パラメーターを持つこの構造体を初期化します。

**注**  この NDIS 状態の表示は、IEEE 802.1 データ センター ブリッジング (DCB) インターフェイスをサポートするミニポート ドライバーでのみ有効です。

 

<a name="remarks"></a>コメント
-------

ミニポート ドライバーの問題、 **NDIS\_状態\_QOS\_運用\_パラメーター\_変更**次の条件の状態を示す値。

-   ミニポート ドライバーを発行する必要があります、 **NDIS\_状態\_QOS\_運用\_パラメーター\_変更**状態を示す値が最初に解決された後、運用上の NDIS QoS パラメーターとそれらにネットワーク アダプターを構成します。

-   この最初の状態を示す値後、ミニポート ドライバーを発行する必要があります、 **NDIS\_状態\_QOS\_OPERATIONAL\_パラメーター\_変更**状態を示す値とその運用上の NDIS QoS パラメーターが変更されます。 これは、ローカルまたはリモートの NDIS QoS パラメーターのいずれかが変更されたときに発生します。

-   ミニポート ドライバーでは、データ センター ブリッジング (DCB) コンポーネント (Msdcb.sys) のオブジェクト識別子 (OID) メソッド要求を発行するときに、Windows オペレーティング システムからローカルの NDIS QoS パラメーターを取得[OID\_QOS\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-parameters)します。 この OID 要求に含まれる、 [ **NDIS\_QOS\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_qos_parameters)をローカルの NDIS QoS パラメーターを指定します。

    ミニポート ドライバーがあるその運用上の NDIS QoS パラメーターを解決するときに、ローカルの NDIS QoS パラメーターを上書きする場合があります。 これは、ローカルの QoS パラメーターの基になるプロトコルまたはネットワーク アダプターで現在有効になっているテクノロジで使用されている運用面の QoS パラメーターを危険にさらす場合に特に当てはまります。 たとえば、ドライバーは、Ethernet (FCoE) プロトコル経由でファイバー チャネル経由のリモート ブート用にネットワーク アダプターが有効になっている場合、ローカル QoS パラメーターをオーバーライドできます。

    ミニポート ドライバーに通知を発行して、ローカルの NDIS QoS パラメーターをオーバーライドする意向上にあるドライバーの NDIS および、 **NDIS\_状態\_QOS\_OPERATIONAL\_パラメーター\_変更**状態を示す値。

    詳細については、次を参照してください。 [NDIS QoS パラメーターを管理する](https://docs.microsoft.com/windows-hardware/drivers/network/managing-ndis-qos--parameters)します。

**注**  重なってドライバーを使用できます、 **NDIS\_状態\_QOS\_運用\_パラメーター\_変更**に状態を示す値運用上の NDIS QoS パラメーターを決定します。 または、これらのドライバーにはの OID クエリ要求が発行できますも[OID\_QOS\_運用\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-operational-parameters)をいつでも運用の NDIS QoS パラメーターを取得します。

 

ミニポート ドライバーの問題については、 **NDIS\_状態\_QOS\_運用\_パラメーター\_変更**状態を示す値を参照してください[運用上の NDIS QoS パラメーターへの変更を示す](https://docs.microsoft.com/windows-hardware/drivers/network/indicating-changes-to-the-operational-ndis-qos-parameters)します。

NDIS QoS パラメーターのさまざまな種類の詳細については、次を参照してください。 [NDIS QoS パラメーターの概要](https://docs.microsoft.com/windows-hardware/drivers/network/overview-of-ndis-qos-parameters)します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>NDIS 6.30 以降をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h (Ndis.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


****
[**NDIS\_状態\_を示す値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)

[**NDIS\_QOS\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_qos_parameters)

[OID\_QOS\_OPERATIONAL\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-operational-parameters)

 

 





---
title: NDIS_STATUS_QOS_OPERATIONAL_PARAMETERS_CHANGE
description: NDIS Quality of Service (QoS) をサポートするミニポートドライバーは、運用 NDIS QoS パラメーターが最初に解決されるか、後で変更されるときに、NDIS_STATUS_QOS_OPERATIONAL_PARAMETERS_CHANGE 状態を示します。
ms.assetid: 15D2B139-1AEA-4252-8599-0EA4ED2E3733
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_QOS_OPERATIONAL_PARAMETERS_CHANGE ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 9e537e9f05b1705aa252503b880e5ec670e1a7e1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843529"
---
# <a name="ndis_status_qos_operational_parameters_change"></a>NDIS\_ステータス\_QOS\_操作\_パラメーター\_変更


NDIS Quality of Service (QoS) をサポートするミニポートドライバーでは、 **ndis\_の状態\_qos\_操作\_\_パラメーター**に関する問題が発生しています。また、動作している ndis QoS パラメーターが解決されると、状態が変化します初めての場合、または後で変更した場合。 ミニポートドライバーは、これらの操作パラメーターを使用してネットワークアダプターを構成し、QoS パケット転送を実行します。

ミニポートドライバーによってこの状態が示されると、 [**ndis\_ステータス\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)表示構造体の**statusbuffer**メンバーが、 [**ndis\_QOS\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体へのポインターに設定されます。 この構造体は、動作する NDIS QoS パラメーターを使用して初期化されます。

この NDIS 状態の表示は、IEEE 802.1 データセンターブリッジング (DCB) インターフェイスをサポートするミニポートドライバーに対してのみ有効である  に**注意**してください。

 

<a name="remarks"></a>注釈
-------

ミニポートドライバーは、次の条件に従って、 **QOS\_操作\_\_パラメーター\_、NDIS\_の状態**を発行して、変更の状態を示します。

-   ミニポートドライバーは、 **ndis\_の状態\_QOS\_操作\_パラメーター**を発行する必要があります。また、動作している ndis qos パラメーターを最初に解決してネットワークを構成した後に、状態の表示を変更\_ます。アダプターを使用します。

-   この初期状態を示すと、ミニポートドライバーは、 **ndis\_ステータス\_QOS\_操作\_\_パラメーター**を発行する必要があります。また、動作している ndis QOS パラメーターが変更された場合は、状態が変化します。 これは、ローカルまたはリモートの NDIS QoS パラメーターが変更された場合に発生する可能性があります。

-   ミニポートドライバーは、データセンターブリッジング (DCB) コンポーネント (Msdcb) が Oid のオブジェクト識別子 (OID) メソッド要求を発行するときに、Windows オペレーティングシステムからローカル NDIS QoS パラメーターを取得します。これは、 [QoS\_パラメーター\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-parameters)です。 この OID 要求には、ローカル NDIS QoS パラメーターを指定する[**ndis\_QOS\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体が含まれています。

    場合によっては、動作している NDIS QoS パラメーターを解決するときに、ミニポートドライバーがローカル NDIS QoS パラメーターを上書きする必要があります。 これは、ネットワークアダプターで現在有効になっている、基になるプロトコルまたはテクノロジによって使用されている操作の QoS パラメーターをローカル QoS パラメーターが損なう場合に特に当てはまります。 たとえば、ネットワークアダプターでファイバーチャネル over Ethernet (FCoE) プロトコルによるリモートブートが有効になっている場合、ドライバーはローカルの QoS パラメーターを上書きできます。

    ミニポートドライバーは、ndis およびそれ以降のドライバーに対して、ndis **\_の状態\_qos\_操作\_\_パラメーター**を発行して、ローカル ndis QoS パラメーターを上書きすることを意図しています。

    詳細については、「 [NDIS QoS パラメーターの管理](https://docs.microsoft.com/windows-hardware/drivers/network/managing-ndis-qos--parameters)」を参照してください。

**注**  は、 **NDIS\_の状態\_QOS\_操作\_パラメーター**を使用して、動作している ndis qos パラメーターを決定するように状態を変更\_ます。 また、これらのドライバーは[oid\_QOS\_操作\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-operational-parameters)の oid クエリ要求を発行して、いつでも運用 NDIS QOS パラメーターを取得することもできます。

 

ミニポートドライバーが NDIS\_の状態\_どのように発行するかについては、 **qos\_操作\_パラメーター\_変更**の状態の表示については、「 [Operational NDIS QOS パラメーターの変更を示す](https://docs.microsoft.com/windows-hardware/drivers/network/indicating-changes-to-the-operational-ndis-qos-parameters)」を参照してください。

さまざまな種類の NDIS QoS パラメーターの詳細については、「 [Ndis Qos パラメーターの概要](https://docs.microsoft.com/windows-hardware/drivers/network/overview-of-ndis-qos-parameters)」を参照してください。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>NDIS 6.30 以降でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis .h (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


****
[**NDIS\_状態\_表示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[**NDIS\_QOS\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)

[OID\_QOS\_操作\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-operational-parameters)

 

 





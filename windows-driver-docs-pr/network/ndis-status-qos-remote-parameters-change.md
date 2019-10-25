---
title: NDIS_STATUS_QOS_REMOTE_PARAMETERS_CHANGE
description: NDIS Quality of Service (QoS) をサポートするミニポートドライバーは、リモート NDIS QoS パラメーターがピアから受信されたとき、または後で変更されたときに、NDIS_STATUS_QOS_REMOTE_PARAMETERS_CHANGE 状態を示します。
ms.assetid: 3DA5F4FA-193F-4716-8678-7B6FB833E68E
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_QOS_REMOTE_PARAMETERS_CHANGE ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 80746117e4c132f9af3598438a4c273f11dbbf48
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843527"
---
# <a name="ndis_status_qos_remote_parameters_change"></a>NDIS\_ステータス\_QOS\_リモート\_パラメーター\_変更


NDIS Quality of Service (QoS) をサポートするミニポートドライバーでは、 **ndis\_の状態\_qos\_リモート\_\_パラメーター**に関する問題が発生し、そのリモート NDIS QoS パラメーターがピアから受信されたときに状態が示されます。初めての場合、または後で変更する場合。 ミニポートドライバーは、IEEE 802.1 Qaz Data Center ブリッジング Exchange (DCBX) プロトコルを使用して、リモートピアからこれらの QoS パラメーターを受信します。

ミニポートドライバーによってこの状態が示されると、 [**ndis\_ステータス\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)表示構造体の**statusbuffer**メンバーが、 [**ndis\_QOS\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体へのポインターに設定されます。 ドライバーは、リモート NDIS QoS パラメーターを使用して、この構造体を初期化します。

この NDIS 状態の表示は、IEEE 802.1 データセンターブリッジング (DCB) インターフェイスをサポートするミニポートドライバーに対してのみ有効である  に**注意**してください。

 

<a name="remarks"></a>注釈
-------

ミニポートドライバーは、DCBX プロトコルを使用して、リモートピアの QoS パラメーターを受信します。 ミニポートドライバーは、ローカルおよびリモートの QoS 設定に基づいて、動作している NDIS QoS パラメーターを解決します。 操作パラメーターが解決されると、ミニポートドライバーは、これらのパラメーターを使用して QoS パケット転送用にネットワークアダプターを構成します。

ドライバーが動作している NDIS QoS パラメーター設定を解決する方法の詳細については、「[運用 Ndis Qos パラメーターの解決](https://docs.microsoft.com/windows-hardware/drivers/network/resolving-operational-ndis-qos-parameters)」を参照してください。

ミニポートドライバーは、次のガイドラインに従って、 **NDIS\_ステータス\_QOS\_リモート\_パラメーター**を発行して、状態の表示を変更\_必要があります。

-   ミニポートドライバーがリモートピアから DCBX フレームを受信していない場合は、 **NDIS\_ステータス\_QOS\_リモート\_パラメーター**を発行して、状態の表示を変更\_ことはできません。

-   ミニポートドライバーは、リモートピアから QoS 設定を最初に受信した後に、 **\_リモート\_\_パラメーター\_NDIS\_状態**を発行する必要があります。

    ネットワークアダプターがピアからリモート QoS パラメーター設定を受信してから、ドライバーのローカル QoS パラメーターが設定されている場合は、ミニポートドライバーがこの状態を**確認**する必要が  ます。 詳細については、「[ローカル NDIS QoS パラメーターの設定](https://docs.microsoft.com/windows-hardware/drivers/network/setting-local-ndis-qos-parameters)」を参照してください。

     

-   この初期状態を示すと、ミニポートドライバーは、リモートピアの QoS 設定の変更を判断したときに、 **\_qos\_リモート\_\_パラメーターの NDIS\_状態**のみを発行する必要があります。

    **注**  ミニポートドライバーでは、 **NDIS\_の状態\_QOS\_リモート\_のパラメーター**を発行しないでください。リモート NDIS QOS のパラメーターに変更がない場合は、状態の表示を変更します。 ドライバーがこの種類の状態を示している場合、NDIS は、このような指示を後続のドライバーに渡すことはできません。

     

**注**  は、 **ndis\_status\_QOS\_リモート\_パラメーター**を使用して、リモートの ndis QOS パラメーターを確認するための状態の表示\_変更します。 また、これらのドライバーは[oid\_QOS\_リモート\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-remote-parameters)の oid クエリ要求を発行して、リモート NDIS QOS パラメーターをいつでも取得することもできます。

 

ミニポートドライバーが**NDIS\_の状態\_\_** どのように発行するかの詳細については、「リモート\_パラメーター\_変更の状態を[示す](https://docs.microsoft.com/windows-hardware/drivers/network/indicating-changes-to-the-remote-ndis-qos-parameters)」を参照してください。

リモート NDIS QoS パラメーターの詳細については、「 [Ndis Qos パラメーターの概要](https://docs.microsoft.com/windows-hardware/drivers/network/overview-of-ndis-qos-parameters)」を参照してください。

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

[OID\_QOS\_リモート\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-remote-parameters)

 

 





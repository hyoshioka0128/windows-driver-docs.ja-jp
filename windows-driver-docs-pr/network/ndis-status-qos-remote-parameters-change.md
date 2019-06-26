---
title: NDIS_STATUS_QOS_REMOTE_PARAMETERS_CHANGE
description: NDIS サービスの品質 (QoS) をサポートしているミニポート ドライバーは、そのリモートの NDIS QoS パラメーターは、最初に、ピアから受信したか、または後で変更するときに NDIS_STATUS_QOS_REMOTE_PARAMETERS_CHANGE 状態を示す値を発行します。
ms.assetid: 3DA5F4FA-193F-4716-8678-7B6FB833E68E
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_QOS_REMOTE_PARAMETERS_CHANGE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: b5246fc3d5d960193b5b12263e1ed263bc074a36
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381196"
---
# <a name="ndisstatusqosremoteparameterschange"></a>NDIS\_状態\_QOS\_リモート\_パラメーター\_変更


NDIS サービスの品質 (QoS) の問題をサポートしているミニポート ドライバー、 **NDIS\_状態\_QOS\_リモート\_パラメーター\_変更**状態を示す値とそのリモートの NDIS QoS パラメーターは、最初に、ピアから受信したか、または後で変更します。 ミニポート ドライバーでは、これらの QoS パラメーターを受け取る IEEE 802.1 qaz を通じてリモート ピアから Data Center Bridging Exchange (DCBX) プロトコル。

ミニポート ドライバーはこの状態表示を行うときに、設定、 **StatusBuffer**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)構造体へのポインターを[ **NDIS\_QOS\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体。 ドライバーでは、そのリモートの NDIS QoS パラメーターを持つこの構造体を初期化します。

**注**  この NDIS 状態の表示は、IEEE 802.1 データ センター ブリッジング (DCB) インターフェイスをサポートするミニポート ドライバーでのみ有効です。

 

<a name="remarks"></a>コメント
-------

ミニポート ドライバーでは、DCBX プロトコルを使用して、リモート ピアの QoS パラメーターを受信します。 ミニポート ドライバーでは、そのローカルおよびリモートの QoS 設定に基づき、運用の NDIS QoS パラメーターを解決します。 オペレーションのパラメーターが解決されると、ミニポート ドライバーは、QoS パケット転送のこれらのパラメーターを持つネットワーク アダプターを構成します。

ドライバーがその運用上の NDIS QoS パラメーター設定を解決する方法の詳細については、次を参照してください。[運用上の NDIS QoS パラメーターを解決する](https://docs.microsoft.com/windows-hardware/drivers/network/resolving-operational-ndis-qos-parameters)します。

ミニポート ドライバーが発行するための次のガイドラインに従う必要があります、 **NDIS\_状態\_QOS\_リモート\_パラメーター\_変更**状態を示す値。

-   発行する必要があります、ミニポート ドライバーは、リモート ピアから DCBX フレームを受信しないが場合、 **NDIS\_状態\_QOS\_リモート\_パラメーター\_変更**状態示します。

-   ミニポート ドライバーを発行する必要があります、 **NDIS\_状態\_QOS\_リモート\_パラメーター\_変更**から QoS の設定が最初に受信した後の状態を示す値をリモート ピア。

    **注**  ネットワーク アダプターは、ドライバーのローカルの QoS パラメーターを設定する前に、ピアからリモートの QoS パラメーター設定を受信する場合、ミニポート ドライバーはこの状態を示す値を発行する必要があります。 詳細については、次を参照してください。 [NDIS QoS パラメーターをローカル設定](https://docs.microsoft.com/windows-hardware/drivers/network/setting-local-ndis-qos-parameters)します。

     

-   この初期状態を示す値を後に、ミニポート ドライバーを発行する必要がありますのみ、 **NDIS\_状態\_QOS\_リモート\_パラメーター\_変更**状態を示す値とリモート ピアの QoS の設定の変更が決定します。

    **注**  ミニポート ドライバーが発行する必要があります、 **NDIS\_状態\_QOS\_リモート\_パラメーター\_変更**状態表示場合リモートの NDIS QoS パラメーターに変更はありませんがあります。 場合は、ドライバーはこの種類の状態表示するには、NDIS が重なってドライバーを示す値を渡すことができません。

     

**注**  重なってドライバーを使用できます、 **NDIS\_状態\_QOS\_リモート\_パラメーター\_変更**に状態を示す値リモートの NDIS QoS パラメーターを決定します。 または、これらのドライバーにはの OID クエリ要求が発行できますも[OID\_QOS\_リモート\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-remote-parameters)をいつでも、リモートの NDIS QoS パラメーターを取得します。

 

ミニポート ドライバーの問題の詳細については、 **NDIS\_状態\_QOS\_リモート\_パラメーター\_変更**状態を示す値を参照してください[リモートの NDIS QoS パラメーターへの変更を示す](https://docs.microsoft.com/windows-hardware/drivers/network/indicating-changes-to-the-remote-ndis-qos-parameters)します。

リモートの NDIS QoS パラメーターの詳細については、次を参照してください。 [NDIS QoS パラメーターの概要](https://docs.microsoft.com/windows-hardware/drivers/network/overview-of-ndis-qos-parameters)します。

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

[OID\_QOS\_リモート\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-remote-parameters)

 

 





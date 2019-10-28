---
title: NDIS_STATUS_NIC_SWITCH_CURRENT_CAPABILITIES
description: NDIS_STATUS_NIC_SWITCH_CURRENT_CAPABILITIES の状態は、ネットワークアダプターの NIC スイッチで現在有効になっているハードウェア機能が変更されたことを、NDIS およびそれ以降のドライバーに示します。
ms.assetid: 8F5DF045-4993-45E6-A5B9-502B695E3C62
ms.date: 08/08/2017
keywords: -Windows Vista 以降の NDIS_STATUS_NIC_SWITCH_CURRENT_CAPABILITIES ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 2787a2717480edef70ae77994b77bf8928067efe
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842780"
---
# <a name="ndis_status_nic_switch_current_capabilities"></a>NDIS\_STATUS\_NIC\_スイッチ\_現在の\_機能


**Ndis\_STATUS\_NIC\_スイッチ\_現在の\_機能**の状態は、ネットワークアダプターの nic スイッチで現在有効になっているハードウェア機能が変更されたことを ndis およびそれ以降のドライバーに示します。

状態の表示は、ネットワークアダプターの PCI Express (PCIe) 物理機能 (PF) のミニポートドライバーによって行われます。 PF ミニポートドライバーは、Hyper-v の親パーティションの管理オペレーティングシステムで実行されます。

<a name="remarks"></a>注釈
-------

PF ミニポートドライバーは、 **NDIS\_の状態\_nic\_\_スイッチ**に発行する必要があります。これは、現在の\_の nic スイッチで現在有効になっているハードウェア機能に対する変更が検出されるたびに、ネットワークアダプター。 これらの機能は、次のいずれかの条件に該当する場合に変更される可能性があります。

-   現在有効になっている NIC スイッチのハードウェア機能は、独立系ハードウェアベンダー (IHV) によって開発された管理アプリケーションを通じて変更されます。

-   現在有効になっている NIC スイッチのハードウェア機能は、MUX 中間ドライバーによって管理される負荷分散フェールオーバー (LBFO) チームに属する1つまたは複数のネットワークアダプターに対して変更されます。 詳細については、「 [NDIS MUX 中間ドライバー](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-mux-intermediate-drivers)」を参照してください。

PF ミニポートドライバーによって、 **NDIS\_status\_NIC\_\_スイッチ**が発行されると、現在の\_の機能の状態が表示されます。そのためには、次の手順を実行する必要があります。

1.  ミニポートドライバーは、ネットワークアダプターの NIC スイッチで現在有効になっているハードウェア機能を使用して、 [**NDIS\_nic\_スイッチ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)の構造を初期化します。
2.  ミニポートドライバーは、次の方法で[**NDIS\_ステータス\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)構造体を初期化します。

    -   **StatusCode**メンバーを**NDIS\_STATUS\_NIC\_スイッチ\_現在の\_機能**に設定する必要があります。

    -   **Statusbuffer**メンバーは、 [**NDIS\_NIC\_SWITCH\_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)構造体へのポインターに設定する必要があります。 この構造体には、NIC スイッチの現在有効なハードウェア機能が含まれています。

    -   **Statusbuffersize**メンバーは、Sizeof ([**NDIS\_NIC\_スイッチ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)) に設定する必要があります。

3.  PF ミニポートドライバーは、 [**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)を呼び出すことによって状態通知を発行します。 ドライバーは、 [**NDIS\_STATUS\_を示す**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)ポインターを*statusindication*パラメーターに渡す必要があります。

これまでのドライバーでは、 **NDIS\_status\_NIC\_スイッチ**を使用して\_現在の\_機能の状態を表示し、ネットワークアダプターで現在有効になっている nic スイッチの機能を確認できます。 また、これらのドライバーは[oid\_\_NIC](oid-nic-switch-current-capabilities.md)の oid クエリ要求を発行することもでき\_現在の\_機能を使用して、いつでもこれらの機能を取得できます。

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
<td>Ndis. h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


****
[**NDIS\_NIC\_スイッチ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)

[**NDIS\_状態\_表示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[OID\_NIC\_スイッチ\_現在の\_機能](oid-nic-switch-current-capabilities.md)

 

 





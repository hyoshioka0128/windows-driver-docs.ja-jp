---
title: NDIS_STATUS_NIC_SWITCH_HARDWARE_CAPABILITIES
description: NDIS_STATUS_NIC_SWITCH_HARDWARE_CAPABILITIES の状態は、ネットワークアダプターの NIC スイッチのハードウェア機能が変更されたことを、NDIS およびそれ以降のドライバーに示します。
ms.assetid: 21B326EC-22CC-4E41-895F-457971202C0B
ms.date: 08/08/2017
keywords: -Windows Vista 以降の NDIS_STATUS_NIC_SWITCH_HARDWARE_CAPABILITIES ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 978b74796c3f5fd45f4f1266f66488e532c60958
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842782"
---
# <a name="ndis_status_nic_switch_hardware_capabilities"></a>NDIS\_STATUS\_NIC\_スイッチ\_ハードウェア\_機能


**Ndis\_STATUS\_nic\_スイッチ\_ハードウェア\_機能**の状態は、ネットワークアダプターの nic スイッチのハードウェア機能が変更されたことを ndis およびそれ以降のドライバーに示します。 これらの機能には、現在 INF ファイルの設定によって無効にされているハードウェア機能や、 **[詳細設定**] プロパティページがあります。

状態の表示は、ネットワークアダプターの PCI Express (PCIe) 物理機能 (PF) のミニポートドライバーによって行われます。 PF ミニポートドライバーは、Hyper-v の親パーティションの管理オペレーティングシステムで実行されます。

<a name="remarks"></a>注釈
-------

PF ミニポートドライバーは、ネットワークアダプターの NIC スイッチのハードウェア機能の変更を検出するたびに、 **nic\_スイッチ\_ハードウェア\_機能**の状態を示す\_、NDIS\_の状態を発行する必要があります。 これらの機能は、次のいずれかの条件に該当する場合に変更される可能性があります。

-   NIC スイッチのハードウェア機能は、独立系ハードウェアベンダー (IHV) によって開発された管理アプリケーションによって有効または無効になります。

-   MUX 中間ドライバーによって管理される負荷分散フェールオーバー (LBFO) チームに属する1つまたは複数のネットワークアダプターについて、NIC スイッチのハードウェア機能が変更されます。 詳細については、「 [NDIS MUX 中間ドライバー](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-mux-intermediate-drivers)」を参照してください。

PF ミニポートドライバーが**NDIS\_状態\_NIC に発行するとき\_\_ハードウェア\_機能**の状態の表示に切り替えるには、次の手順に従う必要があります。

1.  ミニポートドライバーは、ネットワークアダプターの NIC スイッチのハードウェア機能を使用して、 [**NDIS\_nic\_スイッチ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)の構造を初期化します。
2.  ミニポートドライバーは、次の方法で[**NDIS\_ステータス\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)構造体を初期化します。

    -   **StatusCode**メンバーを**NDIS\_STATUS\_NIC\_スイッチ\_ハードウェア\_機能**に設定する必要があります。

    -   **Statusbuffer**メンバーは、 [**NDIS\_NIC\_SWITCH\_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)構造体へのポインターに設定する必要があります。 この構造体には、NIC スイッチのハードウェア機能が含まれています。

    -   **Statusbuffersize**メンバーは、Sizeof ([**NDIS\_NIC\_スイッチ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)) に設定する必要があります。

3.  PF ミニポートドライバーは、 [**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)を呼び出すことによって状態通知を発行します。 ドライバーは、 [**NDIS\_STATUS\_を示す**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)ポインターを*statusindication*パラメーターに渡す必要があります。

これまでのドライバーでは、 **NDIS\_STATUS\_NIC\_スイッチ\_ハードウェア\_機能**の状態の表示を使用して、ネットワークアダプターで現在有効になっている nic スイッチの機能を特定できます。 また、これらのドライバーは Oid\_NIC の OID クエリ要求を発行して、これらの機能をいつでも取得できるように[ハードウェア\_機能\_\_](oid-nic-switch-hardware-capabilities.md)できます。

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

[OID\_NIC\_スイッチ\_ハードウェア\_機能](oid-nic-switch-hardware-capabilities.md)

 

 





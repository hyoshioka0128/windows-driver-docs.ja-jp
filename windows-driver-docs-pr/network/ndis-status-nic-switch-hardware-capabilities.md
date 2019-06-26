---
title: NDIS_STATUS_NIC_SWITCH_HARDWARE_CAPABILITIES
description: NDIS_STATUS_NIC_SWITCH_HARDWARE_CAPABILITIES 状態は、NDIS とのネットワーク アダプターで NIC スイッチ ハードウェア機能が変更されたドライバーの上にあることを示します。
ms.assetid: 21B326EC-22CC-4E41-895F-457971202C0B
ms.date: 08/08/2017
keywords: -NDIS_STATUS_NIC_SWITCH_HARDWARE_CAPABILITIES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: b72ea7d982eb197a547b0b80bb411a89cf481ea1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368561"
---
# <a name="ndisstatusnicswitchhardwarecapabilities"></a>NDIS\_状態\_NIC\_スイッチ\_ハードウェア\_機能


**NDIS\_状態\_NIC\_スイッチ\_ハードウェア\_機能**NDIS と関連付けたドライバーに状態を示します NIC のハードウェア機能ネットワーク アダプターのスイッチが変更されました。 これらの機能には、INF ファイルの設定、または、現在無効になっているハードウェア機能が含まれる、**詳細**プロパティ ページ。

状態の表示が、ミニポート ドライバーのネットワーク アダプターの PCI Express (PCIe) 物理機能 (PF) によって行われます。 PF のミニポート ドライバーは、HYPER-V 親パーティションの管理オペレーティング システムで実行されます。

<a name="remarks"></a>コメント
-------

PF のミニポート ドライバーを発行する必要があります、 **NDIS\_状態\_NIC\_スイッチ\_ハードウェア\_機能**状態を示す値に変更を検出するたびに、NIC のハードウェア機能は、ネットワーク アダプターに切り替えます。 次の条件のいずれかが true の場合、これらの機能を変更できます。

-   NIC スイッチ ハードウェアの機能では、有効または独立系ハードウェア ベンダー (IHV) によって開発された管理アプリケーションで無効にします。

-   負荷分散マルチプレクサー中間ドライバーによって管理されているフェールオーバー (LBFO) のチームに属している 1 つまたは複数のネットワーク アダプターの NIC スイッチ ハードウェアの機能を変更します。 詳細については、次を参照してください。 [NDIS MUX 中間ドライバー](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-mux-intermediate-drivers)します。

PF のミニポート ドライバーを発行したとき、 **NDIS\_状態\_NIC\_スイッチ\_ハードウェア\_機能**状態を示す値、次の手順に従う必要があります。

1.  ミニポート ドライバーを初期化します、 [ **NDIS\_NIC\_切り替える\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)ネットワーク アダプターの NIC のスイッチのハードウェア機能を含む構造体.
2.  ミニポート ドライバーを初期化します、 [ **NDIS\_状態\_INDICATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)次のように構造体。

    -   **StatusCode**にメンバーを設定する必要があります**NDIS\_状態\_NIC\_スイッチ\_ハードウェア\_機能**します。

    -   **StatusBuffer**へのポインターにメンバーを設定する必要があります、 [ **NDIS\_NIC\_スイッチ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)構造体。 この構造体には、NIC のスイッチのハードウェア機能が含まれています。

    -   **StatusBufferSize** sizeof にメンバーを設定する必要があります ([**NDIS\_NIC\_スイッチ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities))。

3.  PF のミニポート ドライバーが呼び出すことで状態の通知を発行[ **NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex)します。 ドライバーへのポインターを渡す必要があります、 [ **NDIS\_状態\_INDICATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)構造体を*StatusIndication*パラメーター。

後続のドライバーを使用できます、 **NDIS\_状態\_NIC\_切り替える\_ハードウェア\_機能**状態を示す値を現在有効な NIC スイッチの確認ネットワーク アダプターに機能します。 または、これらのドライバーにはの OID クエリ要求が発行できますも[OID\_NIC\_スイッチ\_ハードウェア\_機能](oid-nic-switch-hardware-capabilities.md)をいつでもこれらの機能を取得します。

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
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


****
[**NDIS\_NIC\_スイッチ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)

[**NDIS\_状態\_を示す値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)

[OID\_NIC\_スイッチ\_ハードウェア\_機能](oid-nic-switch-hardware-capabilities.md)

 

 




